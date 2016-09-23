Pi Cluster
----------
###### Sat Sep 10 07:34:03 EDT 2016

This project is about a clusterhat, strapped to a raspberry pi 3, strapped to a touchscreen.

Hardware:

- [Raspberry Pi 3](https://shop.pimoroni.com/products/raspberry-pi-3)
- [Raspberry Pi 0](https://shop.pimoroni.com/products/raspberry-pi-zero) (4x)
- [Raspberry Touchscreen](https://shop.pimoroni.com/products/raspberry-pi-7-touchscreen-display-with-frame)
- [Clusterhat](https://shop.pimoroni.com/products/cluster-hat)
- [Adafruit standoffs]()
- [Pimonori microusb Y splitter](https://shop.pimoroni.com/products/split-microb-usb-power-cable)
- [Pimonori raspberry powersupply](https://shop.pimoroni.com/products/raspberry-pi-universal-power-supply)

Software:

- Raspbian
- For the Pi3 only, probably not used: https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/net_tutorial.md
- https://learn.adafruit.com/turning-your-raspberry-pi-zero-into-a-usb-gadget/overview

Progress
--------
##### Sat Sep 10 07:48:56 EDT 2016
- Everything is acquired and assembled.
- Added `lcd_rotate=2` to /boot/config.txt to rotate the lcd screen.
- Added the following to `/etc/network/interfaces.d/wlan0` to configure wifi at start:
```
auto wlan0
iface wlan0 inet dhcp
        wpa-ssid Network Name
        wpa-psk Network Password
```
- Turning pi0s on and off requires gpio support:
  - http://blog.hypriot.com/post/lets-get-physical/
  - http://wiringpi.com/download-and-install/

##### Sun Sep 18 12:19:50 EDT 2016
- hypriot can't bring up ethernet gadgets
  - tried rebuilding the kernel, no luck. g_ether refused to load
- switched to rasbian
  - got ethernet gadget working
- http://blog.hypriot.com/post/install-docker-on-chip-computer/
- https://github.com/DieterReuter/arm-docker-fixes/blob/master/002-fix-install-docker-on-chip-computer/apply-fix-002.sh
- https://github.com/RPi-Distro/pi-gen
- https://easypi.herokuapp.com/kubernetes-on-raspberry-pi/
- pi-gen seems to build an img, ready to be written to a microsd card. will test later.

##### Mon Sep 19 21:57:49 EDT 2016
- pi-gen firmware worked. There's still some tweaks to be made:
- docker group
- configure usb0
  - http://flnkr.com/2016/03/identify-your-raspberry-pi-version/
	auto usb0
	iface usb0 inet static
		address 192.168.0.2
		netmask 255.255.255.0
		gateway 192.168.0.1
		dns-nameservers 10.42.0.1
- configure config.txt
- configure cmdline.txt
- add bridge utils
- no sleep thing in /etc/issues

##### Thu Sep 22 19:53:55 EDT 2016
- pi-gen is progressing nicely
- network config for the pi3 and pi0 in testing
- to turn on pi0 3: `docker run --rm --cap-add SYS_RAWIO --device /dev/mem hypriot/rpi-gpio write 24 1`
- pi-gen image boots on pi3 and pi0s
- pi-gen image pushed to github: https://github.com/brimstone/pi-gen
