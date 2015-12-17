---
title: 'How to Compile Android Kernel from Source : A Beginner’s Guide'
author: admin
layout: post
date: 2014-03-20
url: /how-to-compile-android-kernel-from-source-a-beginners-guide/
duoshuo_thread_id:
  - 6218977982262805250
categories:
  - 操作系统
  - 硬件
format: aside

---
ref:http://www.movzio.com/howto/compile-android-kernel-source-beginners-guide

<div>
  <div>
    <div>
      <a href="http://www.movzio.com/wp-content/uploads/2014/03/42e8aa42827d3b994516fe86973cd3bc2_Fotor.jpg"><img itemprop="image" title="How to Compile Android Kernel from Source : A Beginner’s Guide" alt="42e8aa42827d3b994516fe86973cd3bc2_Fotor" src="http://www.movzio.com/wp-content/uploads/2014/03/42e8aa42827d3b994516fe86973cd3bc2_Fotor-790x444.jpg" width="790" height="444" /></a>
    </div>
  </div>
</div>

<div>
  <div>
    <div>
    </div>
    
    <div>
      <p>
        &nbsp;
      </p>
      
      <div id="ssba">
        <center>
          Don&#8217;t be shellfish&#8230;<a id="ssba_facebook_share" href="http://www.facebook.com/sharer.php?u=http://www.movzio.com/howto/compile-android-kernel-source-beginners-guide/" target="_blank"><img title="Facebook" alt="Facebook" src="http://www.movzio.com/wp-content/plugins/simple-share-buttons-adder/buttons/ribbons/facebook.png" /></a>17<a id="ssba_google_share" href="https://plus.google.com/share?url=http://www.movzio.com/howto/compile-android-kernel-source-beginners-guide/" target="_blank"><img title="Google+" alt="Google+" src="http://www.movzio.com/wp-content/plugins/simple-share-buttons-adder/buttons/ribbons/google.png" /></a><a id="ssba_twitter_share" href="http://twitter.com/share?url=http://www.movzio.com/howto/compile-android-kernel-source-beginners-guide/&text=How+to+Compile+Android+Kernel+from+Source+%3A+A+Beginner%E2%80%99s+Guide+%40movzio" target="_blank"><img title="Twitter" alt="Twitter" src="http://www.movzio.com/wp-content/plugins/simple-share-buttons-adder/buttons/ribbons/twitter.png" /></a><a id="ssba_pinterest_share"></a><img title="Pinterest" alt="Pinterest" src="http://www.movzio.com/wp-content/plugins/simple-share-buttons-adder/buttons/ribbons/pinterest.png" /><a id="ssba_stumbleupon_share" href="http://www.stumbleupon.com/submit?url=http://www.movzio.com/howto/compile-android-kernel-source-beginners-guide/&title=How%20to%20Compile%20Android%20Kernel%20from%20Source%20:%20A%20Beginner%E2%80%99s%20Guide" target="_blank"><img title="StumbleUpon" alt="StumbleUpon" src="http://www.movzio.com/wp-content/plugins/simple-share-buttons-adder/buttons/ribbons/stumbleupon.png" /></a><a id="ssba_email_share" href="mailto:?Subject=How%20to%20Compile%20Android%20Kernel%20from%20Source%20:%20A%20Beginner%E2%80%99s%20Guide&Body=%20http://www.movzio.com/howto/compile-android-kernel-source-beginners-guide/"><img title="Email" alt="Email" src="http://www.movzio.com/wp-content/plugins/simple-share-buttons-adder/buttons/ribbons/email.png" /></a>
        </center>
      </div>
      
      <p>
        Hello everyone, want to compile an <b>Android</b> <b>kernel</b> on your own? Than why not begin doing it so by following the simple guide below?
      </p>
      
      <h2>
        <b>1) Setup Environment:</b>
      </h2>
      
      <p>
        First you will need these things,
      </p>
      
      <ul>
        <li>
          A Linux PC (32 bit will work for compilation of <i>kernel</i>)
        </li>
        <li>
          Basic knowledge of using terminal in Unix based operating system
        </li>
        <li>
          Few packages for compilation
        </li>
        <li>
          Tool chains for compilation
        </li>
        <li>
          <span style="text-decoration: underline;">Kernel</span> source code
        </li>
        <li>
          Patience :p
        </li>
      </ul>
      
      <p>
        So now we begin, First of all open terminal in your Linux PC. I am using here Linux Mint 16, a Debian based Linux Distribution. You can use any Linux distro for it such as Ubuntu, fedora, Arch Linux, etc. procedure will be same just you need to use different commands with terminal as per your distro. Now type this code in your terminal:
      </p>
      
      <div>
        <pre>sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl libc6-dev libncurses5-dev:i386 x11proto-core-dev libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 libgl1-mesa-dev g++-multilib mingw32 openjdk-6-jdk tofrodos python-markdown libxml2-utils xsltproc zlib1g-dev:i386 git</pre>
        
        <p>
          &nbsp;
        </p>
        
        <p>
          <img title="Android" alt="1" src="http://www.movzio.com/wp-content/uploads/2014/03/1-1024x640.png" width="1024" height="640" />
        </p>
      </div>
      
      <p>
        This will install required packages for kernel compilation. Now last thing, we need tool chains for<b>compiling</b> kernel. You can get it from here: <a href="https://github.com/crossfire77/Android_Toolchains" rel="nofollow">https://github.com/crossfire77/<i>Android</i>_Toolchains</a>Download it and extract it somewhere. Then, We have to setup path of our tool chains, so type this in terminal:
      </p>
      
      <div>
        <pre>gedit .bashrc</pre>
      </div>
      
      <p>
        It will open one document, then put this codes at the end of it.
      </p>
      
      <div>
        <pre>export PATH=${PATH}:path/to/toolchain/folder/arm-eabi-4.4.3/bin</pre>
      </div>
      
      <p>
        <img title="Android" alt="2" src="http://www.movzio.com/wp-content/uploads/2014/03/2-1024x640.png" width="1024" height="640" />
      </p>
      
      <p>
        Now we are done with downloading and setting up things. Let’s move to next step!
      </p>
      
      <h2>
        2) Download Source Code:
      </h2>
      
      <p>
        Kernel source codes are under GNU GPL open source license so vendors (ex. Sony, HTC, Samsung, LG) have to release it. You can find your appropriate kernel source code from mentioned websites:
      </p>
      
      <p>
        For Sony: <a href="http://developer.sonymobile.com/" rel="nofollow">http://developer.sonymobile.com/</a>
      </p>
      
      <p>
        For Samsung: <a href="http://opensource.samsung.com/" rel="nofollow">http://opensource.samsung.com/</a>
      </p>
      
      <p>
        For HTC: <a href="http://www.htcdev.com/" rel="nofollow">http://www.htcdev.com/</a>
      </p>
      
      <p>
        For LG: <a href="http://www.lg.com/global/support/opensource/index" rel="nofollow">http://www.lg.com/global/support/opensource/index</a>
      </p>
      
      <p>
        Just download it from mentioned websites as per your device and extract it somewhere in your computer.
      </p>
      
      <h2>
        3) Getting Config file:
      </h2>
      
      <p>
        Now this is where you should put your focus. For building a kernel you need config file. There is two ways for it:
      </p>
      
      <ul>
        <li>
          You can either get it from your phone with help of ADB (<span style="text-decoration: underline;">Android</span> Debug Bridge) or
        </li>
        <li>
          You can get it from your kernel source code.
        </li>
      </ul>
      
      <p>
        I will show you both the ways of doing it so.
      </p>
      
      <p>
        <strong>1) <i>Getting config file from your phone with the help of ADB:</i><i> </i></strong>
      </p>
      
      <ul>
        <li>
          First of all connect your phone to your computer.
        </li>
        <li>
          Then type the mentioned code below:
        </li>
      </ul>
      
      <div>
        <pre>adb pull proc/config.gz ~/home/crossfire77/kernel</pre>
      </div>
      
      <p>
        This will pull your existing config file from your phone and put it in kernel folder. Now extract it,
      </p>
      
      <div>
        <pre>zcat config.gz &gt; .config</pre>
      </div>
      
      <p>
        So we have directly config for building our kernel.
      </p>
      
      <p>
        <strong>NOTE: </strong> Many times users’ faces errors while connecting phone with computer via ADB, it’s mostly issue of a permission. There is two solutions for it.
      </p>
      
      <p>
        <strong>1.) Using ADB as root user: </strong>$sudo -s $ adb kill-server $ adb start-server $ adb devices And you will see your device now in terminal, it is a temporary solution meaning you have to do every time you connect your phone.
      </p>
      
      <p>
        <strong>2.) Solve permission problem permanently:</strong>
      </p>
      
      <p>
        Open terminal and type this: $ sudo gedit /etc/udev/rules.d/51-android.rules and copy content from this file, http://goo.gl/bldQS9 In this file, please replace “crossfire77” with your username.
      </p>
      
      <p>
        Now last thing to do is, giving executing permission to file, and we are good to go.
      </p>
      
      <div>
        <pre>$ sudo chmod a+r /etc/udev/rules.d/51-android.rules $ sudo service udev restart</pre>
        
        <p>
          This will solve your problem with ADB and FASTBOOT while connecting through them your phone with computer.
        </p>
        
        <p>
          <strong>2) <i>Getting config file from kernel source code:</i></strong>
        </p>
        
        <p>
          This part is little tricky. For this you have to have little knowledge about your device chipset number. In kernel source code there are lots of config files so from your chipset number you can find your config file. As example, My device is HTC Wildfire S and it has MSM7227 chipset so I can find its config in mentioned path: <i>arch/arm/configs/msm7227_defconfig</i><img title="Android" alt="3" src="http://www.movzio.com/wp-content/uploads/2014/03/3-1024x640.png" width="1024" height="640" />
        </p>
        
        <p>
          So now just type this code in terminal:
        </p>
      </div>
      
      <div>
        <pre>make ARCH=arm CROSS_COMPILE=arm-eabi- msm7227_defconfig</pre>
      </div>
      
      <p>
        <img title="Android" alt="4" src="http://www.movzio.com/wp-content/uploads/2014/03/4-1024x640.png" width="1024" height="640" />
      </p>
      
      <p>
        It will create .config file from your existing chipset config and then we are good to go. As I told you before you need to have little knowledge about your device chipset then you can able to tell what is your correct config file, so be careful while doing this step. Everything is done now so shall we start building?
      </p>
      
      <p>
        <b>4) Building:</b>
      </p>
      
      <p>
        Type this in your terminal,
      </p>
      
      <div>
        <pre>make ARCH=arm CROSS_COMPILE=arm-eabi- -jX</pre>
      </div>
      
      <p>
        <img title="Android" alt="5" src="http://www.movzio.com/wp-content/uploads/2014/03/5-1024x640.png" width="1024" height="640" />It is main command for compilation and here X can be replaced by maximum numbers of jobs your computer can handle simultaneously. For ease just enter the twice number of your cores. Ex. If your computer has two cores enter four.
      </p>
      
      <p>
        <strong>NOTE: P<em></em><em>lease do not enter high number or your computer will explode due to overheating.</em></strong>
      </p>
      
      <p>
        It will take around ~15-1 hour as per your computer hardware specs.so keep sit down and keep patience. After completing this procedure we will have our zImage (kernel)! <img title="Android" alt="afafa" src="http://www.movzio.com/wp-content/uploads/2014/03/afafa-1024x640.png" width="1024" height="640" />Let’s create one working directory:
      </p>
      
      <div>
        <pre>mkdir kernell</pre>
      </div>
      
      <p>
        Now, we will copy our zImage to our working directory:
      </p>
      
      <div>
        <pre>cp arch/arm/boot/zImage kernell</pre>
      </div>
      
      <p>
        Next step, modules (modules builds with kernel and we need it for Wi-Fi and etc. as per your device requirement)
      </p>
      
      <div>
        <pre>find . -name '*ko' -exec cp '{}' kernell ;</pre>
      </div>
      
      <p>
        <img title="Android" alt="7" src="http://www.movzio.com/wp-content/uploads/2014/03/7-1024x640.png" width="1024" height="640" />So we are done with the main part, now last step to make flash able zip out of this to flash our kernel.
      </p>
      
      <p>
        <b>5) Making Flashable Zip:</b> We are done with <i>compiling</i> and building task and at the end we have our zImage (kernel) and modules. <img title="Android" alt="Screenshot from 2014-03-05 14:22:03" src="http://www.movzio.com/wp-content/uploads/2014/03/Screenshot-from-2014-03-05-142203-1024x640.png" width="1024" height="640" />Now time to flash it to your phone, for it we have one very easy method, “any kernel updater” by koush. So download this file from here: <a href="http://goo.gl/mQpHhC" rel="nofollow">http://goo.gl/mQpHhC</a> <img title="Android" alt="ffafa" src="http://www.movzio.com/wp-content/uploads/2014/03/ffafa-1024x640.png" width="1024" height="640" />
      </p>
      
      <p>
        So, this was all about <span style="text-decoration: underline;">compiling</span> an Android Kernel. Share me your any doubts or acknowledgements if you have.
      </p>
      
      <p>
        Have fun compiling Android Kernel.
      </p>
    </div>
  </div>
</div>