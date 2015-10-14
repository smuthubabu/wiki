To test the Rescue image on your machine you will need the Rescue image and a USB stick/thumb drive.

Print out a copy of this page and the Encrypting Page for reference.

Download the Rescue Image

     gunzip <rescuefile>  (windows users will need to use 7-zip)

Transfer the Rescue image to the USB stick.

Linux:  dd if=<rescuefile.img> of=/dev/sd?     (/dev/sd? is the USB stick base device node, no number)
Windows:  use Win32DiskImager from sourceforge to write the image to the USB stick

 

Boot the USB stick, you should be booted into a linux root shell.  The image is a TinyCore Linux image that has been remastered to include sedutil.   When you get the root prompt enter:

    sedutil-cli –scan
    sedutil-cli –query /dev/sda <== chose an OPAL compliant device

You should see output similar to the example output.

You can either activate the locking while running on the rescue disk or reboot and activate it on your real OS.

It is recommended that you keep a copy of the rescue disk and a printout of the managing page available until you are comfortable that msed is functioning well on your system.
