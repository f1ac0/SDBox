# SDBox
The SDBox project by jbilander and based on the SPI adapter by niklasekstrom is a wonderful parallel sdcard reader for Amiga computers. Thank you guys for sharing it under GPLv3 license.
I use it to transfer files either to my A500 with internal IDE adapter or to my A600 or 1200 without blocking the PCMCIA port.

The project in this repository is just a recrated board making use of the bare chips instead of breadboard modules.
- It is smaller
- It accomodates big SD cards instead of microSD
- It takes its power from a Mini or Micro USB or from a pin header (I use it to power another serial adapter using the same power pack)
- It does not include the 2nd LED and power switch
- It uses SMD stuff

I guess it is not better than the original, just different for those who prefer tiny (but maybe harder to solder) stuff.

# BOM
1x Male DB25 header
1x SDCARD socket (SDP11-4-12B on the schematic I have but known with other names online)
1x ATMEGA 328p-au
1x SPX3819M5-L-3-3 3.3v LDO
1x 16MHz HC-49S crystal
2x 1uF (or more) 0805 capacitors
3x 100nF 0805 capacitors
2x 22pf 0805 capacitors
1x 4.7K 0805 resistor
1x 6.8K 0603x4 resistor array
1x 4.7K 0603x4 resistor array
1x optional 0805 LED and 0805 resistor (330 ohm or more)
For power, install the one you need :
1x Mini USB Female Socket 4 foot
1x Micro USB Female Socket B type 4.85 horn connector
1x2 2.54mm pin header

# Making it
I recommend 1.6mm PCB since it is sandwiched between the pins of the DB25 connector.
Check for shorts at least between 5V, 3.3V, and GND traces before applying power !
The programming port does not need to be soldered since it needs to be programmed just once : you can just hold it in place during the few seconds needed for programming.

There are several methods to program the uC. I personnaly used a standard TTL serial adapter connected to all the pins of the prog pin header, and with avrdude provided in the arduino setup :
```
~/arduino/hardware/tools/avr/bin/avrdude -C~/arduino/hardware/tools/avr/etc/avrdude.conf -v -patmega328p -carduino -P/dev/ttyUSB0 -b57600 -D -Uflash:w:main.hex:i
```

# Using it
- Plug it to the parralel port
- Plug it to power block
- Insert SDcard
- Apply power
- Turn amiga on
- Install the drivers
- Mount the sdcard using mount devs:SD0
- Unmount the sdcard using assign SD0: DISMOUNT

# About hotplugging.
If you care about your Amiga, this is a bad idea to plug or unplug the parallel port while live.
If you care about the data on the card or the card itself, it might also be a bad idea to plug or unplug it while power is applied. I personnaly have done so several times already, just dismount the partition before unplugging.
