---
title: Measuring latency in the Linux network stack between kernel and user space
author: admin
layout: post
date: 2013-12-04
url: /measuring-latency-in-the-linux-network-stack-between-kernel-and-user-space/
categories:
  - 操作系统
tags:
  - latency
  - linux
  - network
  - stack
format: aside

---
一篇量化网络数据延时的很好的文章，在很多场合应该能用到：<https://vilimpoc.org/research/ku-latency/>

原文：

Using the SO_TIMESTAMP option to setsockopt(), we can measure the amount of time it takes the Linux kernel to hand a received network packet off to user space. With the option set, the kernel returns an extra struct timeval to the recvmsg() packet reception function.

At the moment the recvmsg() blocking call returns, the user-space code grabs another timestamp. The time difference between the kernel space and user space timestamps is the network stack&#8217;s latency.

The code also demonstrates the use of SIOCGIFADDR to retrieve the IP address from a named interface.

Key functions used: getopt(), strerror_r(), signal(), socket(), setsockopt(), bind(), recvmsg(), sendto(), gettimeofday().

<div>
  Files
</div>

[ku-latency.c file][1]
  
[send-data.c file][2]

Compiles clean (or should) with:

gcc -o ku-latency ku-latency.c -lrt -Wall

gcc -o send-data send-data.c -lrt -Wall

Usage looks like this:

<div>
  <pre>    Usage: ./ku-latency [-i IP address] [-p port]

           -h          Help.
           -i          Specifies IP address of interface you want to listen to.
           -e          Specifies the ethernet interface name you want to listen to.
           -p          Specifies port number of packets you want to see.

    If neither option is specified (they are both optional), then the program
    will listen on IPADDR_ANY (all interfaces), port 1025.</pre>
</div>

&nbsp;

<div>
  <pre>    ~$ ./send-data
    Not all * required parameters were entered.

    ./send-data accepts the following parameters: 

            * --destination or -d [ip address]
              --port        or -p [port number]          (default: 1025)
              --repeat      or -r [repeat every x msec.] (default: 20)</pre>
</div>

To do the measurements, pop open two Terminal windows and have one run the ku-latency listener and the other run the send-data packet sender.

&nbsp;

<div>
  ku-latency.c
</div>

<div>
  <pre>/*
Copyright (c) 2008, Max Vilimpoc, http://vilimpoc.org/

All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:

    * Redistributions of source code must retain the above
      copyright notice, this list of conditions and the following
      disclaimer.
    * Redistributions in binary form must reproduce the above
      copyright notice, this list of conditions and the following
      disclaimer in the documentation and/or other materials
      provided with the distribution.
    * Neither the name of the author nor the names of its
      contributors may be used to endorse or promote products
      derived from this software without specific prior written
      permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR
CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
*/

#define _XOPEN_SOURCE 600

#include &lt;sys/types.h&gt;
#include &lt;sys/socket.h&gt;
#include &lt;netinet/ip.h&gt;

#include &lt;netinet/in.h&gt;
#include &lt;arpa/inet.h&gt;

#include &lt;sys/time.h&gt;

#include &lt;sys/ioctl.h&gt;
#include &lt;linux/if.h&gt;

#include &lt;unistd.h&gt;
#include &lt;stdio.h&gt;
#include &lt;stdbool.h&gt;
#include &lt;stdint.h&gt;
#include &lt;stdlib.h&gt;
#include &lt;string.h&gt;

#include &lt;signal.h&gt;

#include &lt;getopt.h&gt;

typedef enum
{
    STRERROR_LEN           = 80,
    NUM_LATENCIES          = 32,
    DEFAULT_PORT           = 1025,
} CONSTS;

static int                 inSocket;
static struct sockaddr_in  inInAddr;

static int                 totalUsec;
static int                 totalPackets;

static int                 latencies[NUM_LATENCIES];
static int                 index;
static int                 rollingAverage;

static bool                keepRunning;

