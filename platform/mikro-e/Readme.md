# Using Contiki on Mikro-E Clicker

## Overview

This section explains how to build Contiki code for Mikro-E Clicker and to flash the compiled application image on Mikro-E Clicker.
Please refer [6LoWPAN Clicker Quick Start Guide](https://docs.creatordev.io/clicker/guides/quick-start-guide/) for more details about the 6LoWPAN clicker.

## Package Content

Some key paths of source code added to support Contiki on Mikro-E Clicker:

| Folder              				| Content                                              							                      |
| :----               				| :----                                                							                      |
| platform/mikro-e			      | Porting of drivers for peripherals like Button, LED, CA8210 etc. on Mikro-E Clicker			|
| examples/mikro-e            | Applications for Mikro-E Clicker board                                                  |         

## Cascoda ca8210 transceiver support

Cascoda ca8210 transceiver driver has been added git submodule. So you first need to checkout the driver code before building any contiki application based upon ca8210.

    $ git submodule init "dev/ca8210"
    $ git submodule update

## Getting Started

The xc32 compiler version 1.34 from Microchip can be used for compilation of the source code. Download the xc32 compiler from
[Microchip's website](http://www.microchip.com/pagehandler/en_us/devtools/mplabxc/) and add tool chain path in the
environment variables and compile an example, say "Hello World" which is included in Contiki as per below:

    $ export PATH=$PATH:/opt/microchip/xc32/v1.34/bin/

* Platform mikro-e makefile builds the application for 6LoWPAN clicker.
* 6LoWPAN channel(default 26) and pan_id(default 0xabcd) can be passed from makefile options.
* For debugging purposes, UART3 will be used by default, but USE_SERIAL_PADS can be selected for UART2.

The application e.g. Hello World can be built for Mikro-E Clicker and HEX file can be generated to flash on the board along with possible build options as per below:


    $ cd examples/hello-world
    $ make TARGET=mikro-e CHANNEL=26 PAN_ID=0xabcd USE_SERIAL_PADS=1
    $ /opt/microchip/xc32/v1.34/bin/xc32-bin2hex hello-world.mikro-e

