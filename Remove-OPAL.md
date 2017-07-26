The steps outlined below will allow you to turn off the opal locking and return the drive to the manufactured default state without erasing any data **managed by the global locking range**.

This process has been tested on the following drive/firmware versions:  
    Crucial_CT120M500SSD3                    MU05  
    ST500LT025-1DH142                        0001SDM7  
    Samsung SSD 850 EVO 500GB                EMT01B6Q  

even though this procedure is part of the OPAL specification there is no guarantee that sedutil is compatible with the OPAL firmware on all drives.

1. revert the locking SP.  
sedutil-cli --revertnoerase {Admin1Password} {drive}

2. verify that the locking SP has been deactivated  
sedutil-cli --query {drive}

look at the query output and make certain that the Locking section shows lockingEnabled=N  
    --------  
    Locking function (0x0002)  
        Locked = N, LockingEnabled = N, LockingSupported = Y,   <snip>  
    ---------  

If the query does not show lockingEnabled=N DO NOT CONTINUE with the next step, if you do all your data will be erased.

3. msedutil-cli --reverttper {SIDpassword} {drive}

When this is finished the drive will be in a non-opal managed state.  This would allow you to do anything that you could have done before starting OPAL management under OPAL.  You can also reinitiate OPAL management if you wish.
