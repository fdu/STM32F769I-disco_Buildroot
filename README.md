# Linux on the STM32F769I Discovery board with Buildroot

The project is a set of patches and configuration files to build a bootloader and a Linux based system image with a minimal root file system for the great [STM32F769I Discovery board](http://www.st.com/en/evaluation-tools/32f769idiscovery.html).

## Build

Let's download, extract and patch Buildroot 2016.08.1:
`$ make bootstrap`

Then build:
`$ make build`

After the build, the directory `buildroot/output/images/` contains 
 - U-Boot `u-boot.bin` and its environment configuration `uboot-env.bin`
 - a U-Boot image `stm32f769i-disco_system.uImage` containing the Linux kernel, a RAM disk linked to it, and the device tree for this board

## Run

Flash U-Boot:
`$ make flash_bootloader`

U-Boot is pre-configured to load a system image called `stm32f7/stm32f769i-disco_system.uImage` from over TFTP from a host with `IP 192.168.201.6` (change the configuration in `configs/uboot-env`). This image can be written to the embedded SPI flash with the command `update_spi` in U-Boot. After this, U-Boot can be configured to boot from the SPI with `boot_spi`.

