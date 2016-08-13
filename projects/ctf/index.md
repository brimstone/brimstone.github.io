CTF
===
###### Wed Aug  3 11:50:22 UTC 2016

_This is a repost from a mailing list_

You would love to take part in a CTF but where do you start?

This article shows just how simple some of the attacks are to pull off. You can learn all about the OWASP top ten web app vulnerabilities and how they work by using WebGoat (links after article).

Sealed with an XSS: Popular vulnerabilities probed
You don't have to be an infosec genius to protect yourself
http://www.theregister.co.uk/2016/08/03/what_do_those_vulnerabilities_mean/

http://preview.tinyurl.com/jsbn7bg



"OWASP WebGoat is a deliberately insecure web application maintained by OWASP designed to teach web application security lessons."
https://www.owasp.org/index.php/Category:OWASP_WebGoat_Project


You can get the latest version of WebGoat here:
https://github.com/WebGoat/WebGoat/releases/latest


Scroll down until you see

   Downloads

   WebGoat-7.0.1-war-exec.jar


Click on WebGoat-7.0.1-war-exec.jar and down load it to your desktop

https://github.com/WebGoat/WebGoat/releases/download/7.0.1/webgoat-container-7.0.1-war-exec.jar


From a command prompt run

"[path to java.exe]\java.exe" -jar "[path to WebGoat]\WebGoat-7.0.1-war-exec.jar"


Bring up a browser (Chrome and Firefox work).

Browse to (case sensitive)

http://localhost/WebGoat/attack


Login using the Webgoat user account and password

User = guest
Password = guest


You will also need a copy of OWASP Zed Attack Proxy (ZAP) to complete the lessons
https://www.owasp.org/index.php/ZAP


You can get the latest version of ZAP here:
https://github.com/zaproxy/zaproxy/releases/latest

	
You can get more CTF information here:

Capture The Flag (CTF) and Pentest Training Tools
http://www.cc.gatech.edu/~krwatson/ctf.html

keith
