To test the PBA on your machine you will need the PBA image and a USB stick/thumb drive.

Unzip the PBA
  Linux:  gunzip [BIOS32 | UEFI64].img.gz
  Windows:  Use 7-zip.
Transfer the PBA image to the USB stick.  
  Linux:  dd if=[BIOS32 | UEFI64].img of=/dev/sd?        (/dev/sd? is the USB stick base device node, no number)  
  Windows:  use Win32DiskImager from sourceforge to write the image to the USB stick  

Boot the USB stick, enter "debug" when asked for the passphrase and verify that it scans your system correctly identifying your OPAL disks.  

The output should look something like this:
******insert new example here******

If the PBA is correctly identifying your drives then you should be able to use it to unlock them after you have enabled locking on your drive.  If it's not you can open an issue at github and we'll try to determine what is wrong.  I would suggest taking a picture of the screen so you can accurately report what the output was.

Now its time to test the rescue system.

