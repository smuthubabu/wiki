**SCAN**

U:\Users\r0m30\Documents\Visual Studio 2013\Projects> sedutil-cli –scan  
Scanning for Opal compliant disks  
\\.\PhysicalDrive0  2  Crucial_CT120M500SSD3                    MU05  
\\.\PhysicalDrive1  2  ST500LT025-1DH142                        0001SDM7  
\\.\PhysicalDrive2 No  Hitachi HDT725040VLA360                  V5COA7BA  
\\.\PhysicalDrive3 12  Samsung SSD 850 EVO 500GB                EMT01B6Q  
No more disks present ending scan  

**QUERY**

U:\Users\r0m30\Documents\Visual Studio 2013\Projects> sedutil-cli –query \\.\PhysicalDrive3  
\\.\PhysicalDrive3 ATA Samsung SSD 850 EVO 500GB                <DRIVESERIALNO>  
TPer function (0x0001)  
ACKNAK = N, ASYNC = N. BufferManagement = N, comIDManagement  = N, Streaming = Y, SYNC = Y  
Locking function (0x0002)  
Locked = N, LockingEnabled = Y, LockingSupported = Y, MBRDone = Y, MBREnabled = Y, MediaEncrypt = Y  
Geometry function (0x0003)  
Align = N, Alignment Granularity = 1 (512), Logical Block size = 512, Lowest Aligned LBA = 0  
unction (0x0200)  
Base comID = 0x1004, comIDs = 1  
SingleUser function (0x0201)  
ALL = N, ANY = N, Policy = Y, Locking Objects = 9  
DataStore function (0x0202)  
Max Tables = 9, Max Size Tables = 10485760, Table size alignment = 1  

OPAL 2.0 function (0x0203)  
Base comID = 0x1004, Initial PIN = 0x0 , Reverted PIN = 0x0 , comIDs = 1  
Locking Admins = 4, Locking Users = 9, Range Crossing = N  

TPer Properties:  
MaxComPacketSize = 66048  MaxResponseComPacketSize = 66048  
MaxPacketSize = 66028  MaxIndTokenSize = 65992  MaxPackets = 1  
MaxSubpackets = 1  MaxMethods = 1  MaxAuthentications = 5  
MaxSessions = 1  MaxTransactionLimit = 1  DefSessionTimeout = 0  

Host Properties:  
MaxComPacketSize = 2048  MaxResponseComPacketSize = 2048  
MaxPacketSize = 2028  MaxIndTokenSize = 1992  MaxPackets = 1  
MaxSubpackets = 1  MaxMethods = 1  