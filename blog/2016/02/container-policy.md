Container Policy
----------------
######Tue Feb  9 12:59:13 EST 2016

I don't have a better place, so this goes here.

Containers need to follow some sort of a policy to be reasonable. I'm going to
attempt to describe that here. This document should and will change over time.

Docker Images
-------------
- *All images must be built from a known acceptable layer.*
- *All images must include a label identifying the command to retrieve a package listing.*
- *All images must define each environment variable that can affect the image with a sane default.*

Docker Containers
-----------------
