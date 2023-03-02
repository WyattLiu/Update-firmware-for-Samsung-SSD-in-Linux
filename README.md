# Update-firmware-for-Samsung-SSD-in-Linux
The Samsung 2TB NVME firmware has issues and could render the disk useless by wear them out rapidly and lock in read-only mode. This is a tutorial how to verify and update firmware for Samsung nvme SSDs. There are so many videos about using the GUI on Windows machine, I don't have a time for videos but hope this repo can point you to the right direction.

## Disk of interest
Currently, we know SSD 980 PRO 2TB with Firmware starting with 3 has issue. If you drive is bought in 2021, good chance is your firmware starts with 2 but in general we could just update to 5xxx firmware.

## Verify your issue.
`sudo fwupdmgr get-devices`

From my experience, I could not update with fwupdmgr facilities, to be fair, use smart tools could also verify firmware version but that is kind of verbose

## If you are using 3XXX firmwares, do the following
The firmware is located here; https://semiconductor.samsung.com/consumer-storage/support/tools/

Download the firmware:
`wget https://semiconductor.samsung.com/resources/software-resources/Samsung_SSD_980_PRO_5B2QGXA7.iso`

`sudo mkdir /mnt/iso; chmod 777 -R /mnt/iso`

`sudo mount -o loop ./Samsung_SSD_980_PRO_5B2QGXA7.iso /mnt/iso/`

`mkdir ~/tmp_firmware; cd ~/tmp_firmware`

`gzip -dc /mnt/iso/initrd | cpio -idv --no-absolute-filenames`

`cd root/fumagician/`

`sudo ./fumagician`

Don't run the fumagician.sh... it will run into issues.
Samsung will ask if you backed up your drives which I always recommand doing it via rsync.
Then just yes and yes to update the firmware.

You need to reboot then run `sudo fwupdmgr get-devices` to verify.