void Usage(const char * const progName)
{
    printf("n");
    printf("Usage: %s [-i IP address] [-e ethx] [-p port]n", progName);
    printf("n");
    printf("       -h          Help.n");
    printf("       -i          Specifies IP address of interface you want to listen to.n");
    printf("       -e          Specifies the ethernet interface name you want to listen to.n");
    printf("       -p          Specifies port number of packets you want to see.n");
    printf("n");
    printf("If no option is specified (they are all optional), then the programn");
    printf("will listen on IPADDR_ANY (all interfaces), port 1025.");
    printf("n");
    printf("n");
}

static void printError(int errorCode, const char * const lastFunction)
{
    static char strError[STRERROR_LEN];
    memset(strError, 0, STRERROR_LEN);

    /* Old school. */
    perror(lastFunction);

    /* New school. */
    strerror_r(errorCode, strError, STRERROR_LEN);

    printf(strError);
    printf("n");
}

void catchIntr(int signalNumber)
{
    /* Exit the main loop. */
    keepRunning = false;
}

int main(int argc, char **argv)
{
    int rc = 0;

    /* Defaults */
    inInAddr.sin_addr.s_addr    = INADDR_ANY;
    inInAddr.sin_port           = htons(DEFAULT_PORT);
    inInAddr.sin_family         = AF_INET;

    inSocket = socket(PF_INET, SOCK_DGRAM, 0);
    if (0 &gt; inSocket)
    {
        printf("socket() call failed.n");
        printError(inSocket, "socket");
        rc = -1;
        goto socket_failed;
    }

    /* Process cmdline opts. */
    char *shortOpts = "hi:e:p:";
    int   getoptRet;

    while(-1 != (getoptRet = getopt(argc, argv, shortOpts)))
    {
        switch(getoptRet)
        {
            case 'i':
                inInAddr.sin_addr.s_addr = inet_addr(optarg);
                break;
            case 'e':
                {
                struct ifreq fetchIfInfo;
                memset(&fetchIfInfo, 0, sizeof(struct ifreq));
                memcpy(fetchIfInfo.ifr_name, optarg, IFNAMSIZ - 1);

                /* Fetch the IP address to listen to based on interface name. */
                ioctl(inSocket, SIOCGIFADDR, &fetchIfInfo);

                struct sockaddr_in * const sockInfo = (struct sockaddr_in * const) &fetchIfInfo.ifr_addr;
                inInAddr.sin_addr.s_addr   = sockInfo-&gt;sin_addr.s_addr;
                }
                break;
            case 'p':
                inInAddr.sin_port        = htons(atoi(optarg));
                break;
            case 'h':
            case '?':
            default:
                Usage(argv[0]);
                goto normal_exit;
                break;
        }
    }

    printf("Listening to: %s:%dn", inet_ntoa(inInAddr.sin_addr),
                                    ntohs(inInAddr.sin_port));

    int timestampOn = 1;
    rc = setsockopt(inSocket, SOL_SOCKET, SO_TIMESTAMP, (int *) &timestampOn, sizeof(timestampOn));
    if (0 &gt; rc)
    {
        printf("setsockopt(SO_TIMESTAMP) failed.n");
        printError(rc, "setsockopt");
        goto setsockopt_failed;
    }

    rc = bind(inSocket, (struct sockaddr *) &inInAddr, sizeof(struct sockaddr_in));
    if (0 &gt; rc)
    {
        printf("UDP bind() failed.n");
        printError(rc, "bind");
        goto bind_failed;
    }

    struct msghdr   msg;
    struct iovec    iov;
    char            pktbuf[2048];

    char            ctrl[CMSG_SPACE(sizeof(struct timeval))];
    struct cmsghdr *cmsg = (struct cmsghdr *) &ctrl;

    msg.msg_control      = (char *) ctrl;
    msg.msg_controllen   = sizeof(ctrl);    

    msg.msg_name         = &inInAddr;
    msg.msg_namelen      = sizeof(inInAddr);
    msg.msg_iov          = &iov;
    msg.msg_iovlen       = 1;
    iov.iov_base         = pktbuf;
    iov.iov_len          = sizeof(pktbuf);

    struct timeval  time_kernel, time_user;
    int             timediff;

    printf("Starting main loop.n");

    for(keepRunning = true; keepRunning;)
    {
        rc = recvmsg(inSocket, &msg, 0);

        gettimeofday(&time_user, NULL);

        if (cmsg-&gt;cmsg_level == SOL_SOCKET &&
            cmsg-&gt;cmsg_type  == SCM_TIMESTAMP &&
            cmsg-&gt;cmsg_len   == CMSG_LEN(sizeof(time_kernel))) 
        {
            memcpy(&time_kernel, CMSG_DATA(cmsg), sizeof(time_kernel));
        }

        printf("n");
        printf("time_kernel                  : %d.%06dn", (int) time_kernel.tv_sec, 
                                                           (int) time_kernel.tv_usec);
        printf("time_user                    : %d.%06dn", (int) time_user.tv_sec,   
                                                           (int) time_user.tv_usec);

        timediff      = (time_user.tv_sec - time_kernel.tv_sec) * 1000000 + 
                        (time_user.tv_usec - time_kernel.tv_usec);
        totalUsec    += timediff; 
        ++totalPackets;

        rollingAverage  += timediff;
        rollingAverage  -= latencies[index];
        latencies[index] = timediff;
        index = (index + 1) % NUM_LATENCIES;

        printf("Total Average                : %d/%d = %.2f usn", totalUsec, 
                                                                   totalPackets, 
                                                                   (float) totalUsec / totalPackets);
        printf("Rolling Average (%d samples) : %.2f usn", NUM_LATENCIES, 
                                                           (float) rollingAverage / NUM_LATENCIES);
    }

bind_failed:    
setsockopt_failed:
    close(inSocket);
socket_failed:
normal_exit:
    return rc;
}</pre>
</div>

