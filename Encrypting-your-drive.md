```
**Note to users of non us_english keyboards**
Both the PBA and rescue systems use the us_english keyboard.  This can cause issues 
when setting the password on your normal operating system if you use another 
keyboard mapping.  To make sure the PBA recognizes your password you are encouraged
to set up you drive from the rescue system as described on this page.
```  
  
Download and prepare the rescue system for a [BIOS](https://github.com/Drive-Trust-Alliance/exec/blob/master/RESCUE32.img.gz?raw=true) or [64bit UEFI](https://github.com/Drive-Trust-Alliance/exec/blob/master/RESCUE64.img.gz?raw=true) machine (UEFI support currently requires that Secure Boot be turned off.)  

  Decompress the Rescue system:  (Windows users will need to use 7-zip)      
     `gunzip RESCUE32.img.gz`    
       --or--  
     `gunzip RESCUE64.img.gz`  

  Transfer the Rescue image to the USB stick.

  Linux:  dd if=RESCUE32.img of=/dev/sd?     (/dev/sd? is the USB stick base device node, no number)  
               --or--  
        dd if=RESCUE64.img of=/dev/sd?   
  Windows:  use Win32DiskImager from sourceforge to write the image to the USB stick
  
Boot the USB thumb drive with the rescue system on it.
You will see the Login prompt, enter "root" there is no password so you will get a root shell prompt

Test sedutil by entering the command `sedutil-cli --scan`  
Expected Output:    
```
#sedutil-cli --scan
Scanning for Opal compliant disks
/dev/nvme0  2  Samsung SSD 960 EVO 250GB                2B7QCXE7
/dev/sda    2  Crucial_CT250MX200SSD1                   MU04    
/dev/sdb   12  Samsung SSD 850 EVO 500GB                EMT01B6Q
/dev/sdc    2  ST500LT025-1DH142                        0001SDM7
/dev/sdd   12  Samsung SSD 850 EVO 250GB                EMT01B6Q
No more disks present ending scan

```

Verify that your drive has a 2 in the second column indicating OPAL 2 support.
If it doesn't **do not proceed**, there is something that is preventing sedutil from
supporting your drive.  If you continue you may **erase all of your data**

Test the PBA by entering the command `linuxpba` and entering a pass-phrase of `debug`. If you don't use debug as the pass-phrase your system will reboot!   
Expected Output:  
```
#linuxpba 
DTA LINUX Pre Boot Authorization 


Please enter pass-phrase to unlock OPAL drives: *****
Scanning....
Drive /dev/nvme0 Samsung SSD 960 EVO 250GB                is OPAL NOT LOCKED   
Drive /dev/sda   Crucial_CT250MX200SSD1                   is OPAL NOT LOCKED   
Drive /dev/sdb   Samsung SSD 850 EVO 500GB                is OPAL NOT LOCKED   
Drive /dev/sdc   ST500LT025-1DH142                        is OPAL NOT LOCKED   
Drive /dev/sdd   Samsung SSD 850 EVO 250GB                is OPAL NOT LOCKED   
```
Verify that Your drive is listed and the that the PBA reports it as \"is OPAL\"  
  
**Issuing the commands in the steps that follow will enable OPAL locking.  If you have a problem you will need to follow the steps at the end of this page to either disable or remove OPAL locking**  
  

**The following steps use /dev/sdc as the device and UEFI64-1.15.img.gz for the PBA image, substitute the proper /dev/sd? for your drive and the proper PBA name for your system** 
   
Enable locking and the PBA by issuing these commands:  **(Use the password of `debug` for this test, it will be changed later)**  
`sedutil-cli --initialsetup debug /dev/sdc`  
`sedutil-cli --enablelockingrange 0 debug /dev/sdc`  
`sedutil-cli --setlockingrange 0 lk debug /dev/sdc`  
`sedutil-cli --setmbrdone off debug /dev/sdc`    
`gunzip /usr/sedutil/UEFI64-n.nn.img.gz` <-- Replace n.nn with the release number.    
`sedutil-cli --loadpbaimage debug /usr/sedutil/UEFI64-n.nn.img /dev/sdc` <-- Replace n.nn with the release number.      


Expected Output:  
```
#sedutil-cli --initialsetup debug /dev/sdc
- 14:06:39.709 INFO: takeOwnership complete
- 14:06:41.703 INFO: Locking SP Activate Complete
- 14:06:42.317 INFO: LockingRange0 disabled 
- 14:06:42.694 INFO: LockingRange0 set to RW
- 14:06:43.171 INFO: MBRDone set on 
- 14:06:43.515 INFO: MBRDone set on 
- 14:06:43.904 INFO: MBREnable set on 
- 14:06:43.904 INFO: Initial setup of TPer complete on /dev/sdc
#sedutil-cli --enablelockingrange 0 debug /dev/sdc
- 14:07:24.914 INFO: LockingRange0 enabled ReadLocking,WriteLocking
#sedutil-cli --setlockingrange 0 lk debug /dev/sdc
- 14:07:46.728 INFO: LockingRange0 set to LK
#sedutil-cli --setmbrdone off debug /dev/sdc
- 14:08:21.999 INFO: MBRDone set off 
#gunzip /usr/sedutil/UEFI64-1.15.img.gz 
#sedutil-cli --loadpbaimage debug /usr/sedutil/UEFI64-1.15.img /dev/sdc
- 14:10:55.328 INFO: Writing PBA to /dev/sdc
33554432 of 33554432 100% blk=1500 
- 14:14:04.499 INFO: PBA image  /usr/sedutil/UEFI64.img written to /dev/sdc
#
```
Test the PBA (yes again) by entering the command `linuxpba` and entering a pass-phrase of `debug`  
This second test will verify that your drive really does get unlocked.  
Expected Output:  
```
#linuxpba 

DTA LINUX Pre Boot Authorization 


Please enter pass-phrase to unlock OPAL drives: *****
Scanning....
Drive /dev/nvme0 Samsung SSD 960 EVO 250GB                is OPAL NOT LOCKED   
Drive /dev/sda   Crucial_CT250MX200SSD1                   is OPAL NOT LOCKED   
Drive /dev/sdb   Samsung SSD 850 EVO 500GB                is OPAL NOT LOCKED   
Drive /dev/sdc   ST500LT025-1DH142                        is OPAL Unlocked   <--- IMPORTANT!!   
Drive /dev/sdd   Samsung SSD 850 EVO 250GB                is OPAL NOT LOCKED   

```
Verify that the PBA unlocks your drive, it should say "is OPAL Unlocked"
If it doesn't then you will need to follow the steps at the end of this page to either remove OPAL or disable locking.

Set a real password.  The SID and Admin1 passwords do not have to match but it makes things easier.  
`sedutil-cli --setsidpassword debug yourrealpassword /dev/sdc`  
`sedutil-cli --setadmin1pwd  debug yourrealpassword /dev/sdc`    

Expected Output:  
```
#sedutil-cli --setsidpassword debug yourrealpassword /dev/sdc
#sedutil-cli --setadmin1pwd  debug yourrealpassword /dev/sdc
- 14:20:53.352 INFO: Admin1 password changed
```

Make sure you didn't mistype your password by testing it.  
`sedutil-cli --setmbrdone on yourrealpassword /dev/sdc`  
Expected Output:  
```
#sedutil-cli --setmbrdone on yourrealpassword /dev/sdc
- 14:22:21.590 INFO: MBRDone set on 
```
  
You have now set up your system to use OPAL encryption and locking.  
You now need to **COMPLETLY POWER DOWN YOUR SYSTEM**  
This will lock the drive so that when you restart your system it will boot the PBA.  


If there is an issue after enabling locking you can either disable locking or remove OPAL to continue using your drive without locking.

**If you want to disable Locking and the PBA:**

    sedutil-cli -–disableLockingRange 0 <password> <drive>  
    sedutil-cli –-setMBREnable off <password> <drive>
Expected Output:  
```
#sedutil-cli --disablelockingrange 0 debug /dev/sdc
- 14:07:24.914 INFO: LockingRange0 disabled 
#sedutil-cli --setmbrenable off debug /dev/sdc
- 14:08:21.999 INFO: MBREnable set off 

```

  You can re-enable locking and the PBA using this command sequence  

    sedutil-cli -–enableLockingRange 0 <password> <drive>      
    sedutil-cli –-setMBREnable on <password> <drive>  
Expected Output:  
```
#sedutil-cli --enablelockingrange 0 debug /dev/sdc
- 14:07:24.914 INFO: LockingRange0 enabled ReadLocking,WriteLocking
#sedutil-cli --setmbrenable on debug /dev/sdc
- 14:08:21.999 INFO: MBREnable set on 
```  
  
**Some OPAL drives have a firmware bug that will erase all of your data if you issue the commands below.  See [remove opal](https://github.com/Drive-Trust-Alliance/sedutil/wiki/Remove-OPAL) for a list of drive/firmware pairs that is know to have been tested.**  
To remove OPAL issue these commands:  
`sedutil-cli --revertnoerase <password> <drive>`  
`sedutil-cli --reverttper <password> <drive> `  
Expected Output:  
```
#sedutil-cli --revertnoerase debug /dev/sdc
- 14:22:47.060 INFO: Revert LockingSP complete
#sedutil-cli --reverttper debug /dev/sdc
- 14:23:13.968 INFO: revertTper completed successfully
#
```
