
**Warning**  
See the removing OPAL page for instructions on returning the drive to a non-OPAL managed state.  If you just want to turn off the locking and PBA see the steps at the end of this page.

 

Download the host program for [Windows](https://github.com/Drive-Trust-Alliance/exec/blob/master/sedutil_WIN.zip?raw=true) or [Linux](https://github.com/Drive-Trust-Alliance/exec/blob/master/sedutil_LINUX.tgz?raw=true)

Download the PBA for a [BIOS](https://github.com/Drive-Trust-Alliance/exec/blob/master/LINUXPBARelease.img.gz?raw=true) or [64bit UEFI](https://github.com/Drive-Trust-Alliance/exec/blob/master/UEFI64_Release.img.gz?raw=true) machine (UEFI support currently requires that Secure Boot be turned off.)

 

**Optional but highly recommended:**

Test the PBA on your machine

Prepare and test the rescue image

 

**Set up the Drive:**

gunzip the PBA  (Windows users will need to use 7-zip)

sedutil-cli –initialsetup <password> <drive>

 

If the drive is a boot drive:

sedutil-cli –loadPBAimage <password> <pabfilename>  <drive>

sedutil-cli –setMBREnable on <password> <drive>

 

**Enable locking:**

sedutil-cli –enableLockingRange 0 <password> <drive>

 

**<drive> = \\.\PhysicalDrive? on windows and /dev/sd? on Linux

 

Power off the computer to lock the drive.  Power the computer on. The PBA should ask for your password, unlock the drive and chain-load the real OS on the drive you booted from.

 

If you want to turn off Locking and the PBA:

sedutil-cli –disableLockingRange 0 <password> <drive>

sedutil-cli –setMBREnable off <password> <drive>