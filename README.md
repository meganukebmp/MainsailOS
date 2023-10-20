# MainsailOS for the OrangePi Zero 3
There are very few differences between the OrangePi Zero 2 and Zero 3. Different power controller, ethernet and DRAM. As such support for the Zero 3 only really needs an armbian build. As this board is not officially supported by armbian (yet), but the orangepi OS (debian based) is simply an armbian fork, it's rudimentary to build this with just the Zero 2 config.

There are 4 versions of the Orange Pi Zero 3: **1GB, 1.5GB, 2GB & 4GB**.

The **1.5GB** is the odd one out. As it appears to have a 2GB chip layout but without all banks filled actually populated. It appears that OrangePi have not found a way to detect this in runtime in the bootloader so it ends up with a different bootloader. To make this simple, I've just made builds for both, even though the only difference is the bootloader.

**If you have a 1GB, 2GB or 4GB model use the regular build**.
**If you have the 1.5GB model use the 1.5GB build**

To build this from scratch you must first compile orangepi's fork of armbian. There is a guide on how to do this in the manual, which you can get here: http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/service-and-support/Orange-Pi-Zero-3.html. **MINIMAL BUILD DOES NOT WORK FOR MAINSAIL!**

After you've built your image you can put it in `src/image/` and edit `src/config` with your image name. To build

```bash
git clone https://github.com/guysoft/CustomPiOS.git
git clone https://github.com/meganukebmp/MainsailOS.git
# cp <my_compiled_armbian_image> MainsailOS/src/image
# edit MainsailOS/src/config with filename
cd MainsailOS/src
../../CustomPiOS/src/update-custompios-paths
sudo modprobe loop
sudo bash -x ./build_dist
```

Images are available under releases

---

![downloads](https://img.shields.io/github/downloads/mainsail-crew/MainsailOS/total)
[![discord](https://img.shields.io/discord/758059413700345988?color=%235865F2&label=discord&logo=discord&logoColor=white&style=flat)](https://discord.gg/mainsail)

<p align="center">
<img src=".github/sdcard-logo.png" style="width:40%" >
</p>

# MainsailOS

A [Raspberry Pi OS](https://www.raspberrypi.org/software/) based distribution for 3D Printers. \
It includes everything to get started with Klipper Firmware and Mainsail.

Learn more about:

-   [Klipper Firmware](https://www.klipper3d.org/)
-   [Moonraker](https://moonraker.readthedocs.io/en/latest/)
-   [Mainsail](https://docs.mainsail.xyz/)

## How to install MainsailOS ?

You can find detailed instructions in our [documentation](https://docs-os.mainsail.xyz).

We recommend the installation via [Raspberry Pi Imager](https://docs-os.mainsail.xyz/getting-started/raspberry-pi-os-based).

## How to get help?

Please join us on [Discord](https://discord.gg/mainsail), if you need additional help.

[![discord](https://img.shields.io/discord/758059413700345988?color=%235865F2&label=discord&logo=discord&logoColor=white&style=flat)](https://discord.gg/mainsail)

Also see the [FAQ](#faq) section.

## What is included?

Here a list of included and preinstalled Software:

-   [Klipper (3D Printer Firmware)](https://github.com/Klipper3d/klipper)
-   [Moonraker (API Web Server for Klipper)](https://github.com/Arksine/moonraker)
-   [Mainsail (Web interface for Klipper/Moonraker)](https://github.com/mainsail-crew/mainsail)
-   [Crowsnest (Webcam streaming)](https://github.com/mainsail-crew/crowsnest)
-   [Sonar (Keepalive daemon)](https://github.com/mainsail-crew/sonar)
-   [Nginx (Webserver & Proxy)](https://nginx.org/en/)

## also includes

-   Enabled Serial Connection by default. \
    Using Hardware UART (PL011) for Boards like BTT SKR Mini E3 V3
-   Preinstalled Dependencies for Klipper's Input Shaper. \
    You only need to build the [klipper_mcu](https://www.klipper3d.org/RPi_microcontroller.html) and installing the service. \
    See [Klipper documentation](https://www.klipper3d.org/Measuring_Resonances.html) for more information.
-   Preinstalled python3-serial package, needed for [CanBoot](https://github.com/Arksine/CanBoot)

## Screenshots

![screenshot-dashboard](https://github.com/mainsail-crew/docs/raw/master/assets/img/screenshot.png)

# FAQ

**Q:** How do I report a Bug?
**A:** First of all make sure it is _not_ an misconfiguration of

-   moonraker
-   klipper
-   crowsnest
-   sonar

If there is a bug that belongs to the OS itself,
please look first at the official Forum of Raspberry Pi OS.\
MainsailOS is based on Raspberry Pi OS and is only slightly modified to\
carry the basics to run Klipper on your 3D Printer.
Most configuration of the single components is up to you.
We only want to provide an Image as a starting point.

If there is something that is a bug caused due to the misconfiguration of MainsailOS itself, please let us know, and we will take action as soon as possible.
Please use the issue section for that.
Please provide as much information as you can.

**Q:** What is the philosophy behind MainsailOS?
**A:** KISS - Keep it simple and stupid.\
We only do a bit of modification. All other documented things of the Raspberry Foundation apply.

And that's our main goal of staying compatible with existing documentation.
We will provide documentation if something is handled differently than the original documentation.

**Q:** How do I contribute/support?
**A:** There are several ways to contribute or support our work.
Please take a closer look to [CONTRIBUTING.md](https://github.com/mainsail-crew/MainsailOS/blob/develop/CONTRIBUTING.md)

# Build your own / Developing

To prevent you have to deal with an entire build chain setup, \
simply fork this repository.

Enable the workflows in your fork and you are good to go. \
On each push you make, an image is build and uploaded as an artifact.

If you want or need to build locally please visit [CustomPiOS](https://github.com/guysoft/CustomPiOS). \
Especially ["Build a Distro From within Raspbian / Debian / Ubuntu / CustomPiOS Distros"](https://github.com/guysoft/CustomPiOS#build-a-distro-from-within-raspbian--debian--ubuntu--custompios-distros)
