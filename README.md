# Java on openwrt

### Build an RPI 4 openwrt image with included java (openjdk)

I was inspired by the post [Apparently Yes! You can install OpenJDK (Java) JRE and YaCy on OpenWrt](https://dev.to/reinhart1010/apparently-yes-you-can-install-openjdk-java-jre-and-yacy-on-openwrt-1e33) to make an automated script to build an Openwrt java capable image using [Openwrt's Imagebuilder](https://openwrt.org/docs/guide-user/additional-software/imagebuilder) and the java ARM packages from the [Alpine Linux](https://www.alpinelinux.org/) distribution.

But in contrast to the post the script install's OpenJDK-17 and it builds a larger root filesystem so there is no need for a Extroot overlay. Other versions then OpenJDK-17 should be installable too. The Alpine distro includes versions 7 to 17.

__Note__: Although the current build is meant for RPI 4 it should be usable on any Openwrt capable device running an aarch64 ARM processor and ~500MB of storage. I've tested on Raspberry Pi 4 Model B and Raspberry Pi Compute Module 4 (with eMMC flash).

### Build environment

Please see [Using the Image Builder](https://openwrt.org/docs/guide-user/additional-software/imagebuilder#using_the_image_builder) for build requirements.

### Using

```shell
git clone git@github.com:KJersin/rpi4-openwrt-java.git
cd rpi4-openwrt-java
./build-image
```

__Image location__: `imagebuilder/bin/targets/bcm27xx/bcm2711`

Once booted you should be able to run java from a prompt:  
```shell
java -version
```  
and get an output similar to:  
```
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-alpine-r0)
OpenJDK 64-Bit Server VM (build 17.0.8+7-alpine-r0, mixed mode, sharing)
```

### Build options  
```
Usage: ./build-image [options]
Options:
  -p PROFILE              [server|router] (default: router)
                          server: dhcp will be used for IP allocation
                          router: standard out-of-the-box Openwrt settings
  -r ROOT_DEV             Root file systems device (default: /dev/mmcblk0p2)
                          /dev/mmcblk0p2 : sd-card or eMMC
                          /dev/sda2      : usb disk
```