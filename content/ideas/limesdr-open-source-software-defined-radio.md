* [quicky intro to sdr](http://hackaday.com/2016/05/30/hackaday-dictionary-software-defined-radio-sdr/)
* [Sodera - Your Introduction into SDR](http://sodera.de/)
* LimeSDR and its toolchain have already been used to create a Wireless Multi-tool for IoT, [Part 1](http://www.rs-online.com/designspark/electronics/eng/blog/an-intel-powered-wireless-multi-tool-for-the-iot-part-1), [Part 2](http://www.rs-online.com/designspark/electronics/eng/blog/an-intel-powered-wireless-multi-tool-for-the-iot-part-2), [source code](https://github.com/DesignSparkrs/sdr-ble-demo/)

![limesdr](https://www.crowdsupply.com/img/31d2/limesdr-7_jpg_project-body.jpg)
Ever since I become aware of [RTL-SDR][20] and how it could be used to create
a very cheap [software defined radio (SDR)][21]
by uses a [TV tuner dongle based on the RTL2832U chipset][22],
I have been hooked on diving deeper into SDR.
The use of the TV dongle and the RTL-SDR software is very much a hack,
and can't come close to the abilities of professional grade SDR.
I have been watching the product development in this SDR space,
many are expensive or have technical limitations.
This has been changing (e.g. [HackRF][23]) but I still didn't feel I was getting
enough for the money.

With the arrival of [LimeSDR][24], I'm read to part with my money.
I recently enthusiastically backed a crowd sourced SDR hardware build for $250
(list price will be $300).
[Lime Microsystems][03] launched this project via [CrowdSupply][01].
Lime has also received the [backing of the UK mobile operator EE][18]
and [Ubuntu will supply an App Store for the LimeSDR][19].

Lime billed it project as:

**A Software Defined Radio for Everyone**

LimeSDR is a low cost, open source, apps-enabled software defined radio (SDR)
platform that can be used to support just about any type of wireless communication standard.
LimeSDR can send and receive UMTS, LTE, GSM, LoRa, Bluetooth, Zigbee, RFID,
and Digital Broadcasting, to name but a few.

While most SDRs have remained in the domain of RF and protocol experts,
LimeSDR is usable by anyone familiar with the idea of an app store -
it’s the first SDR to integrate with Snappy Ubuntu Core.
This means you can easily download new LimeSDR apps from developers around the world.
If you’re a developer yourself,
you can share and/or sell your LimeSDR apps through Snappy Ubuntu Core as well.

The LimeSDR platform gives students, inventors,
and developers an intelligent and flexible device for manipulating wireless signals,
so they can learn, experiment, and develop with freedom from limited functionality
and expensive proprietary devices.

**Features & Specifications**

* **RF Transceiver:** Lime Microsystems LMS7002M MIMO FPRF ([Datasheet][04])
* **FPGA:** Altera Cyclone IV EP4CE40F23 - also compatible with EP4CE30F23
* **Memory:** 256 MBytes DDR2 SDRAM
* **USB 3.0 controller:** Cypress USB 3.0 CYUSB3014-BZXC
* **Oscillator:** Rakon RPT7050A @30.72MHz ([Datasheet][05])
* **Continuous frequency range:** 100 kHz – 3.8 GHz
* **Bandwidth:** 61.44 MHz Digital Interface (160MHz Analog Interface)
* **RF connection:** 10 U.FL connectors (6 RX, 4 TX)
* **Power Output (CW):** up to 10 dBm
* **Multiplexing:** 2x2 MIMO
* **Power:** micro USB connector or optional external power supply
* **Power Consumption:** typically 880 mW in full 2x2 MIMO mode (550 mW in SISO mode)
* **Status indicators:** programmable LEDs
* **Operating System:** Snappy Ubuntu Core (Linux), running on USB-connected host system
* **Dimensions:** 100 mm x 60 mm

# Who is Lime Microsystems
[Lime Microsystems][03] is the creator of
[the world's first field programmable RF (FPRF) chip][02]
and uses this technology in the LimeSDR.
[Field Programmable Gate Arrays (FPGAs)][06] are semiconductor devices that are
based around a matrix of configurable logic blocks (CLBs)
connected via programmable interconnects.
FPGAs can be reprogrammed to desired application or functionality requirements after manufacturing.
This feature distinguishes FPGAs from Application Specific Integrated Circuits (ASICs),
which are custom manufactured for specific design tasks.

Some FPGAs have analog functions but FPGAs generally don't touch the analog world.
In contrast, the Lime FPRF deals directly with analog.
At the highest level of abstraction, the FPRF transmitter takes a digital data stream
and converts it into an analog wireless signals,
while the receiver perform the inverse operation.
Add to this the capability to program key parameters like the RF frequency,
gain, and bandwidth, and you have the essential ingredients of an FPRF chip.
The FPRF allows you to experiment with radio characteristics
by changing parameters on the fly.

![trans-path](http://img.deusm.com/eetimes/2014/02/1320986/fprf-pad-0005-02.jpg)
In the transmit path,
the first operation perfromed is to accepts data as
[In-phase (I Data) and Quadrature (Q Data)][07] words.
The transmit path applies the data to a pair of on-chip Digital to Analog Converters (DAC)
to convert it into two analog signals.
The user can choose to bypass the DACs and inject analog signals directly
into the device or monitor the DAC outputs.

The next operation involves filtering the analog signal.
This pass band filter is programmed by the user to a selectable set of bandwidths.
The filtering restricts the signals to the selected bandwidth,
and attenuates any out-of-band noise or aliasing from the DAC.

The next stage is a programmable baseband gain stage that can be user adjusted.
The signal is then mixed to directly give the required modulated RF frequency output.
This is done with a Phase Lock Loop (PLL) clock by a programmable ratio,
which generates a stable frequency radio frequency signal.

The programmable RF gain stage provides the final signal boost that is output from the FPRF device.
The transmit power level is sufficient for short range communications,
without any further amplification, or use external amplification to increase the range.

![recie-path](http://img.deusm.com/eetimes/2014/02/1320986/fprf-pad-0005-03.jpg)
On the receiver path, the FPRF device offers a choice of low noise amplifiers (LNAs).
A general broadband input stage is designed to handle RF inputs across a wide spectrum.
Other LNAs are optimized for enhanced performance for signals in specific frequency bands.

Next the mixer in the receive path uses the PLL clock to provide direct down conversion.
Programmable gain stages and filtering are applied,
before the analog signal is digitised and output as [I&Q data][08] streams.
Of course, the entire receiver path is also highly user programmable,
just like the transmit path.

Configuration of all the different elements is performed
via a [Serial Peripheral Interface (SPI)][09] into the control logic.
Each element is programmed by loading static data or the parameters can be changed on the fly.
The chip was designed to be highly flexible,
because one of the key applications is for cellular femto and pico cells.
These boxes act as local base stations for cell phones,
and link into the Internet to provide fast connectivity inside the home or small office.
The challenge in designing an RF chip for these applications
but for cellular systems that are different around the world.

https://www.youtube.com/watch?v=8IrO4mg2ToA

#  Myriad RF
Lime is a supporter of [MyriadRF][10],
a low cost universal radio platform, based on flexible and programmable integrated circuits.
The MyriadRF websit states,
"Myriad RF is a family of open source hardware and software projects for wireless communications, and a community that is working to make wireless innovation accessible to as many people as possible."

* [Lime Suite](https://myriadrf.org/projects/lime-suite/)

# LimeSDR Application Ecosystem
Appears [Josh Blum][14] (a major [contributor to several SDR tools][17])
played a [major role][15] in the [LimeSuite software][16],
making sure that LimeSDR is well supported by SDR software tools/platfroms,
and to provide some example demonstrations.

https://myriadrf.org/blog/limesdr-application-ecosystem/

## LMS Suite Software
The board’s host driver architecture, meanwhile, supports both the SoapySDR and UHD APIs. The firmware supports advanced features liked timed TX bursts and RX sample timestamps, “as required for use with GSM and other time-sensitive protocols,” says the project. The LimeSDR’s host driver is built on a “Lime Suite” low level library that handles programming and calibration of the LMS7002M FPRF transceiver, among other gnarly internal communications.

http://wiki.myriadrf.org/LMS_Suite
https://myriadrf.org/projects/lime-suite/
https://myriadrf.org/blog/limesuite-driver-architecture/

## SoapySDR
SoapySDR is the glue layer that sits between the LimeSDR’s driver
and SDR applications.
LimeSDR uses a wrapper (SoapyLMS7)
so it can be supported by SoapySDR or GrOsmoSDR.
This provides support for programming environments like
the Pothos framework, GNU Radio, GQRX, and CubicSDR.

## Snappy Ubuntu Core
Lime Microsystems has partnered with [Canonical][25],
so that the LimeSDR board can take advantage of [Snappy Ubuntu Core][26].
The Snappy version of Ubuntu features an app store, [hacker-proof updates][28], and a 128MB RAM footprint.
Canonical states this is the smallest, safest Ubuntu ever,
and they are particualty [targing IoT embedded devices][27]
(Ubuntu 15.04 includes Snappy).
It can be use in the cloud or on samll devices.
The IoT version of Snappy requires a 600MHz CPU and 128MB RAM,
only 40MB of which is directly used by the system,
while the rest is available for apps.
The system also needs 4GB of flash for factory reset and system rollback.

Lime claims that via the Ubuntu software ecosystem,
users will be able to download apps that put LimeSDR to a variety of uses:
an IoT gateway for smart-home products, a cellular base station,
a streaming media server, even radio astronomy.
Developers will be able to share and distribute their own creations as well.

## GNURadio

## Pothos
[Pothos][11] is an [open source project][12] is a dataflow framework for
creating topologies of interconnected processing blocks.
Topologies can be distributed across hosts.
Pothos boasts an elegant framework API,
as well as a fully-functional graphical topology designer.
[Pothos SDR][13] is a development environment for Windows,
making it easier for Windows users to design and develop for SDR hardware.

http://www.joshknows.com/projects
http://www.pothosware.com/
[Pothos features summary page](https://github.com/pothosware/pothos/wiki/Features)

## LuaRadio
GNURadio is a gigantic suite of software,
and it’s a lot harder to code up in Python than it is to use the GUI.
The LuaRadio project trys to deal with these shortcomings  bykeeping things easy to code
and keeping the codebase small and tidy.

http://luaradio.io/docs/reference-manual.html
http://luaradio.io/examples/rtlsdr-wbfm-mono.html
http://luaradio.io/docs/embedding-luaradio.html
http://luaradio.io/docs/comparison-gnuradio.html

# Digital Signal Processing
* [three-part tutorial on using Octave](http://hackaday.com/2016/06/30/tutorial-on-signal-processing-in-linux-with-octave/)
* [ MATLAB under Linux](https://help.ubuntu.com/community/MATLAB)
* Scilab, Freemat, Sage, and Spyder


##############################
[MyRiad RF has confirmation][29] that LimeSDR can be made to work together with an
Ubuntu Virtualbox VM, on top of Windows 10, and via USB passthrough from the host computer.
##############################



[01]:https://www.crowdsupply.com/lime-micro
[02]:http://www.eetimes.com/author.asp?doc_id=1320986
[03]:http://www.limemicro.com/
[04]:https://myriadrf.org/blog/lms7002m-datasheet-now-available-wiki/
[05]:http://www.rakon.com/products/families/download/file?fid=39.225
[06]:https://en.wikipedia.org/wiki/Field-programmable_gate_array
[07]:https://en.wikipedia.org/wiki/In-phase_and_quadrature_components
[08]:http://whiteboard.ping.se/SDR/IQ
[09]:https://learn.sparkfun.com/tutorials/serial-peripheral-interface-spi
[10]:https://myriadrf.org/
[11]:http://www.pothosware.com/#overview
[12]:https://github.com/pothosware/pothos/wiki
[13]:http://www.joshknows.com/blog/67/AnnouncingPothosSdrDevEnvironment
[14]:https://www.linkedin.com/in/josh-blum-1681537a
[15]:http://www.joshknows.com/blog/74/LimesdrOnTheCrowdFundingCampaignTrail
[16]:https://myriadrf.org/projects/lime-suite/
[17]:http://www.joshknows.com/projects
[18]:http://www.limemicro.com/press-releases/ee-backs-lime-microsystems-crowdfunding-campaign-leapfrog-wireless-innovation-uk/
[19]:http://www.limemicro.com/press-releases/ubuntu-app-store-announced-limesdr-developed-applications/
[20]:http://www.rtl-sdr.com/about-rtl-sdr/
[21]:https://en.wikipedia.org/wiki/Software-defined_radio
[22]:https://www.amazon.com/gp/product/B008S7AVTC/ref=oh_details_o00_s00_i00?ie=UTF8&psc=1
[23]:https://greatscottgadgets.com/hackrf/
[24]:https://myriadrf.org/projects/limesdr/
[25]:http://www.canonical.com/
[26]:http://www.ubuntu.com/internet-of-things
[27]:http://hackerboards.com/lightweight-snappy-ubuntu-core-os-targets-iot/
[28]:http://thenewstack.io/snappy-ubuntu-core-powering-microcontrollers-to-microservices/
[29]:https://myriadrf.org/blog/limesdr-native-windows-via-ubuntu-vm/?utm_source=LimeSDR+supporters&utm_campaign=7c106bb9cf-Project_Update_Lime_Beta_7_7_2016&utm_medium=email&utm_term=0_1e5a81cd57-7c106bb9cf-112302893
[30]:
[31]:
[32]:
[33]:
[34]:
[35]:
[36]:
[37]:
[38]:
[39]:
[40]:
