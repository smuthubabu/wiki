How does msed store my password?  
Msed does not store your password anywhere, ever.  msed takes the password you enter and runs it through the PKCS PBKDF2 function using the drive serial number as the salt to create a 32 byte drive unique password.  This drive unique password is then passed to the OPAL subsystem, the OPAL specification says that the password is stored in the "c_pin table" of the SP,  securing this table is the responsibility of the drive manufacture.  

What does method status xxxx mean?  
The method status codes are defined in excruciating detail in the OPAL SSCs.  Here are simple explanations of the method status codes you are likely to see when using msed.  
  
Return code | Explanation
------------ | -----------
NOT_AUTHORIZED | you typed in your password incorrectly.
AUTHORITY_LOCKED_OUT | You have exceeded the maximum number of tries to enter your password correctly, the drive must be powered down before you can continue.
SP_BUSY | A prior session was not correctly closed.  The drive will need to be powered off to reset this condition. This is probably a bug, please report it if you can duplicate it.
INVALID_PARAMETER | The command sent to the drive is incorrectly formatted.  This can be either a program or user error.  The most likely error is that you are trying to issue a command to the ADMIN SP before it has been activated.  Make sure you have run initialsetup before trying to setup the locking ranges.

Why does it take so long to load the PBA?
Two reasons:

Interaction with the OPAL subsystem is a low priority task, this is actually a good thing as you would not want your real I/O slowed down during OPAL configuration.  Typical times to issue an OPAL command and receive the response vary wildly, the Crucial M500 drive responds almost instantly while the Seagate ST500-LT025 takes 50-100ms  so msed waits 25ms before looking for a response and 25ms before looking again if the response is not ready. This means that a write to an OPAL configuration table can take 5-20 times longer that a typical disk write.

To keep the code as uncomplicated as possible msed uses the minimum buffer size defined in the OPAL SSCs even it the drive is capable of using larger buffers. Smaller buffers mean more transfer operations.  The higher number of operations combined with the long operation time above means slow PBA loading.

The good news is that you shouldn't have to load the PBA often.
What does xxxxxx mean?

The OPAL/TCG world is full of wonderful new terms, here is a list of the ones used on this site.