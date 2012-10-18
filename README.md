Code for communicating wirelessly with [Current Cost home energy monitors](http://www.currentcost.com/products.html)
and [EDF EcoManager](http://www.edfenergy.com/products-services/for-your-home/ecomanager/) monitors.  The main planned aim of this code is the
robust gathering of data from an arbitrary number of EDF EcoManager
[Wireless Transmitter Plugs](https://shop.edfenergy.com/Item.aspx?id=540&CategoryID=1) for tracking the state of the majority of appliances
in a building.

Current status
==============

At present the code is in a very early stage.  The code as-is
will capture and display all Current Cost or EDF EcoManager RF packets it
receives.


Hardware requirements
=====================

 - The easiest way to get started is to buy a [Nanode Classic](http://www.nanode.eu/products/)
   and a 433MHz [RFM12b](http://www.hoperf.com/rf_fsk/fsk/21.htm) wireless transceiver.  Note that the Nanode RF kit
   comes with an 868 MHz RFM12b, which is not what you want.

 - If you build a DIY board, or if you connect an RFM12b to an Arduino,
   make sure the RFM12b's nFFS pin is set permanently high.


Usage
=====

 - Load this program onto your ATmega. The easiest way to do this is to use
   the pre-compiled hex file (see "[Uploading pre-compiled hex file](#uploading-pre-compiled-hex-file)" below).  

 - Then watch the serial port.  On Linux this can be achieved with
   the command: `screen /dev/ttyUSB0 115200`

 - You should see each RF packet displayed on your screen (each byte
   displayed as hex).


Acknowledgements & further reading
==================================

 - A massive thank you to Graham Murphy, Matt Thorpe and Paul Cooper who helped to decode the Current Cost and EDF RF protocols.

 - Many thanks to the good folks who wrote [JeeLib](https://github.com/jcw/jeelib) as it provided lots
   of help.
   
 - As did [this tutorial on SPI on AVR devices](https://sites.google.com/site/qeewiki/books/avr-guide/spi).

 - If you want an indepth insight into the RFM01 then read the [RFM12B.pdf](http://www.hoperf.com/upload/rf/RFM12B.pdf)
   manual BEFORE or INSTEAD OF [RFM12B_code.pdf](http://www.hoperf.com/upload/rf/RF12B_code.pdf) as the latter has far less detail.
   The only advantage of the RFM12B_code.pdf is that it contains a
   code example in C.

 - For more details please see [the CurrentCost category on my blog](http://jack-kelly.com/taxonomy/term/121).


Uploading pre-compiled hex file
===============================

First change directory into the `Release/` directory.

Uploading to AVR using FTDI serial cable:

```bash
avrdude -pm328p -carduino -P/dev/ttyUSB0 -b57600 -F -V 
            -Uflash:w:rfm_edf_ecomanager.hex:a
```

Uploading to AVR using STK500v2 programmer:

```bash
avrdude -pm328p -cstk500v2 -P/dev/ttyACM0 -Uflash:w:rfm_edf_ecomanager.hex:a
```

Building from source
====================

Using the Arduino IDE
---------------------

With the Arduino IDE closed, place the rfm_edf_ecomanager directory and files into your sketchbook directory.
Then start the Arduino IDE and opening this code should be as simple as going to 
Open -> rfm_edf_ecomanager.   Please note that I'm currently using Eclipse 
to develop this code (not the Arduino IDE).  However, I do try to test in the
Arduino IDE regularly.  Many thanks to [robomotic](https://github.com/robomotic) for
help converting my code to complile in the Arduino IDE.

Using Eclipse
-------------

 - Setup Eclipse for Arduino development [as described by Francesco Rigoni](http://horrorcoding.altervista.org/arduino-development-with-eclipse-a-step-by-step-tutorial-to-the-basic-setup/).

 - Clone the git repository into your Eclipse workspace directory

 - Create a new C++ AVR Cross Target Application project called 'rfm_edf_ecomanager'.  Be sure to modify the build settings for this project as described in Francesco's guide.

Building without Eclipse or the Arduino IDE
-------------------------------------------

I'm afraid building this code isn't especially user-friendly at the moment
because I'm developing on Eclipse and am using the auto-generated makefile
at the moment while there's a lot of code churn. If I have time I'll manually
create a more user friendly makefile.

I haven't tried this so I'm afraid I don't know if this will work but
here are some pointers.

First, open Release/subdir.mk.  You'll almost certainly need to modify
the include directories to point to the relevant directories on 
your system.

Then run:

```bash
cd Release
make all
```
Then upload your `rfm_edf_ecomanager.hex` using the "[Uploading pre-compiled hex file](#uploading-pre-compiled-hex-file)"
instructions above.

Warranty
========

Sorry to have to shout, but:

THERE IS NO WARRANTY FOR THE PROGRAM, TO THE EXTENT PERMITTED BY APPLICABLE
LAW. EXCEPT WHEN OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS AND/OR OTHER
PARTIES PROVIDE THE PROGRAM “AS IS” WITHOUT WARRANTY OF ANY KIND, EITHER
EXPRESSED OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK AS TO THE
QUALITY AND PERFORMANCE OF THE PROGRAM IS WITH YOU. SHOULD THE PROGRAM PROVE
DEFECTIVE, YOU ASSUME THE COST OF ALL NECESSARY SERVICING, REPAIR OR CORRECTION.

