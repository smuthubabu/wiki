**Getting the source**  
clone this repository.

**Windows**  
Only the Host management portion of sedutil can be built on windows.

sedutil has a VIsual Studio solution you can use to select the architecture and build the executable. There are no external dependencies.

**Linux**  
To build sedutil on Linux you need to have a host that supports multiarch builds.
sedutil requires both 32 & 64 bit C and C++ libraries to build successfully.

There is a NetBeans project to build Linux host management program portion of sedutil included in the repo, if you wish to build from the command line you can use make and select the configuration to build.
make CONF=”” build where conf is one of the NetBeans configurations.

There is also an autotools based make system in the project root.  This is the standard ./configure, make, make install that is expected with autotools.

To build the Syslinux based PBA:
cd /dir/containing/syslinux
make clean
make bios

When the PBA has compiled you can build the image using the shell script in sedutil/images
cd /dir/containing/sedutil-cli
cd images
sudo ./buildbiospba

To build the a Linux based PBA:

cd /dir/containing/sedutil-cli
cd images
sudo ./script-to-build-pba