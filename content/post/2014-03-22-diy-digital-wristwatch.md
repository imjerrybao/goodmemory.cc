---
title: DIY Digital Wristwatch
author: admin
layout: post
date: 2014-03-22
url: /diy-digital-wristwatch/
duoshuo_thread_id:
  - 6218977982787093250
categories:
  - 硬件

---
ref：http://blog.zakkemble.co.uk/diy-digital-wristwatch/

&nbsp;

**Getting kits available for the wristwatch is currently in the works, I will start accepting orders towards the end of March. If you would like to be notified of any updates please send an email to wristwatchkit@zakkemble.co.uk (blank email or something, doesn’t really matter).**

# Introduction

The main incentive behind this project was to see how much I could cram, in terms of both hardware and software, into a wristwatch-like device that is no larger than the display itself. An OLED display was chosen for being only 1.5mm thick and not requiring a backlight (each pixel produces its own light), but mostly because they look cool. The watch was originally going to have a 0.96″ display, but this proved too difficult to get all the things I wanted underneath it. Going up a size to 1.3″ was perfect.

<div>
  <div>
    <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2272.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2272-300x225.jpg" width="300" height="225" /></a>
  </div>
  
  <div>
    <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2284.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2284-300x225.jpg" width="300" height="225" /></a>
  </div>
</div>

视频：



# Hardware

&nbsp;

