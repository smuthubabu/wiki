TERM | Explanation
---- | -----------
ADMIN SP | This is the Administrative Security Provider.  It is the OPAL construct that administers the security on the drive.  
LOCKING SP | This is the Locking Security Provider.  It is the OPAL construct that manages the locking and unlocking of the locking ranges on the drive 
MBR shadow table | An OPAL table that can be loaded with a PBA and will be presented to the BIOS/OS if the drive is locked and the MBREnable flag is set on.  
 PBA | Pre-Boot Authorization a) The sequence of events that occur before the OS is booted that unlock a drive. b) The boot image loaded to the MBR shadow table that is presented to the BIOS as a bootable image to initiate the Pre-Boot authorization activity.
PSID | Physical Security Identification - This is a method of identifying a user who has physical possession of the drive.  "If they have the PSID they must be able to touch the drive."
SID | Security ID - root/administrator ID in the ADMIN SP
SSC | Security Subsystem Class - A standard for how a subsystem should work in the TCG frame work.  The OPAL SSCs are part of the storage subdivision of the TCG framework and are fully described as a "Storage Security Subsystem Class".
TCG | Trusted Computing Group  - The standards body that developed the OPAL SSCs