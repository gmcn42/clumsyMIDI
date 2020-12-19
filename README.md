# clumsyMIDI
A Raspberry Pi expansion board containing a MIDI interface, DAC, and OLED display requiring only through-hole soldering skills. This is primarily intended as an all-in-one hardware solution for the [mt32-pi Roland MT-32 emulator](https://github.com/dwhinham/mt32-pi) but all features are usable with Raspberry Pi OS, too.

[<img src="https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/assembled_with_pi_small.jpg" height="300">](https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/assembled_with_pi.jpg) [<img src="https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/assembled_top_small.jpg" height="300">](https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/assembled_top.jpg)

## Table of contents

<!-- toc -->
- [Features](#features)
- [Schematic and BOM](#schematic-and-bom)
- [How to get the PCB](#how-to-get-the-pcb)
  * [PCB Specs](#pcb-specs)
- [Assembly](#assembly)
  * [An ⚠IMPORTANT⚠ note on the DAC board solder bridges](#an-%E2%9A%A0important%E2%9A%A0-note-on-the-dac-board-solder-bridges)
  * [Rewiring MIDI Thru to Out](#rewiring-midi-thru-to-out)
  * [Mechanical Parts](#mechanical-parts)
  * [A General Note](#a-general-note)
- [Software Config](#software-config)
  * [mt32-pi](#mt32-pi)
  * [Raspberry Pi OS](#raspberry-pi-os)

<!-- tocstop -->

## Features
* TI PCM5102 I2S HiFi DAC (using the ubiquitous GY-PCM5102 carrier board)
* GPIO MIDI interface with in, out, and thru
* 0.91" OLED display
* large-ish 5V bypass capacitor which may help with slightly weak power supplies
* works with [mt32-pi](https://github.com/dwhinham/mt32-pi) and Raspberry Pi OS
* no SMT soldering required, so it should be suitable for clumsy DIYers like me ;)

## Schematic and BOM
Schematic and BOM are available in the [`pdf/` subfolder](https://github.com/gmcn42/clumsyMIDI/tree/main/pdf).

## How to get the PCB
You can get a zip file with the Gerber files from the [releases page](https://github.com/gmcn42/clumsyMIDI/releases/) and let your favorite board house build the PCB. Alternatively, you can also order directly from PCBWAY via [this link](https://www.pcbway.com/project/shareproject/clumsyMIDI___Raspberry_Pi_expansion_board.html) for convenience. Full disclosure: If you use the link, PCBWAY will donate 10% of the PCB price to me. I want to make clear that the PCB design is completely free and you are in no way obligated or even encouraged to use that link.

In case you want to make changes to the PCB before ordering somewhere, you can use [KiCAD](https://kicad.org/) and import the project.

***⚠IMPORTANT NOTE:⚠*** Before soldering down the DAC board make *sure* you check the assembly instructions below about the DAC's solder bridges. Their factory configuration appears to be varying from supplier to supplier and you may need to change them.

### PCB Specs
* PCB size (height * width): 56mm * 65mm
* Layers: 2
* Minimum drill size: 0.6mm
* Minimum track size: 0.25mm (=9.84mil)
* Minimum track clearance/spacing: 0.25mm (=9.84mil)
* Surface finish: by preference (the pictured boards are lead-free HASL but pretty much anything will do)

[<img src="https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/pcb_top_small.jpg" height="300">](https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/pcb_top.jpg)
[<img src="https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/pcb_bottom_small.jpg" height="300">](https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/pcb_bottom.jpg)


## Assembly
As all components are through-hole, you should get by with basic soldering skills. It is usually the best idea to start with the flattest components and work your way up. The 40-Pin GPIO socket should be soldered on last, also remember that it goes on the *bottom* :).

As shown in the BOM, I recommend socketing U1 and U2 as they are the most likely casualties if defective MIDI devices are connected for some reason. Be mindful of the ICs' orientation. The notch of the 74HCT14 should be where the notch is on the silkscreen. Likewise, the H11L1's dot (marking for Pin 1) should also face the in the direction of the notch on the silkscreen. If inserted correctly, U1 and U2 will "face outward and away from each other".

It is possible to leave out some components, e.g. if you only need MIDI-In. Consult [the schematic](https://github.com/gmcn42/clumsyMIDI/blob/main/pdf/clumsyMIDI-schematic.pdf) for details.

As I happily noticed people are actually really starting to build these things, I have opened the [discussions page](https://github.com/gmcn42/clumsyMIDI/discussions) of this project. If you have questions about anything related to the board and its assembly, feel free to open a topic!

### An ⚠IMPORTANT⚠ note on the DAC board solder bridges
Before soldering on the DAC board please double-check that the solder bridges on the bottom of your GY-PCM5102 are configured as in the following picture:

<img src="https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/solderbridges.jpg" height="240">

So: 1, 2, and 4 to L and 3 to H. This should be the standard factory-set config but at least one builder encountered a board with an unconnected bridge resulting in the DAC being permanently muted. If you have a multimeter you might also want to check good connection from the board's pins to rule out bad solder joints. FLT, FMT, and DEMP should have almost 0Ω to GND while XSMT should have almost 0Ω to pin 20 (top right) of the DAC chip itself.

If yours are un- or wrongly set, you'll have to resolder them.

### Rewiring MIDI Thru to Out
In standard configuration, the MIDI Thru output is available on a 5-pin header due to space constraints. If you do not need MIDI Out but want a MIDI Thru, it is possible to route the Thru signal to the MIDI-Out socket instead of the pin header. In that case, leave J4, R1, and R5 unpopulated and solder a wire between the footprint pads of J4 and R1 marked with a circle on the silkscreen, as shown in these two pictures (click for larger version):

[<img src="https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/midithru-top_small.jpg" height="300">](https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/midithru-top.jpg)
[<img src="https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/midithru-bottom_small.jpg" height="300">](https://github.com/gmcn42/clumsyMIDI/raw/main/pictures/midithru-bottom.jpg)

### Mechanical Parts
Be sure to use some kind of standoffs or similar when connecting clumsyMIDI to the PI. Without them, the board may sit lopsided and come in contact with the HDMI port, potentially causing a short circuit. Apart from that, it's more mechanically stable and simply looks nicer :). The BOM contains the brass standoffs I am using in the pictures.

### A General Note
Use caution and common sense while working with electronics, especially while soldering stuff. As stated in the license, I am offering this PCB design as-is incuding any and all defects it may have and will not be held liable for any harm that comes to you or others as a result of using/building/looking at it.

## Software Config
### mt32-pi
Follow the setup instructions on their site and then set the following options in `mt32-pi.cfg`:
```
usb = off
output_device = i2s
type = ssd1306_i2c
```
The option `gpio_thru` will also work with the MIDI Out port on clumsyMIDI, so use at your preference.

### Raspberry Pi OS
You need to add the following to `/boot/config.txt` to get GPIO MIDI, I2S DAC, and I2C support
```
enable_uart=1
dtoverlay=pi3-miniuart-bt
dtoverlay=midi-uart0

dtparam=i2s=on
dtoverlay=hifiberry-dac

dtparam=i2c_arm=on,i2c_arm_baudrate=400000
```
Also you need to comment out or remove the line `dtparam=audio=on`

Additionally for I2C support, add the following line to `/etc/modules`:
```
i2c-dev
```

To get regular ALSA MIDI support you need to bridge `/dev/ttyAMA0` and an ALSA MIDI port. You can do this with [`ttymidi`](https://github.com/cjbarnes18/ttymidi).
Once you have it compiled and installed, run the following in a terminal:
```
sudo ttymidi -s /dev/ttyAMA0 -b 38400
```
If you are asking yourself why it needs to be set to 38400 Baud: The line `dtoverlay=midi-uart0` causes the Pi's UART base clock to be slightly lowered, so that 38400 (a common RS232 baud rate) effectively becomes 31250 Baud which is MIDI-compatible.

Now you when run `aconnect -l` in another terminal, you should see a new MIDI client. Something similar to:
```
client 128: 'ttymidi' [type=user,pid=920]
    0 'MIDI out     '
    1 'MIDI in      '
```
Somewhat confusingly, the out/in naming is reversed because it is from the perspective of `ttymidi`. That means 'MIDI in' is what it receives from another application and then forwards to the UART. So if you want to play something on a synth connected to the clumsyMIDI's output, the correct command will be
```
aplaymidi -p 128:1 somefile.mid
```

The I2C display is supported by the [Adafruit SSD1306 Python library](https://github.com/adafruit/Adafruit_Python_SSD1306.git), among others.

Have fun!

clumsyMIDI ©2020 by Andreas Zdziarstek.<br>This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).<br>[![CC BY-SA 4.0](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-sa/4.0/)
