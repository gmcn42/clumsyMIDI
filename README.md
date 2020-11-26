# clumsyMIDI
A Raspberry Pi expansion board containing a MIDI interface, DAC, and OLED display requiring only through-hole soldering skills. This is primarily intended as an all-in-one hardware solution for the [mt32-pi Roland MT-32 emulator](https://github.com/dwhinham/mt32-pi) but all features are usable with Raspberry Pi OS, too.

## Features
* TI PCM5102 I2S HiFi DAC (using the ubiquitous GY-PCM5102 carrier board)
* GPIO MIDI interface with in, out, and thru
* 0.91" OLED display
* large-ish 5V bypass capacitor which may help with slightly weak power supplies
* works with [mt32-pi](https://github.com/dwhinham/mt32-pi) and Raspberry Pi OS
* no SMT soldering required, suitable for DIY electronics beginners and clumsy people ;)

## Schematic and BOM
Schematic and BOM are available in the [`pdf/` subfolder](https://github.com/gmcn42/clumsyMIDI/tree/main/pdf).

## How to get the PCB
You can get a zip file with the Gerber files from the releases page and 
