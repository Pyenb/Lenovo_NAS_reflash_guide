# IX2 flash guide
This guide was based on [this guide by Jeroen Baert.](https://www.forceflow.be/2021/09/23/restore-an-iomega-lenovo-storcenter-ix2-without-original-disks/)

## Get the necessary files
The following files are needed:
- initrd
- zImage
- The USB flash tool

The `initrd` and `zImage` files can be found in this folder. The usb flash tool can be found under [releases](https://github.com/Pyenb/Lenovo_NAS_reflash_guide/releases): [(ix2-ng-4.1.408.34845.zip)](/releases/latest/download/ix2-ng-4.1.408.34845.zip)

## Prepare your machine
- To run the flash tool, you will need a windows host OS. I found the tool to work correctly on Windows 11.
- For copying the disk files, you will to run the DD command. I used Debian for this.


## Prepare USB stick
- Format the USB drive to FAT32
-  Run ix2-ng-4.1.408.34845.exe
-  Select the correct drive to write to and let the tool finish

    Note that most instructions mention that the usb tool creates a FAT32 partition. In my experience the tool created a partition that was not readable by Windows.


## Prepare Hard Drive

The tool on the USB drive expects zImage and initrd (two essential startup-related tools) to be in the first few sectors of the disk.

- Connect the drive to a working Linux system (where you have access to the devices under /dev). you could use a live USB for this, or a Raspberry PI.
- Copy zImage and initrd to that system.
- Copy them, byte by byte, to the hard disk. Double check which disk you’re copying to! It might (and probably won’t) be at /dev/sda for you! Writing to the wrong disk might render your system unbootable.

`sudo dd if=./zImage of=/dev/sda seek=2048`
`sudo dd if=./initrd of=/dev/sda seek=8192`

## Reset Storcenter ix2
- Mount the prepared hard disk into the first bay of the Storcenter ix2
- Plug in the prepared USB stick into the Storcenter ix2
- Hold the reset button on the back of the device down (using a paperclip or pencil) and hold it for a minute, or until the USB stick's activity light (if you have it) turns on.
- While doing that, insert the power adapter
- The Storcenter will start resetting the device. (You can probably hear the hard disk head moving). If your USB stick has an activity light, it will flash.
- Wait until the Storcenter shuts itself down
- Remove the USB stick
- Plug in the ethernet cable
- Turn on the device

And this should get your device back in a functioning state. Now remember, the management software is installed on that first disk. Don’t remove that first disk without adding a second one, or you’re back to square one.