[<img alt="Wristwatch schematic" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/watch_schematic-300x201.png" width="300" height="201" />][1]

Wristwatch schematic
  
On the hardware side the watch contains an Atmel ATmega328P microcontroller, 2.5V regulator, Maxim DS3231M RTC, 1.3″ 128×64 monochrome OLED, 2 LEDs (red and green), a buzzer sounder, 3 way switch for navigation, powered by a 150mAh LiPo battery which can be charged via USB and 2 PCBs (though one PCB is just used as a raiser for the OLED).

&nbsp;

The [ATmega328P][2] uses its internal 8MHz oscillator and runs on 2.5V from a linear regulator. Its current draw is around 1.5mA when active and 100nA in sleep mode.

The [DS3231M][3] RTC is an excellent chip, housed in a small 8 pin package which includes a built-in temperature compensated MEMS resonator with an accuracy of ±5ppm (± 2 minutes 40 seconds per year). Only a decoupling capacitor and a few extra pull-up resistors were required. The RTC is wired up so that instead of having power applied to the VCC pin, it’s applied to the Vbat pin which reduces its current draw from around 100uA down to 2.5uA.
  
Unfortunately this chip seems to be very hard to get hold of at a reasonable price if you’re not in the US. I had to get mine as samples.

The battery charging circuit uses a [Microchip MCP73832][4] along with some additional components for [load sharing][5], where the battery can charge without the rest of the watch interfering with it.

You might have noticed in the schematic that the LEDs are directly connected to the microcontroller without any resistors. The internal MOSFETs of the microcontroller have an on resistance of around 40Ω, so with a 2.5V supply voltage and LEDs with 2V<sub>f</sub>, around 20mA ends up through the LEDs. I would have liked to have a blue LED, but the voltage drop for those are usually more than 3V which would have required some additional resistors and a MOSFET.

As the microcontroller is running on 2.5V the battery voltage needs to be brought down a bit to obtain an ADC reading. This is done by a simple voltage divider. However, with the voltage divider connected across the battery there would be a current of around 350uA constantly flowing through it, this is a huge waste of power. A P-MOSFET (and some voltage level conversion for it, which I forgot about in the first version so it was always stuck on) was added so the divider can be turned on only when needed.

The 2.5V regulator being used is a [Torex XC6206][6], primarily chosen for its tiny quiescent current of just 1uA.
  
Why a linear regulator and not a switching regulator? The switching regulators I looked at had an efficiency of at least 80% with a 2mA load, but that efficiency quickly dropped off to less than 50% with loads of 100uA. Since the devices connected to the regulator draw 2-3uA in sleep mode, a switching regulator would have performed incredibly poor compared to a linear regulator. The 2.5V linear regulator efficiency is 60% with 4.2V input going up to 83% with 3V input.

<div>
  <div>
    <p>
      <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2137.jpg"><img alt="Underside" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2137-300x225.jpg" width="300" height="225" /></a>
    </p>
    
    <p>
      Underside
    </p>
  </div>
  
  <div>
    <p>
      <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT1970.jpg"><img alt="Top side, under display" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT1970-300x225.jpg" width="300" height="225" /></a>
    </p>
    
    <p>
      Top side, under display
    </p>
  </div>
</div>

# Software

So we’ve got a nice OLED display and 32KB of program space at our disposal, surely we can have more than just the time and date?

#### Almost everything is animated

A lot of time was spent optimizing the rendering code which, in short, involves copying bitmap images from flash to the frame buffer in RAM and sending the frame buffer over SPI to the OLED. The end result was being able to maintain 100+ FPS in almost all areas of the watch with an 8MHz AVR. However, since the animations are frame based instead of time based and to save power, the frame rate is limited to 60FPS.

Some of the main animated things:

  * CRT animation when entering and exiting sleep mode (similar to Android CRT animation).
  * Main time numbers have a ticker effect.
  * Menus have a scroll left/right animation and selecting an option will cause the current menu to fall off the screen and the next thing to fall on.

#### Alarms

  * Set up to 10 alarm times.
  
    Number of alarm times is only limited by the amount of available EEPROM and RAM.
  * Each alarm has the hour, minute and which days of the week it should be active on.

[<img alt="Alarms menu" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2252-300x225.jpg" width="300" height="225" />][7]

Alarms menu

#### Games

<div>
  <div>
    <p>
      <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2151.jpg"><img alt="Breakout" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2151-300x225.jpg" width="300" height="225" /></a>
    </p>
    
    <p>
      Breakout
    </p>
  </div>
  
  <div>
    <p>
      <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2153.jpg"><img alt="Car dodge" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2153-300x225.jpg" width="300" height="225" /></a>
    </p>
    
    <p>
      Car dodge
    </p>
  </div>
</div>

#### Apps

<div>
  <div>
    <p>
      <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2238.jpg"><img alt="Flashlight" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2238-300x225.jpg" width="300" height="225" /></a>
    </p>
    
    <p>
      Flashlight<br /> Turns on all OLED pixels and LEDs, also has <span style="text-decoration: line-through;">seizure</span>strobe mode
    </p>
  </div>
  
  <div>
    <p>
      <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2254.jpg"><img alt="Stopwatch" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2254-300x225.jpg" width="300" height="225" /></a>
    </p>
    
    <p>
      Stopwatch
    </p>
  </div>
</div>

#### Plenty of options

  * 3 Channel volume control 
      * UI
      * Alarms
      * Hour beeps
  * Sleep timeout
  * Display brightness
  * Animations
  
    You’re not going to turn them off, right?

[<img alt="Volume settings" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2156-300x225.jpg" width="300" height="225" />][8]

Volume settings

#### Power saving

In ‘active’ mode the microcontroller tries to go into idle sleep as much a possible. In idle sleep the controller is woken each millisecond to see if anything needs to be updated, if not then it goes back to idle sleep, this usually takes less than 100us if the display doesn’t need to be updated. In this mode the current draw can be anywhere between 0.8mA and 2mA, depending on how long it takes to draw frames (fast frame draw time = more time in idle sleep).

In ‘sleep’ mode the microcontroller turns the OLED off and goes into power-down sleep mode where it is only woken by either a button press, an RTC alarm or USB being plugged in. In this state the microcontroller draws ~100nA.

# Power consumption

In sleep mode the overall current draw of the watch is around 6uA. In active mode the current draw can vary from 2mA to over 70mA, though 10mA is the typical current draw.

&nbsp;

<center>
  <br /> Battery capacity: 150mAh 
</center>

<table>
  <tr>
    <th>
      Minimum<br /> (sleep mode)
    </th>
    
    <th>
      Typical<br /> (main time display)
    </th>
    
    <th>
      High<br /> (flashlight)
    </th>
  </tr>
  
  <tr>
    <td>
      6uA<br /> 2.85 years
    </td>
    
    <td>
      10mA<br /> 15 hours
    </td>
    
    <td>
      64mA<br /> 2 hours, 20 minutes
    </td>
  </tr>
</table>

&nbsp;

&nbsp;

If the watch is in active mode for an average of 1 minute per day (with a 5 second sleep timeout that would be checking the time 12 times a day) and all volume channels set to minimum the watch should last for around <del datetime="2013-11-03T16:37:25+00:00">30 days</del> 1 year and 4 months on a single charge. (Oops, 30 days is if the watch is on for 1 minute per hour, not day).

&nbsp;

<center>
  <br /> Current draw breakdown (typical) 
</center>

<table>
  <tr>
    <th>
      Part
    </th>
    
    <th>
      Current
    </th>
  </tr>
  
  <tr>
    <td>
      ATmega328P (sleep / active)
    </td>
    
    <td>
      100nA / 1.5mA
    </td>
  </tr>
  
  <tr>
    <td>
      OLED (sleep / active)
    </td>
    
    <td>
      500nA / 8.5mA
    </td>
  </tr>
  
  <tr>
    <td>
      DS3231M RTC
    </td>
    
    <td>
      2.5uA
    </td>
  </tr>
  
  <tr>
    <td>
      Schottky diode (D1) (reverse leakage)
    </td>
    
    <td>
      1uA
    </td>
  </tr>
  
  <tr>
    <td>
      Regulator (quiescent current)
    </td>
    
    <td>
      1uA
    </td>
  </tr>
  
  <tr>
    <td>
      Other (MOSFET and capacitor leakage etc)
    </td>
    
    <td>
      1uA
    </td>
  </tr>
  
  <tr>
    <td>
      <strong>Total (sleep / active)</strong>
    </td>
    
    <td>
      <strong>6.1uA / 10mA</strong>
    </td>
  </tr>
</table>

&nbsp;

&nbsp;

# v1 to v1.1 changes

The first version had a few problems:

  * Added level conversion for the ADC P-MOSFET.
  
    Without level conversion the P-MOSFET was always stuck on. To turn of the P-MOSFET off the gate voltage needs to be at around the same level as its source voltage (which is connected to the battery), but the microcontroller was only providing 2.5V.
  * Added a gate pull-down resistor for the MOSFET driving the sounder.
  
    The MOSFET gate was floating when the microcontroller was being programmed which was causing the MOSFET to turn on and allow non-pulsed current to flow through the sounder, which probably wasn’t good for it.
  * Larger solder pads for MicroUSB connector.
  
    Normally SMD MicroUSB connectors have solder tabs at the sides and should have extra solder pads underneath, but since this is soldered by hand the underneath is unreachable. With out the extra solder pads the USB connector was wobbly so some of the connector pins eventually broke their solder joints. To fix this issue I enlarged the side solder pads so that the connector can be soldered all along its side instead of just the tab. No more wobbly connectors.

[<img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/usbpads-300x112.jpg" width="300" height="112" />][9]

# Other problems

Out of 3 OLED displays, 2 died after a few minutes of being attached to the watch. One from Ebay and the other from AliExpress. I’m still not sure why they died, maybe just China quality? The one that worked was also from Ebay.

# Future improvements

  * Programming via USB.
  
    At the moment 4 wires need to be poked into the board (SPI programming) and then hope they don’t fall out while programming.
  * Add a fuel gauge IC.
  
    At the moment the battery level is determined by its voltage, this isn’t a very accurate method of getting the remaining battery charge.
  * Different microcontroller.
  
    The current firmware is using ~28KB out of the 32KB of available program space in the ATmega328P, a different microcontroller with more program space and probably more RAM would be needed to add more things like a calculator (floating point stuff eats up a lot of program space). However, the ATmega328P has the most program space for an AVR in a 32 pin TQFP package, to have more program space I would have to use a 44 pin AVR. The ATmega1284 looks interesting.
  * Switching regulator, charge pump regulator or maybe a hybrid solution?
  
    The linear regulator in use at the moment isn’t particularly efficient and switching regulators don’t seem to be very good with low current draw. Perhaps a charge pump regulator or a hybrid solution to swap between a linear regulator for sleep mode and a switching regulator for active mode?
  * A case of some sort?

# Parts list

&nbsp;

<center>
  &nbsp;</p> 
  
  <table>
    <tr>
      <th>
        Schematic
      </th>
      
      <th>
        Part/value
      </th>
      
      <th>
        Description
      </th>
      
      <th>
        Quantity
      </th>
    </tr>
    
    <tr>
      <td>
        U1
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=1715486">Atmel ATmega328P</a>
      </td>
      
      <td>
        Microcontroller
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        U3
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=1332159">MCP73832</a>
      </td>
      
      <td>
        Lithium battery charger IC
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        U4
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=8796947">XC6206P252MR</a>
      </td>
      
      <td>
        2.5V LDO Regulator
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        U2
      </td>
      
      <td>
        DS3231MZ+
      </td>
      
      <td>
        RTC
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        Q1, Q2
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=2061526">DMP1045U</a>
      </td>
      
      <td>
        P-MOSFET
      </td>
      
      <td>
        2
      </td>
    </tr>
    
    <tr>
      <td>
        Q3, Q4
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=1843757">DMG6968U</a>
      </td>
      
      <td>
        N-MOSFET
      </td>
      
      <td>
        2
      </td>
    </tr>
    
    <tr>
      <td>
        D1
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=1843764">ZLLS410</a>
      </td>
      
      <td>
        Schottky diode
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        D2
      </td>
      
      <td>
        <a href="http://www.rapidonline.com/Electronic-Components/High-Speed-Switching-Diode-400mW-0805-47-1004">TS4148</a>
      </td>
      
      <td>
        High speed diode
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        C5
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=1759293">4.7nF</a>
      </td>
      
      <td>
        Capacitor
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        C4, C6, C7
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=1759166">100nF</a>
      </td>
      
      <td>
        Capacitor
      </td>
      
      <td>
        3
      </td>
    </tr>
    
    <tr>
      <td>
        C3, C8, C9, C10
      </td>
      
      <td>
        <a href="http://www.rapidonline.com/Electronic-Components/1uf-16v-X7r-0805-Ceram-Chip-Capacitor-71-0508">1uF</a>
      </td>
      
      <td>
        Capacitor
      </td>
      
      <td>
        4
      </td>
    </tr>
    
    <tr>
      <td>
        C12
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=2210981">2.2uF</a>
      </td>
      
      <td>
        Capacitor
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        C1, C2, C11
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=2210982">4.7uF</a>
      </td>
      
      <td>
        Capacitor
      </td>
      
      <td>
        3
      </td>
    </tr>
    
    <tr>
      <td>
        R4, R8, R10
      </td>
      
      <td>
        100R
      </td>
      
      <td>
        Resistor
      </td>
      
      <td>
        3
      </td>
    </tr>
    
    <tr>
      <td>
        R6
      </td>
      
      <td>
        2.7K
      </td>
      
      <td>
        Resistor
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        R5
      </td>
      
      <td>
        7.5K
      </td>
      
      <td>
        Resistor
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        R7
      </td>
      
      <td>
        10K
      </td>
      
      <td>
        Resistor
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        R1
      </td>
      
      <td>
        22K
      </td>
      
      <td>
        Resistor
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        R2, R3, R11
      </td>
      
      <td>
        47K
      </td>
      
      <td>
        Resistor
      </td>
      
      <td>
        3
      </td>
    </tr>
    
    <tr>
      <td>
        R9
      </td>
      
      <td>
        390K
      </td>
      
      <td>
        Resistor
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        RN1
      </td>
      
      <td>
        <a href="http://www.rapidonline.com/Electronic-Components/10k-Yc16-1206-5-Chip-Resistor-Network-63-1924">10K network</a>
      </td>
      
      <td>
        Resistor network (4x resistors)
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        LED1
      </td>
      
      <td>
        <a href="http://www.rapidonline.com/Electronic-Components/Kingbright-KPHCM-2012CGCK-0805-Green-SMD-LED-72-8406">LED (green)</a>
      </td>
      
      <td>
        LED
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        LED2
      </td>
      
      <td>
        <a href="http://www.rapidonline.com/Electronic-Components/Kingbright-KPHCM-2012SURCK-0805-Red-SMD-LED-72-8402">LED (red)</a>
      </td>
      
      <td>
        LED
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        LS1
      </td>
      
      <td>
        <a href="http://www.rapidonline.com/Audio-Visual/Abmt-801-rc-Audio-Transducer-Surface-Mount-5x5mm-35-0287">Sounder</a>
      </td>
      
      <td>
        Magnetic sounder
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        SW1
      </td>
      
      <td>
        <a href="http://uk.farnell.com/jsp/search/productdetail.jsp?SKU=1316992">3 Way navigation switch</a>
      </td>
      
      <td>
        &#8211;
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        &#8211;
      </td>
      
      <td>
        MicroUSB connector (<a href="http://www.ebay.co.uk/itm/170909660431">Ebay</a>)
      </td>
      
      <td>
        &#8211;
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        OLED1
      </td>
      
      <td>
        OLED (<a href="http://www.ebay.co.uk/itm/160879860469">Ebay</a> / <a href="http://www.aliexpress.com/item/Free-shippping-1-3-inch-OLED-with-128x64-resolution-white-text/962778142.html">AliExpress</a>)
      </td>
      
      <td>
        &#8211;
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        &#8211;
      </td>
      
      <td>
        Battery (<a href="http://www.ebay.co.uk/itm/171050461126">Ebay</a>)
      </td>
      
      <td>
        &#8211;
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        &#8211;
      </td>
      
      <td>
        Main PCB
      </td>
      
      <td>
        &#8211;
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        &#8211;
      </td>
      
      <td>
        Display raiser PCB
      </td>
      
      <td>
        &#8211;
      </td>
      
      <td>
        1
      </td>
    </tr>
    
    <tr>
      <td>
        &#8211;
      </td>
      
      <td>
        Watch strap
      </td>
      
      <td>
        G10 NATO 22mm
      </td>
      
      <td>
        1
      </td>
    </tr>
  </table>
  
  <p>
    &nbsp;
  </p>
  
  <p>
    </center>&nbsp;
  </p>
  
  <h1>
    Downloads
  </h1>
  
  <table>
    <tr>
      <td>
        <strong>LATEST</strong><br /> <a href="http://blog.zakkemble.co.uk/download/watch_20130925.zip"><img title="Download" alt="Download" src="http://blog.zakkemble.co.uk/wp-includes/images/crystal/archive.png" /></a>
      </td>
      
      <td>
        <strong><a href="http://blog.zakkemble.co.uk/download/watch_20130925.zip">watch_20130925.zip</a> (279.08 kB) </strong><br /> Source code, EAGLE schematic and board layout files<br /> Downloaded 2145 times<br /> MD5: FD24C3229E856742CA388FA2DBEF3842
      </td>
    </tr>
  </table>
  
  <p>
    Water proof down to 0m!
  </p>
  
  <div id="gallery-1">
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/watch_schematic.png"><img alt="Wristwatch schematic" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/watch_schematic-150x150.png" width="150" height="150" /></a>
      </dt>
      
      <dd>
        Wristwatch schematic
      </dd>
    </dl>
    
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2266.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2266-150x150.jpg" width="150" height="150" /></a>
      </dt>
    </dl>
    
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/watchinterfacelabels.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/watchinterfacelabels-150x150.jpg" width="150" height="150" /></a>
      </dt>
    </dl>
    
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2125.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2125-150x150.jpg" width="150" height="150" /></a>
      </dt>
    </dl>
    
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT1937.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT1937-150x150.jpg" width="150" height="150" /></a>
      </dt>
    </dl>
    
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2175.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2175-150x150.jpg" width="150" height="150" /></a>
      </dt>
    </dl>
    
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2193.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2193-150x150.jpg" width="150" height="150" /></a>
      </dt>
    </dl>
    
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2327.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2327-150x150.jpg" width="150" height="150" /></a>
      </dt>
    </dl>
    
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2329.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2329-150x150.jpg" width="150" height="150" /></a>
      </dt>
    </dl>
    
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2207.jpg"><img alt="DIGITAL CAMERA" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2207-150x150.jpg" width="150" height="150" /></a>
      </dt>
    </dl>
    
    <dl>
      <dt>
        <a href="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2184.jpg"><img alt="Just over 10mm" src="http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2184-150x150.jpg" width="150" height="150" /></a>
      </dt>
      
      <dd>
        Just over 10mm
      </dd>
    </dl>
  </div>

 [1]: http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/watch_schematic.png
 [2]: http://www.atmel.com/devices/atmega328p.aspx
 [3]: http://www.maximintegrated.com/datasheet/index.mvp/id/6861
 [4]: http://www.microchip.com/wwwproducts/Devices.aspx?dDocName=en024903
 [5]: http://blog.zakkemble.co.uk/a-lithium-battery-charger-with-load-sharing/ "A Lithium Battery Charger with Load Sharing"
 [6]: http://www.torex-europe.com/products/range/120
 [7]: http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2252.jpg
 [8]: http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/PICT2156.jpg
 [9]: http://blog.zakkemble.co.uk/wp-content/uploads/2013/09/usbpads.jpg