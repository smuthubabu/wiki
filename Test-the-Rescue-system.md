To test the Rescue image on your machine you will need the Rescue image and a USB stick/thumb drive.

Print out a copy of this page and the [Encrypting Page](https://github.com/Drive-Trust-Alliance/sedutil/wiki/Encrypting-your-drive) for reference.

Download the [Rescue Image](https://github.com/Drive-Trust-Alliance/exec/blob/master/RESCUE32.img.gz?raw=true)

     gunzip RESCUE32.img.gz  (windows users will need to use 7-zip)

Transfer the Rescue image to the USB stick.

Linux:  dd if=RESCUE32.img.gz of=/dev/sd?     (/dev/sd? is the USB stick base device node, no number)  
Windows:  use Win32DiskImager from sourceforge to write the image to the USB stick

 

Boot the USB stick, you should be booted into a linux system.  Login as root, there is no password. The image is a Linux system that contains sedutil-cli, linuxpba, BIOS32-x.xx.img.gz and UEFI64-x.xx.img.gz.   When you get the root prompt enter:

    #sedutil-cli –-scan
    #sedutil-cli –-query /dev/sda <== chose an OPAL compliant device

You should see output similar to the [example output](https://github.com/Drive-Trust-Alliance/sedutil/wiki/Sample-Output).

You can either activate the locking while running on the rescue disk or reboot and activate it on your real OS.

It is recommended that you keep a copy of the rescue disk and a printout of the managing page available until you are comfortable that sedutil is functioning well on your system.
