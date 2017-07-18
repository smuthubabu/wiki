# These instructions are for the legacy bios PBA (biosbpa.img)

To test the PBA on your machine you will need the PBA image and a USB stick/thumb drive.

Transfer the PBA image to the USB stick.
Linux: dd if=biospba-.img of=/dev/sd? (/dev/sd? is the USB stick base device node, no number)
Windows: use Win32DiskImager from sourceforge to write the image to the USB stick

Boot the USB stick, enter anything when asked for the passphrase and verify that it scans your system correctly identifying your OPAL disks. After it has scanned the PCI bus for AHCI controllers and the AHCI controllers for SATA drives that conform to the OPAL spec it will chain-load itself and ask for the passphrase again so don't panic when the test zooms by.

The output should look something like this:

Msed PBA for BIOS machines

Enter Pass Phrase to unlock OPAL SSC drives>*****
Found device Crucial_CT120M500SSD3 is OPAL Not Locked
Found Device Samsung SSD 850 EVO 500GB is OPAL Not Locked
Found Device Hitachi HDT725040VLA360 Not OPAL

About to Chainload hd0,0

Msed PBA for BIOS machines

Enter Pass Phrase to unlock OPAL SSC drives>

If the PBA is correctly identifying your drives then you should be able to use it to unlock them after you have enabled locking on your drive. If it's not you can open an issue at github and we'll try to determine what is wrong. I would suggest taking a picture of the screen so you can accurately report what the output was.

Now its time to test the rescue system.
