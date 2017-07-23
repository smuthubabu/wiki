**How does sedutil store my password?**   
sedutil does not store your password anywhere, ever.  sedutil takes the password you enter and runs it through the PKCS PBKDF2 function using the drive serial number as the salt to create a 32 byte drive unique password.  This drive unique password is then passed to the OPAL subsystem, the OPAL specification says that the password is stored in the "c_pin table" of the SP,  securing this table is the responsibility of the drive manufacture.  

**What does method status xxxx mean?**   
The method status codes are defined in excruciating detail in the OPAL SSCs.  Here are simple explanations of the method status codes you are likely to see when using sedutil.  
  
Return code | Explanation
------------ | -----------
NOT_AUTHORIZED | you typed in your password incorrectly.
AUTHORITY_LOCKED_OUT | You have exceeded the maximum number of tries to enter your password correctly, the drive must be powered down before you can continue.
SP_BUSY | A prior session was not correctly closed.  The drive will need to be powered off to reset this condition. This is probably a bug, please report it if you can duplicate it.
INVALID_PARAMETER | The command sent to the drive is incorrectly formatted.  This can be either a program or user error.  The most likely error is that you are trying to issue a command to the ADMIN SP before it has been activated.  Make sure you have run initialsetup before trying to setup the locking ranges.

**What does xxxxxx mean?**  

The OPAL/TCG world is full of wonderful new terms, here is a list of the ones used on this site.

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