```
**Note to users of non us_english keyboards**
Both the PBA and rescue systems use the us_english keyboard.  This can cause issues 
when setting the password on your normal operating system if you use another 
keyboard mapping.  To make sure the PBA recognizes your password you are encouraged
to set up you drive from the rescue system.
```
**Warning**  
See the [Remove OPAL](https://github.com/Drive-Trust-Alliance/sedutil/wiki/Remove-OPAL) page for instructions on returning the drive to a non-OPAL managed state.  If you just want to turn off the locking and PBA see the steps at the end of this page.

 

Download the host program for [Windows](https://github.com/Drive-Trust-Alliance/exec/blob/master/sedutil_WIN.zip?raw=true) or [Linux](https://github.com/Drive-Trust-Alliance/exec/blob/master/sedutil_LINUX.tgz?raw=true)

Download the PBA for a [BIOS](https://github.com/Drive-Trust-Alliance/exec/blob/master/BIOS32.img.gz?raw=true) or [64bit UEFI](https://github.com/Drive-Trust-Alliance/exec/blob/master/UEFI64.img.gz?raw=true) machine (UEFI support currently requires that Secure Boot be turned off.)

 

**Optional but highly recommended:**

[Test the PBA on your machine](https://github.com/Drive-Trust-Alliance/sedutil/wiki/Test-the-PBA)

[Prepare and test the rescue image](https://github.com/Drive-Trust-Alliance/sedutil/wiki/Test-the-Rescue-system)

 

**Set up the Drive:**

    gunzip the PBA  (Windows users will need to use 7-zip)
    sedutil-cli  -–initialsetup <password> <drive>

If the drive is a boot drive:

    sedutil-cli –-loadPBAimage <password> <pbafilename>  <drive>
    sedutil-cli –-setMBREnable on <password> <drive>

**Enable locking:**

    sedutil-cli –-enableLockingRange 0 <password> <drive>

**<drive> = \\.\PhysicalDrive? on windows and /dev/sd? on Linux

Power off the computer to lock the drive.  Power the computer on. The PBA should ask for your password, unlock the drive and reboot the machine.

**If you want to turn off Locking and the PBA:**

    sedutil-cli -–disableLockingRange 0 <password> <drive>  
    sedutil-cli –-setMBREnable off <password> <drive>

  You can re-enable locking and the PBA using this command sequence  

    sedutil-cli -–enableLockingRange 0 <password> <drive>    
    sedutil-cli –-setMBRDone on <password> <drive>  
    sedutil-cli –-setMBREnable on <password> <drive>