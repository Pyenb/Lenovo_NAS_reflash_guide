<div align="center">

# Lenovo NAS reflash

This repository contains information about Lenovo NAS devices. Specifically, information on how to reflash the firmware on these devices.

<img src="images/banner.png" width="900">

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
- [Additional Information](#additional-information)
  - [USB file structure](#usb-file-structure)
- [Background Information](#background-information)
- [Resources](#resources)
- [Contributing](#contributing)
- [Disclaimer](#disclaimer)

## Lenovo LifeLine Imager download

#### What is the Lenovo LifeLine Imager?

The Lenovo LifeLine Imager is a tool that can create a bootable USB drive that can be used to reflash the firmware on LenovoEMC² NAS devices.

#### How to download the Lenovo LifeLine Imager?

Thanks to a comment under [this post](https://www.petenetlive.com/KB/Article/0001381), here is a guide on how to "construct" the download link for the Lenovo LifeLine Imager, specific to your device.

1. Go to the [Support page for LenovoEMC Network Storage, Lenovo Network Storage, and Iomega products](https://download.lenovo.com/lenovoemc/na/en/index.html).
2. Find your device in the list and open the support page for it.
3. Under `DOWNLOADS AND UPDATES` click on `Firmware Version x.x.x.x for XXXX`.
4. Scroll down to `Update Instructions -> Firmware Update Procedure` and take note of the first step of the instructions.
5. The step should be something like `Download the b4b-4.1.414.34909.tgz file to your computer.`
6. Take note of the filename of the `.tgz` file. (But without the `.tgz` extension!!!)
7. Construct the download link as follows: `https://download.lenovo.com/nasupdate/asgimage/ + filename + .zip` and open it in your browser.
8. You should now be able to download the Lenovo LifeLine Imager, specific to your device and firmware version.
9. The downloaded content should look like this, after extracting the `.zip` file:

<div align="center">

<img src="images/extracted.png" width="600">

</div>

### Table of known Lenovo LifeLine Imager downloads

If I have missed anything or if you have a download link that is not listed here, please open an issue or a pull request.

<div align="center">

#### LenovoEMC

| Device | Firmware Version | Download Link | Note | Version |
| ------ | ---------------- | ------------- | ----- | ------- |
| PX4-400R | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/b4b-4.1.414.34909.zip) | Same for PX4-400D | Rack |
| PX4-300R | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/px4-300r-4.1.414.34909.zip) | | Rack |
| PX12-400R | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/r12b-4.1.414.34909.zip) | Same for PX12-450R | Rack |
| PX4-300D | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/px4px6-4.1.414.34909.zip) | Same for PX6-300D | Desktop |
| PX2-300D | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/b2a-4.1.414.34909.zip) | | Desktop |

#### Lenovo

| Device | Firmware Version | Download Link | Note | Version |
| ------ | ---------------- | ------------- | ----- | ------- |
| IX4-300D | 4.1.414.34909 | [Download](https://download.lenovo.com/nasupdate/asgimage/h4c-4.1.414.34909.zip) |  | Desktop |
| IX2 | 4.1.408.34845 | [Download](https://download.lenovo.com/nasupdate/asgimage/ix2-ng-4.1.408.34845.zip) | Same for IX2-DL | Desktop |

#### Iomega (StorCenter)

| Device | Firmware Version | Download Link | Note | Version |
| ------ | ---------------- | ------------- | ----- | ------- |
| ALL | 4.1.414.34909 | | The download links for the StorCenter devices are the same as for the LenovoEMC² devices | Both |

</div>


If any of these links are broken, please let me know by opening an issue or a pull request. Also you can find the imager tool in the [Releases section](https://github.com/Pyenb/Lenovo_NAS_reflash_guide/releases) of this repository or on my [Storage server](https://data.pyenb.network/Github/Lenovo-NAS-Imager/). I have reuploaded all the files there.

## How to flash the firmware

> [!CAUTION]
> Remove your hard drives before flashing the firmware to prevent data loss! During the flashing process, all connected hard drives will be formatted! (It also helps reduce boot times and gets the flashing done sooner.)

1. Format a USB drive to FAT32. (Needs to be at least 1GB in size, maximum 32GB)
2. Unzip the downloaded Imager file and run the executable file contained within.
3. When prompted, select the USB drive as the destination.
4. Finish the Setup.
5. Check the pendrive has the correct filestructure (See USB file structure below)
6. Eject the USB and insert it into your NAS (in the **top left** port on the backside of the device, acocording to a comment). On Rackmount versions, use the front panel USB socket.
7. Boot the NAS with the USB drive inserted **while** holding the reset button for ~60 seconds or until you see the screen below.
8. You should now see this screen:

<div align="center">

<img src="images/flash.jpg" width="500">

</div>

9. When finished, the device should shut down.
10. Remove the USB.
11. Turn the NAS back on.
12. The device should now boot back up and be ready to be reconfigured.

> [!NOTE]
> On rackmount versions, you can plug in a screen and see the Kernel start, but you will get no confirmation whether the flashback was a success. 
> Three possibilities: 
> A. The pendrive is not recognized, the unit will attempt a normal boot and hang. -> Make sure the pendrive is in the correct USB socket, try another socket.
> B. The pendrive is recognized, you will see GRUB booting the pendrive, if your drive has a LED it will flash as the copying is done, the unit will then, (without any message on VGA display) shut down. Restart the unit, if it hangs again, the pendrive used is not OK for this purpose. -> Try a different pendrive!
> C. The pendrive is recognized, you will see GRUB booting the pendrive, if your drive has a LED it will flash as the copying is done, the unit will then, (without any message on VGA display) shut down. Restart the unit, it boots normally. -> SUCCESS


## Additional Information

- The Lenovo LifeLine Imager is a Windows-only tool.
- The used USB needs to be formatted as FAT32! Otherwise, the NAS won't recognize it.
  > The Imager should format the drive to FAT32 as it's set as such in the image file, but in my case, despite making sure the drive was FAT32 to begin with, it would never correctly write the image file for whatever reason (see workaround below).
- I had to try multiple USB drives until I found one that worked. The NAS recognized all of them and went into the recovery process, but still wouldn't boot after.
  > This may have to do with flashdrive size, despite the partition being sized by the image. Multiple 16GB drives failed to get my PX12-450R to start up successfully. I then tried a cheap old 8GB drive, and the NAS would successfully start after the first attempt. 
- If the Imager tool doesn't recognize the USB drive, try using rufus to reformat the USB drive. Select the drive, then the `Non-bootable` option, select `FAT32` as the file system and `MBR` as the partition scheme. Then press `Start`.

### USB file structure

> [!NOTE]
> The file under `**b_images` is the actual firmware file (** depends on the NAS model). The other files are used for the boot process. If the image file is missing, or if the folder contains junk with abstract characters, re-running the installer will do you no good. For whatever reason the tool corrupts the image file, and it will either not write the file header, or fill the folder with various junk files. (It might work correctly under Windows 7) Read on for a workaround.

The USB drive should have the following structure after running the Imager tool:

```plaintext
USB-DRIVE:.
├───boot
│   └───grub
│       ├───locale
|       └───...
├───images
│   └───...
└───emctools
    └───**b_images
        └───VERSION_Imager.tgz
```
> Workaround if you don't see the .tgz file or have junk in the folder:
> 1. Go to ‪C:\Users\[yourusername]\AppData\Local\LifeLineImager, open folder properties, and under permissions, special permissions, change the erase, and erase subfolders and files permissions to NO.
> 2. Run the imaging tool again, and write the pendrive once more (you might need to delete the pendrive partition manually before it will successfully write the drive again).
> 3. The installer has now left the *.img file for the pendrive in the above folder.
> 4. Use rufus to write the *.img file to the pendrive.
> 5. Congrats, you have achieved what the Lenovo app couldn't, and made a correctly functioning flashback drive.
> 6. Reverse the permissions change and delete the LifeLineImager folder.
> 7. Continue from Step 6 of the flashing guide.
>

## Background Information

I own a LenovoEMC² PX4-400R NAS, which I purchased from eBay. Unfortunately, I bricked the device during the reset process. Fortunately, I was able to recover it using information I found online. After conducting some research, I found posts that could potentially assist **you** in recovering your device too, should you ever find yourself in a similar predicament. I created this repository with the intention of assisting others in the future.

Added info based on experience with a PX12-450R. 

## Resources

> [!NOTE]
> Links marked with ❗ are the most important ones.

❗[PX4-300D Lenovo EMC NAS Device Stuck at 95%](https://www.petenetlive.com/KB/Article/0001381)

❗[Official LenovoEMC, Lenovo, and Iomega network storage support](https://download.lenovo.com/lenovoemc/na/en/app/answers/detail/a_id/14412.html)

[General overview support page](https://download.lenovo.com/lenovoemc/na/en/index.html)

[Help for old Lenovo EMC NAS units, IX2, PX4 etc](https://forums.anandtech.com/threads/help-for-old-lenovo-emc-nas-units-ix2-px4-etc.2609187/)

## Contributing

Contributions to this repository are very welcome! Here's how you can help:

1. **Fork** this repository.
2. **Create a new branch** on your forked repository.
3. **Make your changes**. This could be adding a new device to the table, updating a download link, or improving the instructions.
4. **Submit a pull request**. Make sure to describe your changes in detail.

If you have any questions or need help, feel free to open an issue.

## Disclaimer

Flashing firmware is a potentially risky operation. If done incorrectly, it can result in a bricked device. Please follow the instructions carefully and understand the risks involved. The author of this repository is not responsible for any damage caused by following these instructions.
