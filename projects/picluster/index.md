Pi Cluster
----------
###### Sat Sep 10 07:34:03 EDT 2016

This project is about a clusterhat, strapped to a raspberry pi 3, strapped to a touchscreen.

Hardware:

- Raspberry Pi 3
- Raspberry Pi 0 (4x)
- Raspberry Touchscreen
- Pimonori stand
- Clusterhat
- Adafruit standoffs
- Pimonori microusb Y splitter
- Pimonori raspberry powersupply

Software:

- Hypriot 1.0.0
- For the Pi3 only, probably not used: https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/net_tutorial.md
- https://learn.adafruit.com/turning-your-raspberry-pi-zero-into-a-usb-gadget/ethernet-gadget

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

