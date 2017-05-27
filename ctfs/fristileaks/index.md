fristileaks
===========
##### Thu May 25 12:45:03 EDT 2017

https://www.vulnhub.com/entry/fristileaks-13,133/

- zaproxy doesn't find anything interesting
- robots.txt points to some disallowed directories, all of which mention an image in /images/

Finally found the right drink: /fristi/ ;)

- zaproxy has no insight about this directory
- Found username in comments
- hidden image, decoded password
  - keKkeKKeKKeKkEkkEk

- weevely web shell uploaded with .php.png extension

- found note about admin executing /tmp/runthis every minute
- got a reverse shell with /usr/bin/python to execute and get me to admin
- found crypted passwords in /home/admin
- base64, rot13, and reversing tripped me up for far too long
