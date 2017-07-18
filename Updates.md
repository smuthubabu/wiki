Release 1.15
# V1.15 July 18,2017
Common updates:
- increase PBA load speed by up to 30x
- OS specific scan routine for more robust scan output
- introduce functions necessary to support multiple users
- introduce constants for ACE support
Windows changes:
- Initial NVMe support (identify only)
Linux changes:
- Update identify to allow USB (UASP) support
- Update NVMe support for 4.4+ kernels
PBA changes:
- Support for NVMe drives
- Remove ncurses dep
- Improved testing procedures
- Same kernel/linux base as rescue
- Improved Output

****I'm working on the doc now