To test the PBA on your machine you will need the PBA image and a USB stick/thumb drive.

Unzip the PBA
  Linux:  gunzip [BIOS32 | UEFI64].img.gz
  Windows:  Use 7-zip.
Transfer the PBA image to the USB stick.  
  Linux:  dd if=[BIOS32 | UEFI64].img of=/dev/sd?        (/dev/sd? is the USB stick base device node, no number)  
  Windows:  use Win32DiskImager from sourceforge to write the image to the USB stick  

Boot the USB stick, enter "debug" when asked for the passphrase and verify that it scans your system correctly identifying your OPAL disks.  

The output should look something like this:    
    DTA LINUX Pre Boot Authorization   
    Please enter pass-phrase to unlock OPAL drives: *****  
    Scanning....  
    Drive /dev/nvme0 Samsung SSD 960 EVO 250GB                is OPAL NOT LOCKED        
    Drive /dev/sda   Crucial_CT250MX200SSD1                   is OPAL Failed    
    Drive /dev/sdb   Samsung SSD 850 EVO 500GB                is OPAL Failed    
    Drive /dev/sdc   ST500LT025-1DH142                        is OPAL NOT LOCKED     
    Drive /dev/sdd   Samsung SSD 850 EVO 250GB                is OPAL NOT LOCKED     
    Drive /dev/sde   Micron_1100_MTFDDAK256TBN                is OPAL Unlocked   
  
The meaning of the status messages are:  

Status | Description  
------ | -----------  
is OPAL NOT LOCKED | The drive either not locked or has not been set up  
is OPAL Failed | An error occurred during the unlock  
is OPAL Unlocked | The drive was successfully unlocked
NOT OPAL | The drive is not supported  

If the PBA is correctly identifying your drives (a status other than NOT OPAL) then you should be able to use it to unlock them after you have enabled locking on your drive.  If it's not you can open an issue at github and we'll try to determine what is wrong.  I would suggest taking a picture of the screen so you can accurately report what the output was.  You can also login to the system (user root, no password) and look at the extended messages that were stored in /tmp (cat /tmp/pbaerror.log).  

Now its time to test the rescue system.

