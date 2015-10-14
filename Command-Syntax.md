

**General Usage:**

    sedutil-cli <-v> <--action> <options> <device>

 
Action and Options | Description
-------------------| -----------
-v | optional parameter to increase the verbosity (addition debugging information), one to five v’s
- –initialsetup &lt;password&gt; &lt;device&gt; | Prepare the drive for msed management.  This changes the default password on the drive, activates the LOCKING SP sets and up MBR shadowing. After this command the SID and Admin1 passwords are set to the password you entered and the global locking range is ready to be enabled.
–setSIDPwd &lt;password&gt; &lt;newpassword&gt; &lt;device&gt; | Change the password of the SID user in the ADMIN SP
-–setAdmin1Pwd &lt;password&gt; &lt;newpassword&gt; &lt;device&gt; | Change the password of the ADMIN1 user in the LOCKING SP
-–loadPBAimage &lt;password&gt; &lt;pba file spec&gt; &lt;device&gt; | Load the PBA image to the shadow MBR table.  PBA visibility is controlled by –setMBREnable below.
-–reverttper &lt;password&gt; &lt;device&gt; | Reset the device to it’s factory defaults using the SID password. If the locking SP is active this command ERASES ALL DATA, requires the  SID password
-–revertnoerase &lt;password&gt; &lt;device&gt; | Deactivate the Locking SP without erasing the data in the LBA range controlled by the Global Locking Range.  This command allows you to “shut off” OPAL locking without loosing data if you have not activated any user locking ranges. Requires the Admin1 password.
-–PSIDrevert &lt;password&gt; &lt;device&gt; | Reset the device to it’s factory defaults using the PSID. If the locking SP is active this command ERASES ALL DATA, requires the  32 byte PSID printed on the drive label
-–yesIreallywanttoERASEALLmydatausingthePSID &lt;password&gt; &lt;device&gt; | Reset the device to it’s factory defaults using the PSID. If the locking SP is active this command ERASES ALL DATA. requires the 32 byte PSID printed on the drive label
-–enableuser &lt;password&gt; &lt;userid&gt; &lt;device&gt; | Sets a locking SP user to the enabled state
-–activateLockingSP &lt;password&gt; &lt;device&gt; | Change the state of the Locking SP to active
-–scan | Scan the system and report on TCG disks
-–query &lt;device&gt; | Display details of the devices TCG SSC support
-–takeownership &lt;password&gt; &lt;device&gt; | Change the password of the SID and ADMIN1 users from the default (MSID) password.
-–revertLockingSP &lt;password&gt; &lt;device&gt; | Deactivate the Locking SP.  ERASES ALL DATA
-–setPassword &lt;password&gt; &lt;userid&gt; &lt;newpassword&gt; &lt;device&gt; | Change the password of the specified user in the Locking SP.
-–validatePBKDF2 | Test the password hashing functions output
-–setMBREnable &lt;on&#124;off&gt; &lt;password&gt; &lt;device&gt; | Set the MBREnable flag on the device.  If this is on the device will present the shadow MBR to the BIOS/OS when it is powered up.
-–setMBRDone &lt;on&#124;off&gt; &lt;password&gt; &lt;device&gt; | Set the MBRDone flag on the device.  If MBREnable is on this controls when to switch the drive out of shadowed state.
-–setLockingRange &lt;0-15&gt; &lt;ro&#124;rw&#124;lk&gt; &lt;password&gt; &lt;device&gt; | Modify the state of a locking range.
-–enableLockingRange &lt;0-15&gt; &lt;password&gt; &lt;device&gt; | Activate a locking range
-–disableLockingRange &lt;0-15&gt; &lt;password&gt; &lt;device&gt; | Deactivate a locking range
-–setupLockingRange &lt;0-15&gt; &lt;startLBA&gt; &lt;#LBA&gt; &lt;password&gt; &lt;device&gt; | Set/Change the LBAs controlled by a locking range. Changing the locking range that controls a LBA will ERASE ALL THE DATA on that locking range.
–-readonlyLockingRange &lt;0-15&gt; &lt;password&gt; &lt;device&gt; | Enable a locking range with only write locking active.  Creates a read only area at power up.
–-listLockingRanges &lt;password&gt; &lt;device&gt; | List the status and configutation of the locking ranges on a device.