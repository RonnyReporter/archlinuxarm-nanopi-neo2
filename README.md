This repository can be used to create an ArchLinuxARM image for the NanoPi Neo2
board.


Dependencies
============

- `make`
- `bsdtar` (`libarchive`) -- If you get any errors writing make sure you have version 3.3.x or higher.
- `python2`
- `uboot-tools`
- `sudo`
- `fdisk`


Prerequisite
============

In order to build the image, you need a working ARM toolchain.

Here is a simple way to get one:

    git clone https://github.com/crosstool-ng/crosstool-ng
    cd crosstool-ng
    ./bootstrap
    ./configure --enable-local
    make
    ./ct-ng aarch64-unknown-linux-gnu
    ./ct-ng build
    ./ct-ng build install
    
This will install in ~/x-tools, make sure you have the `bin` directory in your path, see below.


Preparing the files
===================

Run `make` (specifying jobs with `-jX` is supported and recommended).

This will provide:

- the ArchLinuxARM aarch64 default rootfs (`ArchLinuxARM-aarch64-latest.tar.gz`)
- an u-boot image compiled for the NanoPi Neo2 (`u-boot-sunxi-with-spl.bin`)
- a boot script (`boot.scr`) to be copied in `/boot`


Building and installing the distribution
========================================

Run `PATH=$PATH:/home/your-home-directory/x-tools/aarch64-unknown-linux-gnu/bin make` to build, be sure to edit your-home-directory.

Then run `make install BLOCK_DEVICE=/dev/mmcblk0` with the appropriate value for
`BLOCK_DEVICE`.

This is running commands similar to [any other AllWinner ArchLinuxARM
installation][alarm-allwinner].

[alarm-allwinner]: https://archlinuxarm.org/platforms/armv7/allwinner/.

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


TODO
====

- clarify crosstool-ng process
- upstream to ArchLinuxARM
