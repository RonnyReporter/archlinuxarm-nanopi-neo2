This repository can be used to create an ArchLinuxARM image for the NanoPi Neo2
board.


Dependencies
============

- `Debian/Ubuntu based distro`
- `make`
- `bsdtar` (`libarchive`) -- If you get errors writing the image, check if you have v3.3.x or higher.
- `python2`
- `uboot-tools`
- `sudo`
- `fdisk`


Prerequisite
============

In order to build the image, you need a working ARM toolchain.

Here is a simple way to get one:

    apt install gcc-aarch64-linux-gnu g++-aarch64-linux-gnu

Preparing the files
===================

Run `make` (specifying jobs with `-jX` is supported and recommended).

This will provide:

- the ArchLinuxARM aarch64 default rootfs (`ArchLinuxARM-aarch64-latest.tar.gz`)
- an u-boot image compiled for the NanoPi Neo2 (`u-boot-sunxi-with-spl.bin`)
- a boot script (`boot.scr`) to be copied in `/boot`


Building and installing the distribution
========================================

Run `make` to build, be sure to edit your-home-directory.

Then run `make install BLOCK_DEVICE=/dev/mmcblk0` with the appropriate target, either sd card or loop device.

After first boot
===============

After the first boot please run the follow commands, make sure you're connected to a network:

```
pacman-key --init
pacman-key --populate archlinuxarm
pacman -Syu
```

Goodies
=======

If you have a serial cable and `miniterm.py` installed (`python-pyserial`),
`make serial` will open a session with the appropriate settings.