&nbsp;

<div>
  send-data.c
</div>

<div>
  <pre>/*
Copyright (c) 2008, Max Vilimpoc, http://vilimpoc.org/

All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:

    * Redistributions of source code must retain the above
      copyright notice, this list of conditions and the following
      disclaimer.
    * Redistributions in binary form must reproduce the above
      copyright notice, this list of conditions and the following
      disclaimer in the documentation and/or other materials
      provided with the distribution.
    * Neither the name of the author nor the names of its
      contributors may be used to endorse or promote products
      derived from this software without specific prior written
      permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR
CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
*/ 

#include &lt;getopt.h&gt;

#include &lt;netinet/in.h&gt;
#include &lt;sys/types.h&gt;
#include &lt;sys/socket.h&gt;
#include &lt;arpa/inet.h&gt;

#include &lt;sys/time.h&gt;
#include &lt;time.h&gt;
#include &lt;unistd.h&gt;

#include &lt;stdlib.h&gt;
#include &lt;stdio.h&gt;
#include &lt;stdbool.h&gt;
#include &lt;string.h&gt;

#include &lt;signal.h&gt;

typedef enum
{
    DESTINATION = 0x0001,
    DEF_PORT    = 1025,
    MIN_REPEAT  = 20,
    PACKET_SIZE = 32,
} CONSTS;

static bool keepRunning = true;

static void Usage(const char * const progName)
{
    /* Here are the valid commands. */
    printf("n");
    printf("%s accepts the following parameters: nn", progName);
    printf("t* --destination or -d [ip address]n");
    printf("t  --port        or -p [port number]          (default: 1025)n");
    printf("t  --repeat      or -r [repeat every x msec.] (default: 20)n");
    printf("n");
}

void sigintHandler(int signal)
{
    keepRunning = false;
}

