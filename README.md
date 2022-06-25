# RS41GEN is modified version of RS41HUP to use RS41 as an RF frequency generator
The idea is to use two RS41 as a clock source for RTL_SDR dongles, first can be set to 390.0MHz and second to 418.805MHz for example. RF outputs are connected to some Double Balanced Mixer, i used one ESMD-C2HX2, Schottky by MACOM. Mixer output is filtered by 3rd order Chebyshev lowpass filter and can feed few RTL_SDR dongles, just connect it to each R820T pin 9 trought 100pF capacitor. By this way we can moove the well known birdie of RTL_SDR from 403.2 to some other QRG, where there is no chance to mess with signal from any sonde, received in your location. My favorite DX sondes are those launched from Budapest Hungary, about 600km from me and their frequency is exactly 403.2MHz. When i upgrade my RTL_SDRs with TCXO my nightmare begin, so that is my temporary solution, untill i get one Si5351 with TCXO and add to its output 5th or more order lowpass filter.

The text below is unchanged from RS41HUP: 

# RS41HUP (Ham Use Project)
Firmware for RS41 for HAM use.

It is possible to recycle RS41-SGP sondes for amateur radio use without any electrical changes! You just have to build a new firmware (this one) and apply it via a cheap adaptor "ST-Linkv2". Modified sonde now transmits on defineable frequenca in 70cm band GPS and telemetry data in FSK RTTY format which is used by HAB projects and additionally it transmits APRS packets on a seperately defineable TX frequency.

Released under GPL v2


# Windows:

Use:
https://www.wyzbee.com/download/Utilities/Software/CoIDE-1.7.8.exe

And:
https://launchpad.net/gcc-arm-embedded/5.0/5-2016-q3-update/+download/gcc-arm-none-eabi-5_4-2016q3-20160926-win32.exe


# Linux:
Maybe you have to set correct path to gcc-arm-none-eabi in CMakeLists.txt.<br><br>

cd into main folder

cmake .

make

# Configuration
All configs in ```config.h```

* ```SEND_RTTY``` Optionally send RTTY packet every ```TX_DELAY``` ms
* ```SEND_RTTY_<value>``` Include <value> into the RTTY packet
* ```RTTY_CALLSIGN``` RTTY callsign
* ```RTTY_COMMENT``` RTTY comment
* ```RTTY_WWL``` Send WWL instead of the RTTY comment
* ```PAIR_COUNT``` World Wide Locator pairs (precision)
* ```RTTY_FREQUENCY``` RTTY frequency in MHz
* ```RTTY_DEVIATION``` RTTY shift configurable in 270Hz steps
* ```RTTY_SPEED``` RTTY speed in bauds
* ```RTTY_7BIT``` Use 7 bit RTTY
* ```RTTY_USE_2_STOP_BITS``` Use 2 stop bits
* ```SEND_APRS``` Optionally send APRS packet every ```TX_DELAY``` * ```RTTY_TO_APRS_RATIO``` ms
* ```APRS_CALLSIGN``` APRS callsign, 6 characters. If your callsign is shorter add spaces
* ```APRS_SSID``` APRS SSID
* ```APRS_DISPLAY_TABLE``` APRS Display Table
* ```APRS_DISPLAY_SYMBOL``` APRS Display Symbol
* ```APRS_COMMENT``` APRS comment
* ```APRS_FREQUENCY``` APRS frequency in MHz
* ```RTTY_TO_APRS_RATIO``` Number of RTTY frames between each APRS frame
* ```SEND_MORSE``` Optionally send Morse message every ```TX_DELAY``` * ```RTTY_TO_MORSE_RATIO``` ms
* ```MORSE_PREFIX``` Start of the Morse message (DE <callsign>)
* ```SEND_MORSE_<value>``` Include <value> into the Morse message
* ```MORSE_SUFFIX``` Optional end of the Morse message (ar^)
* ```MORSE_WPM``` Morse speed in words per minute
* ```RTTY_TO_MORSE_RATIO``` Number of RTTY frames between each Morse message
* ```TX_POWER``` Power 0-7, (7 means 42.95 mW@434.150 MHz measured on E4406A)
* ```ALLOW_DISABLE_BY_BUTTON``` Allow disabling device using button
* ```TX_DELAY``` Delay between RTTY frames in milliseconds
* ```LED_ENABLED``` Optionally /disable LED blinking (takes effect after approx. 10 minutes)


Have a nice day ;)

# Changelog
 * 14.12.2016 - Reverse engineeded connections, initial hard work, resulting in working RTTY by SQ7FJB
 * 07.01.2017 - GPS now using proprietiary UBLOX protocol, more elastic code to set working frequency by SQ5RWU
 * 23.01.2017 - Test APRS code, small fixes in GPS code by SQ5RWU
 * 06.06.2017 - APRS code fix, some code cleanup
 * June 2017 - starting with Linux support, making configuration more flexible by DF8OE
 * November 2018 by OK1TE
     * Optionally alter the RTTY comment with the World Wide Locator
     * Made the RTTY packet content configurable
     * Optionally turn off RTTY or APRS
     * Optionally turn off LED blinking
     * Added Morse (CW) support
 * 10.01.2020 - Configurable APRS Display Symbol

# TODO
 * Adding support for EmbiTZ IDE
 * Adding support for platform independent IDE Eclipse
 * More APRS config options
 * Temperature and moisture sensor
 * Pressure sensor
 * implementing protocol for using external devices on extension header
 * Configuration via extension header (serial connection) without need for reflashing firmware
 * Possibly add configuration "wireless" using RFID loop present in sonde
