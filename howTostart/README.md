# ULX3S startup guide

First thing you will need are tools and binaries for ULX3S boards

Just clone it on your computer 

    git clone https://github.com/emard/ulx3s-bin

Go to ulx3s-bin folder

    cd ulx3s-bin

In usb-jtag folder is prebuild ujprog with OS arhitectures.

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

With img file loaded you shoud have selftest running in one step.

Experiment with other bit/img samples inside fpga folder

### ESP32

If your board has ESP32 onboard -- it may be already loaded with 