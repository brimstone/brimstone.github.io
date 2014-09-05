Cookie Clicker
--------------
######Sun Sep 15 12:24:00 EDT 2013

I've been playing [Cookie Clicker](http://orteil.dashnet.org/cookieclicker/). A delightful little game where you click cookies. After 15 clicks or so, you can purchase a mouse cursor to click the cookie for you.

Webgames like these are written in Javascript and since they're so large, they have a very human readable memory structure of variables and functions. These games are fun for a bit, but I like to play with the game, not just play the game. For this, we'll need [Firebug](https://getfirebug.com/) or whatever you chrome users use. Install that and come back here.

By default, Firebug puts a little bug icon in the bottom right corner of your screen. Clicking this, or pressing F12, opens Firebug. Across the top you'll see tabs for Console, HTML, CSS, Script, DOM, Net, and Cookies. These cookies have nothing to do with the game. Click the DOM tab to expose all of the objects and attributes of the window object for this page.

You'll see that near the top there's a Game object. Click the plus next to it and explore all of the different objects and attributes for this game. Tweaking these will affect the game. Have fun!

At the bottom of the attributes and objects, there's functions that have been bound to the Game object. One of these is RuinTheFun. If you want, click back over to the Console tab and enter in `Game.RuinTheFun()` then press enter. This does exactly as advertised.
