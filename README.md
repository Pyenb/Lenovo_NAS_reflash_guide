<div align="center">

# Lenovo NAS Reflash

This repository contains information about Lenovo NAS devices. Specifically, information on how to reflash the firmware on these devices.

</div>

## Table of Contents

- [Lenovo LifeLine Imager download](#lenovo-lifeline-imager-download)
  - [What is the Lenovo LifeLine Imager](#what-is-the-lenovo-lifeline-imager)
  - [How to download the Lenovo LifeLine Imager?](#how-to-download-the-lenovo-lifeline-imager)
  - [Table of known Lenovo LifeLine Imager downloads](#table-of-known-lenovo-lifeline-imager-downloads)
    - [LenovoEMC](#lenovoemc)
    - [Lenovo](#lenovo)
    - [Iomega (StorCenter)](#iomega-storcenter)
- [How to flash the firmware](#how-to-flash-the-firmware)
- [Resources](#resources)

## Lenovo LifeLine Imager download

#### What is the Lenovo LifeLine Imager?

The Lenovo LifeLine Imager is a tool that can create a bootable USB drive that can be used to reflash the firmware on LenovoEMC² NAS devices.

#### How to download the Lenovo LifeLine Imager?

Thanks to a comment under [this post](https://www.petenetlive.com/KB/Article/0001381), here is a guide on how to "consruct" the download link for the Lenovo LifeLine Imager, specific to your device.

1. Go to the [LenovoEMC² Support Page](https://download.lenovo.com/lenovoemc/na/en/index.html).
2. Find your device in the list and open the support page for it.
3. Under `DOWNLOADS AND UPDATES` click on `Firmware Version x.x.x.x for XXXX`.
4. Scroll down to `Update Instructions -> Firmware Update Procedure` and take note of the first step of the instructions.
5. The step should be something like `Download the b4b-4.1.414.34909.tgz file to your computer.`
6. Take note of the filename of the `.tgz` file. (But without the `.tgz` extension!!!)
7. Construct the download link as follows: `https://download.lenovo.com/nasupdate/asgimage/ + filename + .zip` and open it in your browser.
8. You should now be able to download the Lenovo LifeLine Imager, specific to your device and firmware version.
(9.) The downloaded content should look like this, after extracting the `.zip` file:

<div align="center">

<img src="images/extracted.png" width="600">

</div>

#### Table of known Lenovo LifeLine Imager downloads

Feel free to add your device and firmware version to the table below using a PR.

##### LenovoEMC

| Device | Firmware Version | Download Link | Notes | Version |
| ------ | ---------------- | ------------- | ----- | ------- |
| PX4-400R | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/b4b-4.1.414.34909.zip) | Same for PX4-400D | Rack |
| PX4-300R | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/px4-300r-4.1.414.34909.zip) | | Rack |
| PX12-400R | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/r12b-4.1.414.34909.zip) | Same for PX12-450R | Rack |
| PX4-300D | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/px4px6-4.1.414.34909.zip) | Same for PX6-300D | Desktop |
| PX2-300D | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/b2a-4.1.414.34909.zip) | | Desktop |

##### Lenovo

| Device | Firmware Version | Download Link | Notes | Version |
| ------ | ---------------- | ------------- | ----- | ------- |
| IX4-300D | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/h4c-4.1.414.34909.zip) |  | Desktop |
| IX2 | 4.1.408.34845 | [Download](https://download.lenovo.com/nasupdate/asgimage/ix2-ng-4.1.408.34845.zip) | Same for IX2-DL | Desktop |

##### Iomega (StorCenter)

| Device | Firmware Version | Download Link | Notes | Version |
| ------ | ---------------- | ------------- | ----- | ------- |
| ALL | 4.1.414.34909 | | The download links for the StorCenter devices are the same as for the LenovoEMC² devices | Both |

## How to flash the firmware

> [!WARNING]
> Remove your hard drives before flashing the firmware to prevent data loss! During the flashing process, all connected hard drives will be formatted!

1. Format a USB drive to FAT32.
2. Unzip the downloaded Imager file and run the executable file contained within.
3. When prompted, select the USB drive as the destination.
4. Reboot the NAS with the USB drive inserted **and** hold the reset button for 60 seconds.
5. You should now see this screen:

<div align="center">

<img src="images/flash.jpg" width="500">

</div>

6. When finished, the device should shut down, simply power it back on.
7. The device should now boot back up and be ready to be reconfigured.

## Background Information

I own an LenovoEMC² PX4-400R NAS that I got from ebay. Sadly during resetting the device, I bricked it. I was **not** able to recover it yet. But after lots of research, I found some forum posts that might help you recover your device, if you ever find yourself in a similar situation. I decided to create this repository to help others in the future.

## Resources

❗[PX4-300D Lenovo EMC NAS Device Stuck at 95%](https://www.petenetlive.com/KB/Article/0001381)

[Help for old Lenovo EMC NAS units, IX2, PX4 etc](https://forums.anandtech.com/threads/help-for-old-lenovo-emc-nas-units-ix2-px4-etc.2609187/)
