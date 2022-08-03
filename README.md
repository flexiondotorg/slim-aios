# Slim.AI OS

Optimised OS for the Raspberry Pi for creating and running containers 🐋. Based
on Ubuntu, but **not** Ubuntu, includes *"Just Enough OS"*,
[Docker Engine](https://docs.docker.com/engine/install/ubuntu/),
[DockerSlim](https://dockersl.im) and [Dropbear](https://github.com/mkj/dropbear).

This repository hosts downloadable images of Slim.AI OS and the script that
builds Slim.AI OS images for Raspberry Pi devices.
## Features

  * Optimized images for Raspberry Pi 2, 3, 4 and 400.
  * Based on [Ubuntu](https://ubuntu.com), [Docker Engine](https://docs.docker.com/engine/install/ubuntu/) and [DockerSlim](https://dockersl.im)
  * Supported Raspberry Pi models:
    * Raspberry Pi Compute Module 3 Lite
    * Raspberry Pi Compute Module 4 Lite
    * Raspberry Pi 2 Model B
    * Raspberry Pi 3 Model A+
    * Raspberry Pi 3 Model B
    * Raspberry Pi 3 Model B+
    * Raspberry Pi 4 Model B  (**Recommended**)
    * Raspberry Pi 400
    * Raspberry Pi Zero 2 W
  * Boot from USB
  * Automatic first boot file system expansion

## Downloads

Alpha images of Slim.AI OS are [available for download from the GitHub releases](https://github.com/flexiondotorg/slim-aios/releases).

### Putting Slim.AI OS on a Raspberry Pi

  * [Download Slim.AI OS](https://github.com/flexiondotorg/slim-aios/releases)
  * Use [Raspberry Pi Imager](https://www.raspberrypi.com/software/) to put the image on microSD card.
  * Select **Use custom** from the Operating System drop down
  * Select the target microSD card or USB drive.
  * Click **Write**
## Building Images

  * Clone the Slim.AI OS project
    * `git clone https://github.com/flexiondotorg/slim-aios.git`

It is best to run the `slim-aios-image` on an Ubuntu 22.04 x86 64-bit
workstation, ideally running in a VM via [Quickemu](https://github.com/quickemu-project/quickemu).
If using a fresh [Quickemu](https://github.com/quickemu-project/quickemu) VM you will need to set the `disk_size` parameter large enough to complete the build (around 26G). This can be achieved by adding `disk_size="32G"` to `ubuntu-jammy.conf` before running `quickemu` to create the VM. Alternatively you could mount external storage into the container for the build area. You'll also need at to `sudo apt install git`.

The following incantation will build a Slim.AI OS arm64 image for Raspberry Pi.
You can replace `arm64` with `armhf` to build an image for 32-bit ARM.

```bash
sudo ./slim-aios-image --arch arm64
```

You can tweak some variables towards the bottom of the `slim-aios-image` script.

```bash
IMG_VER="22.04"
IMG_RELEASE="jammy"
```

### What is the default username and password:

This is the default username and password for logging into Retro Home via SSH
or the desktop.

  * Username: `slimdevops`
  * Password: `slimai`

### Kernel headers

If you need to build kernel modules you can install the kernel header for the
Raspberry Pi kernel like so:

```bash
sudo apt-get install linux-headers-raspi
```

## Reference

### GPIO

As of Linux kernel 5.11, the old methods of communicating with the header pins
on the Raspberry Pi will no longer work. This means that packages such as
RPi.GPIO will no longer function properly with newer kernels.

  * [The Pins They Are A-Changin’](https://waldorf.waveform.org.uk/2021/the-pins-they-are-a-changin.html)
  * [The lg archive](http://abyz.me.uk/lg/)
    * lg is an archive of programs for Linux Single Board Computers which allows control of the General Purpose Input Outputs.
  * [Raspberry Pi GPIO Tutorial](https://blogjawn.stufftoread.com/raspberry-pi-gpio-tutorial.html)