int main(int argc, char **argv)
{
    int theOption, theOptionIndex;
    const char *short_options = "d:p:r:";
    static struct option long_options[] = 
    {
        { "destination", required_argument, NULL, 'd' },
        { "port",        required_argument, NULL, 'p' },
        { "repeat",      required_argument, NULL, 'r' },
        { 0, 0, 0, 0 }
    };

    int requiredParameters = DESTINATION;

    struct in_addr destAddr;
    memset(&destAddr, 0, sizeof(struct in_addr));

    uint16_t destPort = DEF_PORT;
    uint32_t repeatMs = MIN_REPEAT;

    while (-1 != (theOption = getopt_long(argc, argv, short_options, long_options, 
                                          &theOptionIndex)))
    {
        switch(theOption)
        {
            case 'd':
                inet_pton(AF_INET, optarg, &destAddr);
                requiredParameters &= ~DESTINATION;
                break;
            case 'p':
                destPort = (uint16_t) atoi(optarg);
                break;
            case 'r':
                {
                int tempMs = atoi(optarg);
                repeatMs = (tempMs &lt; MIN_REPEAT) ? MIN_REPEAT : tempMs;
                }
                break;
            case 'h': 
            case '?':
            default:
                Usage(argv[0]);
                return -1;
                break;
        }
    }

    /* If not all required parameters were entered, then we need to exit. */
    if (0 != requiredParameters)
    {
        printf("Not all * required parameters were entered.n");
        Usage(argv[0]);
        return -1;
    }

    /* Setup signal handler. */
    signal(SIGINT, sigintHandler);

    /* Print up the options in use: */
    printf("Destination address is %sn",       inet_ntoa(destAddr));
    printf("Destination port    is %dn",       destPort);
    printf("Packet interval     is %d ms.n",   repeatMs);

    /* Data packet to send. */
    uint8_t dataPacket[PACKET_SIZE];

    /* Initialize the random number generator. */
    srand(clock());

    /* Destination ok. */
    int destSocket = socket(PF_INET, SOCK_DGRAM, 0);
    if (destSocket &lt; 0)
    {
        printf("destSocket not opened.n");
        return -1;
    }

    struct sockaddr_in destSocketAddr;
    destSocketAddr.sin_family   = AF_INET;
    destSocketAddr.sin_addr     = destAddr;
    destSocketAddr.sin_port     = htons(destPort);

    /* This thing's only any good under 2.6 w/realtime or High Res Timers active. */
    /*
    struct timespec sleepSpec;
    sleepSpec.tv_sec  = 0;
    sleepSpec.tv_nsec = repeatMs * 1000 * 1000;
    */

    unsigned char randByte;
    struct timeval theStart, afterTx, nextTx, afterSleep;

    gettimeofday(&theStart, NULL);
    nextTx    = theStart;
    repeatMs *= 1000;

    for(;keepRunning;)
    {
        /* busyfrickinwaiting: linux, and its low res timers, are awful. */
        /* Busy-waiting, the only reliable way to sleep less than 1/HZ.  */
        for(;keepRunning;)
        {
            gettimeofday(&afterSleep, NULL);
            if (afterSleep.tv_sec  &gt;= nextTx.tv_sec &&
                afterSleep.tv_usec &gt;= nextTx.tv_usec)
            {
                if (0 &gt; sendto(destSocket, 
                               &dataPacket, 
                               sizeof(dataPacket), 
                               0, 
                               (struct sockaddr *) &destSocketAddr, 
                               sizeof(destSocketAddr)))
                {
                    perror("sendto");
                }
                break;
            }
        }

        /* Prepare next payload. */
        randByte = (unsigned char) (rand() % 255);
        memset(&dataPacket, randByte, sizeof(dataPacket));

        /* Setup next TX time. */
        nextTx.tv_usec += repeatMs; 
        nextTx.tv_sec  += nextTx.tv_usec / 1000000;
        nextTx.tv_usec %= 1000000;

        gettimeofday(&afterTx, NULL);

        printf("aftersleep: %d.%06d, aftersend: %d.%06d, nextTx: %d.%06dn",
               (int) afterSleep.tv_sec, 
               (int) afterSleep.tv_usec,
               (int) afterTx.tv_sec,
               (int) afterTx.tv_usec,
               (int) nextTx.tv_sec, 
               (int) nextTx.tv_usec);
    }

    /* Cleanup. */
    printf("Shutting %s down.n", argv[0]);
    close(destSocket);

    return 0;
}</pre>
  
  <p>
    &nbsp;
  </p>
</div>

 [1]: https://vilimpoc.org/research/ku-latency/ku-latency.c
 [2]: https://vilimpoc.org/research/ku-latency/send-data.c