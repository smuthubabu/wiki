**Warning:**
**This function will erase all of your data** if the Locking SP is active, if you want to keep the data protected by the global locking range then you should perform a the Remove OPAL procedure if you have the Admin1 password.

The PSID revert function is useful if a third-party application or your OS has locked your drive and you are no longer able to access it because of some failure.  It allows you to regain the use of the drive but all of the data on the drive will be erased.  This should only be used if you have exhausted all other recovery methods.

The PSID is a 32 character password that can be used to prove you have physical access to the drive.  It is printed on the drive label.  Here is a [picture](http://www.tweaktown.com/image.php?image=imagescdn.tweaktown.com/content/6/7/6714_10_samsung_850_pro_256gb_ssd_review_full.jpg) of the PSID printed on a Samsung 850 PRO.

 

These steps should allow you use your drive again:

1. sedutil-cli -–scan <- SCAN to find Opal Drive (you should a 1 or 2 next the the drive)
2. sedutil-cli -–query \\.\PhysicalDrive? <–this will show the Opal status
         look at the locking  feature and see if it is Locked = Y  or LockingEnabled = Y
         that’s a good sign that this should work

3. sedutil-cli -–yesIreallywanttoERASEALLmydatausingthePSID <YOURPSID> \\.\PhysicalDrive?
4. You should see INFO: revertTper completed successfully.

If you get a message that says NOT_AUTHORIZED you entered the PSID incorrectly.
If it doesn’t work please execute the command in step 3 with a -vvvvv (5 v’s) as the first option and
redirect the output to a file and open an issue on GitHub.

example:

sedutil-cli -vvvvv –-yesIreallywanttoERASEALLmydatausingthePSID <YOURPSID> \\.\PhysicalDrive? > revertlog.txt 2>&1
