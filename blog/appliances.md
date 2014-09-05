Appliances
----------
######Sun Oct 20 22:34:25 EDT 2013

With the advent of Virtual Machines, appliances have become an interesting topic. At Makers Local 256, I rolled a pretty custom VM hosting solution for them. It's close to unmaintainable :(. At Freeside I've attempted to correct this. Instead of Debian stable + xen, we're using [Proxmox](http://www.proxmox.com/proxmox-ve). Instead of Debian stable + iptables-restore, we're using [openwrt](http://downloads.openwrt.org/attitude_adjustment/12.09/x86/kvm_guest/). Instead of Debian stable + Zimbra debs, we're probably going to use Ubuntu LTS + debs or an appliance, if Zimbra is still providing one of those. Someone has also started an [appliance farm](http://www.turnkeylinux.org/), of sorts.
