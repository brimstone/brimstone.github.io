Regex Isn't Scary
-----------------
Matt

[@brimston3](https://twitter.com/brimston3)

https://brimstone.github.io

Note: <a href="slides.html?talks/regex-isnt-scary.md#!">View this as slides</a>
- How many people have heard of regex?
- Who are the regex masters?



What is regex?
--------------

_REG_ ular _EX_ pressions

"regular" being rooted in mathmatics

Represented by: `/pattern/`



Why regex?
----------

Super powerful!

Supported in every programming language!



Python
------
```
import re
string1 = "Hello, world."
if re.search(r"Hello", string1):
    print "Hello to you too!"
```

`"Hello, world." ~ /Hello/`

`"Hello, world." !~ /banana/`

Note: These formats will be used interchangeably in this document.



Simplest
--------

normal letters are normal

special characters are special

`"abcdefg" ~ /abc/`

`"0123456789" ~ /123/`

Note: Technically, only `abc` and `123` are matched in these examples.



Character sets []
-----------------

Matches any single character

`"banana" ~ /[an]/`

All lower letters: `/[a-z]/`

All numbers: `/[0-9]/` (shortcut: `/\d/`)

Negate chars: `"potato" ~ /[^b]/`



Any character
-------------

A single period matches any character.

`"banana" ~ /./`



Groups ()
---------

`"potato" ~ /(pot)/`

```
string1 = "potato"
m_obj = re.search(r"(pot)", string1)
if m_obj:
    print "We matched '" + m_obj.group(1) + "'"
```

`We matched 'pot'`



Combinations!
-------------

`"potato" ~ /(p..)/`

```
string1 = "potato"
m_obj = re.search(r"(p..)", string1)
if m_obj:
    print "We matched '" + m_obj.group(1) + "'"
```

`We matched 'pot'`



Ranges
------

Match 2: `/a{2}/`

Match 2 or 3: `/a{2,3}/`



Combinations!
-------------

`"potato" ~ /(p.{2})/`

```
string1 = "potato"
m_obj = re.search(r"(p.{2})", string1)
if m_obj:
    print "We matched '" + m_obj.group(1) + "'"
```

`We matched 'pot'`



Wildcards
---------

Any amount: `{0,}` (shortcut:  `*`)

`"banana" ~ /p*/`

At least one: `{1,}` (shortcut: `+`)

`"banana" !~ /p+/`

Previous character optional: `?`

`"banana" ~ /bx?/`



`"potato" ~ /(p.+)/`

```
string1 = "potato"
m_obj = re.search(r"(p.+)", string1)
if m_obj:
    print "We matched '" + m_obj.group(1) + "'"
```

`We matched 'potato'`



`"banana" ~ /b(an)+/`

```
string1 = "banana"
m_obj = re.search(r"b(an)+", string1)
if m_obj:
    print "We matched '" + m_obj.group(1) + "'"
```

`We matched 'banan'`



Anchors
-------

`"hello world" ~ /^hello/`

Matches `hello`

`"hello world" ~ /world$/`

Matches `world`



Replace matches
---------------

```
string1 = "Hello, world"
re.sub("Hello", "Goodbye", string1)
print string1
```

`Goodbye, world`



# Ready?

Note: Got a good grasp? Ready for something useful?



Strip all HTML tags
-------------------

`/<[^>]*>/`

```
string1 = "<html><body>Content</body></html>"
re.sub("<[^>]*>", "", string1)
print string1
```

`Content`



Is Regex still scary to you?
----------------------------
