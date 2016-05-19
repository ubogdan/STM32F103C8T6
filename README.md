# STM32F103C8T6
Included is a demo project that flashes a led connected to PC13 (ready to run on an STM32 Mini Dev Board STM32F103C8T6). 

If you have an J-Link programmer you are allmost ready to play with your device.

Configuration is done through these files:
```
makefile          build options (optimization, etc)
stm32.ld          target memory size and type
stm32f10x_conf.h  firmware library configuration
stm32f10x_it.c    interrupt handlers
jtag/flash.cfg    OpenOCD configuration (JTAG dongle, etc)
```

## Building OpenOcd 0.9
```
sudo apt-get install libusb-dev
git clone git://git.code.sf.net/p/openocd/code openocd-code
cd openocd-code
git checkout tags/v0.9.0
./configure --enable-maintainer-mode --disable-werror --enable-jlink
make
sudo make install
```

## Flashing target
Edit file `jtag/openocd.conf` and chage `transport select jtag` or `transport select swd` according to your board connector

Run command to build and flash the device
````
make flash
````
## Flashing Maple Boot
````
user@local ~ $ openocd -f jtag/openocd.cfg
user@local ~ $ telnet localhost 4444
> reset halt
> flash write_image erase bootloader/maple_mini_boot.bin 0x08000000
> reset run
````
# dmesg Output
````
user@local ~ $ dmesg
[ 2745.356014] usb 6-1: new full-speed USB device number 49 using uhci_hcd
[ 2745.523034] usb 6-1: New USB device found, idVendor=1eaf, idProduct=0003
[ 2745.523038] usb 6-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[ 2745.523040] usb 6-1: Product: Maple 003
[ 2745.523043] usb 6-1: Manufacturer: LeafLabs
[ 2745.523045] usb 6-1: SerialNumber: LLM 003
````

## Hardware
![alt tag](https://raw.githubusercontent.com/ubogdan/STM32F103C8T6/master/jtag/STM32F103C8T6-1.jpg)

![alt tag](https://raw.githubusercontent.com/ubogdan/STM32F103C8T6/master/jtag/STM32F103C8T6-2.jpg)

