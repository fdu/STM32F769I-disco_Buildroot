Linux on the STM32F769I Discovery board with Buildroot
======================================================

The project is a set of patches and configuration files to build a bootloader and a Linux based system image with a minimal root file system for the great [STM32F769I Discovery board](http://www.st.com/en/evaluation-tools/32f769idiscovery.html).

- Buildroot 2016.08.1
- GCC 4.4.1 (external)
- U-Boot from Emcraft
- Linux 4.2 from Emcraft
- Busybox
- OpenOCD 0.10.0

Build
-----

Let's download, extract and patch Buildroot:

`$ make bootstrap`


Then build:

`$ make build`


After the build, the directory `buildroot/output/images/` contains 
 - U-Boot `u-boot.bin` and its environment configuration `uboot-env.bin`
 - a U-Boot image `stm32f769i-disco_system.uImage` containing the Linux kernel, a RAM disk linked to it, and the device tree for this board

Run
---

Flash U-Boot:

`$ make flash_bootloader`


U-Boot is pre-configured to load a system image called `stm32f7/stm32f769i-disco_system.uImage` from over TFTP from a host with `IP 192.168.201.6` (change the configuration in `configs/uboot-env`). This image can be written to the embedded SPI flash with the command `update_spi` in U-Boot. After this, U-Boot can be configured to boot from the SPI with `boot_spi`.

Boot log
--------

Output coming through USART6:
```
U-Boot 2010.03-00000-g884d7b3 (***)

CPU  : STM32F7 (Cortex-M7)
Freqs: SYSCLK=216MHz,HCLK=216MHz,PCLK1=54MHz,PCLK2=108MHz
Board: STM32F769I-DISCO Revision B-01, www.emcraft.com
DRAM:  16 MB
In:    serial
Out:   serial
Err:   serial
QSPI:  64 MB mapped at 0x90000000
Net:   STM32_MAC
Hit any key to stop autoboot:  0 
Booting from network...
...
[load image and boot Linux kernel]
...
Freeing unused kernel memory: 480K (c01c2000 - c023a000)
Starting logging: usb 1-1: new high-speed USB device number 2 using dwc2
OK
Initializing random number generator... random: dd urandom read with 6 bits of entropy available
done.
Starting network: OK

Welcome to Buildroot
buildroot login: root
Jan  1 00:35:13 login[66]: root login on 'console'
~ #
```
