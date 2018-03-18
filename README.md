Linux on the STM32F769I Discovery board with Buildroot
======================================================

The project is a set of patches and configuration files to build a bootloader and a Linux based system image with a minimal root file system for the great [STM32F769I Discovery board](http://www.st.com/en/evaluation-tools/32f769idiscovery.html).

Build
-----

Let's download, extract and patch Buildroot:

`$ make bootstrap`


Then build:

`$ make build`


After the build, the directory `buildroot/output/images/` contains 
 - U-Boot images `u-boot-spl.bin` and `u-boot.bin`
 - compressed Linux kernel with linked RAM filesystem `zImage`
 - device tree blob `stm32f769-disco.dtb`

Run
---

Flash U-Boot:

`$ make flash_bootloader`

U-Boot is pre-configured to load a kernel file called `/stm32f769/zImage` and a DTB called `/stm32f769/stm32f769-disco.dtb` from the first partition of the micro SD card. If the user button (the blue one) is press when U-Boot starts, then those files are loaded over TFTP from a host with IP `192.168.201.6`.

Changelog
---------

* 0.2
  * Buildroot 2018.02
  * GCC 7.3.0
  * U-Boot v2018.03
  * Linux 4.15.10

* 0.1
  * Buildroot 2016.08.1
  * GCC 4.4.1 (external)
  * U-Boot from Emcraft
  * Linux 4.2 from Emcraft
  * Busybox
  * OpenOCD 0.10.0
