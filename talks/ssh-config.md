SSH Config
----------
Matt

[@brimston3](https://twitter.com/brimston3)

https://brimstone.github.io

Note: <a href="slides.html?talks/ssh-config.md#!">View this as slides</a>



Specifying Hosts
----------------
`$HOME/.ssh/config`
```
Host *
	Compression yes
```

```
Host bastion
	Username notroot
	Hostname bastion.us-east1.aws.amazon.com
	Port 2022
```



CLI Tricks
----------
All of these are the same
```
Host bastion
	Username notroot
	Hostname bastion.us-east1.aws.amazon.com
	Port 2022
…
$ ssh bastion
```
```
ssh -o Port=2022 -o Username=notroot bastion.us-east1.aws.amazon.com
```
```
ssh -p 2022 -l notroot bastion.us-east1.aws.amazon.com
```
```
ssh -p 2022 notroot@bastion.us-east1.aws.amazon.com
```



Persistent connections
----------------------
```
Host *
	ControlMaster auto
	ControlPersist 10
	ControlPath ~/.ssh/master-%r@%h:%p
```

If the network goes weird, reconnect:
```
$ ssh -O exit
```

Note: Important to not use 0 for `ControlPersist`
Important to set `ControlPath` to somewhere secure



SSH Agent
---------
Stop entering your ssh key password every time!

Add a key
```
$ ssh-add
```

Show keys
```
$ ssh-add -l
```

Remove all keys
```
$ ssh-add -D
```



IdentityFile
------------
Use a different ssh key for a connection.
```
Host *
	IdentityFile ~/.ssh/id_rsa_otherkey
```
```
$ ssh -i ~/.ssh/id_rsa_otherkey
```



ForwardAgent
------------
Allow a host to use your client's ssh agent
```
Host *
	ForwardAgent yes
```
```
ssh -A host
```
```
$ env
…
SSH_AUTH_SOCK=/tmp/ssh-HE5YrE6Tte/agent.26366
SSH_CLIENT=10.0.0.8 55844 22
SSH_CONNECTION=10.0.0.8 55844 10.0.0.1 22
SSH_TTY=/dev/pts/2
…
```



Forward Ports
-------------
Expose a port through the firewall.
```
Host *
	LocalForward 3306 127.0.0.1:3306
```
```
$ ssh -L3306:127.0.0.1:3306
```




Forward ALL THE PORTS
---------------------
Dynamically forward connections. This is basically a SOCKS5 proxy.
```
Host *
	DynamicForward 1080
```
```
$ ssh -D 1080
```




ProxyCommand
------------
Run a specific command, then use its stdin/out
```
Host *
	ProxyCommand /usr/bin/nc -X connect -x 192.168.0.2:8080 %h %p
```
```
$ ssh backend
```



ConnectionAttempts
------------------
Try to connect more than just once
```
Host *
	ConnectionAttempts 1
```



Dark Magic: Jump host
---------------------
https://wiki.gentoo.org/wiki/SSH_jump_host
```
Host *+*
  ProxyCommand ssh $(echo %h | sed 's/+[^+]*$//;
		s/\([^+%%]*\)%%\([^+]*\)$/\2 -l \1/;
		s/:/ -p /') exec nc -w1 $(echo %h |
			sed 's/^.*+//;/:/!s/$/ %p/;s/:/ /')
```
```
$ ssh host1+host2
```
```
$ ssh user1%host1+host2
```



Dark Magic: `sshf`
------------------
```
alias sshf='ssh -o UserKnownHostsFile=/dev/null
	-o StricktHostKeyChecking=no -S none'
```



Encore: Hidden CLI Commands!
----------------------------
~?
