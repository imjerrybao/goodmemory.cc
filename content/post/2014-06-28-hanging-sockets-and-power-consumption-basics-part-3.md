---
title: Hanging Sockets and Power Consumption – Basics, Part 3
author: admin
layout: post
date: 2014-06-28
url: /hanging-sockets-and-power-consumption-basics-part-3/
categories:
  - 操作系统
  - 硬件

---
很好的文章，就mobile 空socket 的耗电状态做了深入的分析.

更完整的内容参见：<a href="http://www.goodmemory.cc/?attachment_id=" rel="attachment wp-att-829">trepn-whitepaper-apps-power</a>

from：<https://developer.qualcomm.com/blog/hanging-sockets-and-power-consumption-basics-part-3>

<p style="color: #424242;">
  Continuing our series on mobile apps and their effect on battery drain, I’ll pick up where the three guidelines in <a style="color: #1c9daf;" href="https://developer.qualcomm.com/blog/mobile-apps-and-power-consumption-basics-part-2">Wayne Lee’s last post</a> left off, especially #3: “Know what your app is doing with the hardware and when it’s doing it.”
</p>

<p style="color: #424242;">
  One common way that mobile apps use too much power is through hanging sockets –network connections that the app is no longer using, but which the server thinks are still alive because the app has not closed them. The subsequent query from the server results in needless battery drain.
</p>

<p style="color: #424242;">
  Here’s more background on the problem and how you can deal with it.
</p>

<strong style="color: #424242;">“Wake up. It’s time to go to sleep.”</strong>

<p style="color: #424242;">
  Applications often “forget” to close their socket after they are done with it. Then, after some amount of time without data activity, the server times the socket out and closes it.
</p>

<p style="color: #424242;">
  Socket termination in TCP requires a four-way handshake, so the server has to send a FIN packet to the device, which usually takes the device from the low-power dormant state to the higher-power active state. The device goes idle for a bit, then back to dormant. It’s like waking somebody up to tell them that it’s time to go to sleep.
</p>

<p style="color: #424242;">
  Look at the example in the diagram. The red (1) shows the device jumping from dormant to active mode to send and receive data normally for a few seconds. Once finished, the cellular radio drops to a power-saving idle mode (2) in case that it’s needed again. After about 15 seconds of inactivity, the radio goes dormant (3).
</p>

<p style="color: #424242;">
      <img src="https://developer.qualcomm.com/sites/default/files/attachments/sockets.png" alt="The diagram shows inefficiencies in Socket Termination activity on a device, the multiple steps it goes through to send/receive data and why it’s important to close sockets." width="550" height="246" />
</p>

<p style="color: #424242;">
  But the app has left the socket open (hanging). The server doesn’t like loose ends, so it sends its FIN packet to the device. This rouses the radio from dormant to active again (4), the same as if it were sending/receiving data for the app. Worse yet, the radio follows the normal curve back down to idle for another 15 seconds, wasting more power (5).
</p>

<p style="color: #424242;">
  Begin to get the idea?
</p>

<p style="color: #424242;">
  The phone has to bring up the radio for a simple, easily avoidable handshake because the server has asked the device for something that the app should have provided in the first place. If no other traffic moves between the device and the network, the connection is a complete waste of several hundred milliamperes.
</p>

<p style="color: #424242;">
  Assuming that the app uses the network four times in an hour, the simple fix of having the app close the socket when finished can reduce network power consumption by about 20 percent, which would be the difference between eight and ten hours of standby power.
</p>

<p style="color: #424242;">
  The lesson is: Program your app to close sockets when it has finished with them. Otherwise, the phone consumes power to bring up the radio for a needless handshake with the server.
</p>

<strong style="color: #424242;">Next Steps</strong>

<p style="color: #424242;">
  So, to paraphrase Wayne, you need to know what your app is doing with the cellular radio, when it’s doing it and how to turn it off when the app no longer needs it.
</p>

<ul style="color: #424242;">
  <li>
    Watch Wayne’s Uplinq presentation, “<a style="color: #1c9daf;" href="https://www.uplinq.com/schedule/minimum-power-usage-maximum-performance-introducing-new-tool-eclipse" target="_blank">Minimum Power Usage, Maximum Performance</a>.”
  </li>
  <li>
    Read our white paper, &#8220;<a style="color: #1c9daf;" href="https://developer.qualcomm.com/download/trepn-whitepaper-power.pdf">When Mobile Apps Use Too Much Power: A Developer Guide for Android App Performance</a>,” for more background and ideas on mobile apps and power consumption.
  </li>
</ul>

<p style="color: #424242;">
  Questions? Visit the <a style="color: #1c9daf;" href="https://developer.qualcomm.com/forums/qdevnet-forums/trepn-profiler">Trepn Profiler Support Forum</a> or let me know in the comments below.
</p>