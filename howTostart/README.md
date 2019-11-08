# ULX3S startup guide

First thing you will need are tools and binaries for ULX3S boards

Just clone it on your computer 

    git clone https://github.com/emard/ulx3s-bin

Go to ulx3s-bin folder

    cd ulx3s-bin

In usb-jtag folder is prebuild ujprog with OS architectures.

We will use ujprog for board programming.

For x64 linux you just need to copy ujprog to some folder that will be in PATH

    sudo cp ulx3s-bin /usr/local/bin

Now we can use ujprog tu upload bitstream to your board.

First we can try to uplad selftest so you can check how board is running.

Insert SD card into slot (it will be faster)

Connect ULX3S to HDMI monitor (be aware that some big screens do not like smaller resolutions).

Now just load bitstream for your FPGA version into the SDRAM (non permanent).

Instead of XXX you need to put 12F or 45F or 85F depending on what you bought.

    ujprog fpga/f32c/f32c-XXX-v20/f32c_ulx3s_v20_XXX_selftest_100mhz.bit

When upload is finished you will see color test screen 640x480 and LEDS will fade.

Now we have f32c softcore runing inside FPGA.

To tell the core to load selftest binary file to f32c selftest use python script

    fpga/f32c/f32cup.py fpga/f32c/f32c-bin/selftest-mcp7940n.bin

You should get something like:

f32c python uploader (under construction)

    MIPS Little-Endian header received
    ADDR 0x80000000 LEN 8208 CRC 0xF17DE856 OK
    ADDR 0x80002010 LEN 8192 CRC 0x58788D1D OK
    ADDR 0x80004010 LEN 6124 CRC 0xC922F84A OK
    JUMP 0x80000000

Now you should see selftest screen

For permanent load use 

    ujprog -j FLASH XXX.bit

That will load bitstream into FLASH, and it will reload into FPGA after reboot...

Board is unbreakable by software so you can try...

If you want to load bitstream that already contains binary for f32c we usually have .img file.

    ujprog f32c_ulx3s_v20_12k_selftest_100mhz_ws2_flash.img

If it reports error you can just rename .img to .bin and reload

    mv f32c_ulx3s_v20_12k_selftest_100mhz_ws2_flash.img f32c_ulx3s_v20_12k_selftest_100mhz_ws2_flash.bit
    ujprog f32c_ulx3s_v20_12k_selftest_100mhz_ws2_flash.bit

With img file loaded you should have selftest running in one step.

Experiment with other bit/img samples inside fpga folder

### ESP32

If your board has ESP32 onboard -- it may be already loaded with default web server

First thing you need to do to start working with ESP32 directly is to load passthru into FLASH

    ujprog -j flash fpga/passthru/passthru-v20-12f/passthru_ulx3s_v20_12k.bit

Reset board!

Now FPGA is connecting FTDI chip with ESP32 chip so you can use ESP32 independently

Check this tutorial if you want to use visual studio for ESP32 programming

https://gojimmypi.blogspot.com/2019/06/ulx3s-and-visual-micro-in-visual-studio.html

You can also use Arduino

Board is really mature and you can load anything to ESP32 (you will not brake it)

If you want to go back to web interface you need to reload ESP32

While in ulx3s-bin folder 

xxx if your FPGA version for example 12f

    cd esp32
    upload-executable.sh
    upload-spiffs.sh websvf_sd/websvf_sd_v20_xxx.spiffs.bin

When you have passthrue loaded you can also put SD card with wifi.config file and paste 

    XXXX
    XXXX
    XXXX
    XXXX

To tell ESP32 on start to connect to your wifi router.

Once you have SD card in place reboot board.

If you have OLED connected it you will see IP address of ESP32

If not you can always find IP with 

Change IP to be in you network IP range (usually 192.168.1.0)

    nmap -sP XXX.XXX.XXX.0/24 

When you have IP you can go to web browser and go to http://IP

From there you can upload files to SD card or just load SVF files to FPGA

### Using board with lattice diamond tool

You can find lattice diamond tool online and use free license.

After building bitstream you will need to use ujprog for loading bitstream as we shown before.

### Using board with apio

Check this repository to setup environment

https://github.com/ulx3s/fpga-odysseus

Presentation setup is done by Miodrag

https://github.com/mmicko

After you have all you need you can follow this presentation

https://github.com/ulx3s/fpga-odysseus/blob/master/presentation/FPGA%20Odysseus.pdf

### Using board with opensource toolchain

As apio does not have newest toolchain you may notice some problems...

So best way to do development it to use opensource toolchain

You can use this documentation

https://github.com/emard/ulx3s-examples/blob/master/OpenSource-toolchain/README.md

### Using board with IceStudio

Still into development you would need to wait a bit -- but mmicko has some progress

https://github.com/mmicko/icestudio

### Samples and links 

https://github.com/emard/ulx3s-examples

https://github.com/RadionaOrg/ulx3s-links

### Contacts 

We hangout on gitter feel free to contact us!

https://gitter.im/ulx3s/Lobby

We are also on email:

ulx3s.fpga@gmail.com

### Specifications

https://radiona.org/ulx3s

### Orders and buy -- soon at

https://www.crowdsupply.com/radiona/ulx3s

### Social networks

https://twitter.com/RadionaOrg

https://hr-hr.facebook.com/Radiona.org/

https://www.instagram.com/radiona_org/

https://www.flickr.com/photos/lomodeedee/sets/

### Main page

https://radiona.org/

#### Blogspots:

https://trmm.net/Spispy

https://gojimmypi.blogspot.com/search?q=ULX3S

http://langster1980.blogspot.com/

#### Wiki

https://en.wikibooks.org/wiki/Oberon

#### Articles

https://eprint.iacr.org/2019/1152.pdf
