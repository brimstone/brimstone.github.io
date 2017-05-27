pwnlab
------
###### Sat May 27 13:06:17 EDT 2017

https://www.vulnhub.com/entry/pwnlab-init,158/

After hours of poking and prodding, I finally broke down and looked at a
walkthrough. I had found what looked like some sort of LFI, but with a forced
'.php' suffix. The walkthrough pointed out the following:
```
curl http://site/?page=php://filter/convert.base64-encode/resource=index
```

This reveiled the source to all of the php files I had found earlier.

I found valid mysql creds that worked from outside localhost inside
`config.php`.

I was able to dump the mysql database Users with them.

`login.php` showed how to encode, and thus, how to decode the passwords found in
the Users DB.

`upload.php` showed several sanity checks trying to ensure what was uploaded was
actually an image.

It was easy enough to load a webshell that passed all of these checks.

Webshell allowed a revert tcp netcat shell.

netcat shell revealed kernel was vulnerable to dirtycow.

Game over.
