Information Radiator
--------------------
###### Fri Sep  5 22:22:08 EDT 2014

This project is about my information radiator.

I plan on using the following:

Hardware:

* Beagle Bone Black
* DisplayLink monitor - [AOC e2251Fwu](http://note-to-self.baker.com/2012/12/17/aoc-e2251fwu-22-displaylink-usb-monitor/)
* Alfa wireless card
* Logitech bluetooth keyboard, mouse, and adapter.
* Anker battery
* Cheap chinese usb hub and cables
* Cheap 4GB microSD card, cuz why not

Software:

* Beagle Bone Black Debian distro
* [Dashing](https://shopify.github.io/dashing/)

Progress
--------

######Sat Sep  6 14:13:31 EDT 2014
* Started documenting the project.
* Current strategy is to tape the b³, battery and parts to the back of the monitor so it's completely wireless.
* Current architecture is to simply display firefox and have dashing run from a docker container somewhere.
* Today's objective is to get the monitor displaying X.
* udlfb.ko isn't supported in 3.8.13-bone50. I'll might have to [compile from source](http://dumb-looks-free.blogspot.com/2014/06/beaglebone-black-bbb-compile-kernel.html) later.
* 1A usb power adapter -> b³ -> alfa/monitor is not enough. Had to plug the monitor's second usb cable into its own 1A adapter.
* I learned via [a page on elinux.org](http://www.elinux.org/BeagleBoardUbuntu#eMMC:_BeagleBone_Black) that the official image has a `/opt/scripts/tools/update_kernel.sh. The 3.16 "beta" kernel has udl.ko baked in, and udlfb as a module, neither make the screen go green.
* after an unexpected power failure, the b³ now no longer lights up at all under usb power. I need to find a 5V 2A barrel connector to try next.

######Sun Sep 21 17:26:00 EDT 2014
For other versions of linux to find the necessary commit-id's go to https://github.com/raspberrypi/firmware/commits/master and look though the list of firmware commits for one close to your version. Then select browse code (<>) and look at firmware/extra/uname-string to check linux version, 3.12.xx+, and build number, #123. When you find the right version and build look at firmware/extra/git_hash for the linux source commit-id. The full commit-id is a 40 character value but you should only need to use the first 7-10 character to set the right source version.
From [the forums](http://www.raspberrypi.org/forums/viewtopic.php?f=66&t=82811)

# download linux source - --depth will restict the amount downloaded
# as you don't need the whole repository
git clone --depth 500 https://github.com/raspberrypi/linux.git
# download firmware source - restrict the amount downloaded with --depth
git clone --depth 15 https://github.com/raspberrypi/firmware.git
# set up some symbolic links needed by compile
sudo ln -s /home/pi/src/linux /lib/modules/$(uname -r)/build
sudo ln -s /home/pi/src/linux/arch/arm /home/pi/src/linux/arch/armv6l
# enter linux directory
cd linux
# set up linux source to 3.12.22+ #690 (git checkout commit-id)
# for a different version change the commit-id
# for 3.12.22+ #691 use commit-id 1981ddebd4
git checkout 99df631ec3
# enter firmware directory and set for 3.12.22+ #690 (git checkout commit-id)
# for 3.12.22+ #691 use commit-id 462f3e3f47
cd ../firmware
git checkout 5bb0317210
# go back to linux source directory
cd ../linux
# set up linux to compile your module - make mrproper: init sourc
# - make  bcmrpi_defconfig: set up .config file
# - make modules_prepare: compile to set up for module
# - cp ../firmware/extra/Module.symvers . - copy file Module.symvers from firmware to linux directory
# - NOTE: period (full stop) after Module.symvers
make mrproper && make bcmrpi_defconfig && make modules_prepare && cp ../firmware/extra/Module.symvers .
# now go to your rtl8717L source directory wherever it is
cd ../rtl8717L
# init module source and compile it
make clean && make
# and hopefully it will compile without errors. 

http://elinux.org/RPi_Kernel_Compilation
