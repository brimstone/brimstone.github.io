Information Radiator
--------------------
###### Fri Sep  5 22:22:08 EDT 2014

This project is about my information radiator.

I plan on using the following:

Hardware:

* Beagle Bone Black
* DisplayLink monitor
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
* Looks like udlfb.ko isn't supported in 3.8.13-bone50. I'll have to [compile from source](http://dumb-looks-free.blogspot.com/2014/06/beaglebone-black-bbb-compile-kernel.html).
* Today's objective is now to get the b³ accessible from my laptop, but not running from the usb cable connected to my laptop.

