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
