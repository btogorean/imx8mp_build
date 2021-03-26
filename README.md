# Analog Devices's i.MX8MP CMOS TOF build scripts
# Forked from SolidRun

## Introduction
Main intention of this repository is be a build environment for i.MX8MP TOF based product evaluation.

The build script provides ready to use images that can be deployed on micro SD or eMMC.

The buildsystem is capable to create two different targets:
		1. Buildroot based initramfs (Intented for production)
		2. Ubuntu based ROOTFS (Intented for development)

## Build with host tools
Simply running ./runme.sh, it will check for required tools, clone and build images and place results in images/ directory.
The selection of target is performed using "BUILD_TYPE" variable from runme.sh script. Valid options are: ubuntu | buildroot

## Deploying
For SD card bootable images, plug in a micro SD into your machine and run the following, where sdX is the location of the SD card got probed into your machine -

`sudo dd if=images/microsd-<hash>.img of=/dev/sdX`

Take care S3 boot switches to be configured accordingly.

## Work In Progress
		1. Currently the modules geberated by the linux kernle build are not automatically copied in ROOTFS
			In folder build/linux-imx/ after kernel build step is created "modules.tar" archive
			The content of archive should be extracted over ROOTFS
			
		2. Automatic resize of the ROOTFS partition is not performed. Depending on the SD card the user can resize
		partition 2 to fill the whole SD card. Don't forget to "e2fsck -f /dev/sdX" and "resize2fs /dev/sdX"
