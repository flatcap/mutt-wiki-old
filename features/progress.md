Progress Bar Patch
==================

Show a visual progress bar on slow operations

Patch
-----

To check if Mutt supports “Progress Bar”, look for “patch-progress” in
the mutt version.

**Dependencies**
-   mutt-1.5.24

Introduction
------------

The “progress” patch shows a visual progress bar on slow tasks, such as
indexing a large folder over the net.

Colors
------

**Progress Colors**

Name         | Default Color   | Description
------------ | --------------- | ---------------------
`progress`   | default         | Visual progress bar

Muttrc
------

```bash
# Example Mutt config file for the 'progress' patch.
    
# The 'progress' patch provides clear visual feedback for
# slow tasks, such as indexing a large folder over the net.
    
# Set the color of the progress bar
# White text on a red background

color progress white red

# vim: syntax=muttrc
```

See Also
--------

None

Known Bugs
----------

None

Credits
-------

-   Stefan Kuhn \<wuodan@hispeed.ch\>
-   Karel Zak \<kzak@redhat.com\>
-   Richard Russon \<rich@flatcap.org\>
