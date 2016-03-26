Sensible-Browser Patch
======================

Make the file browser behave

Patch
-----

To check if Mutt supports "sensible-browser", look for "patch-sensible-browser" in the mutt version.

**Dependencies**
-   mutt-1.5.24

Introduction
------------

When using the file/folder browser, the selection isn't always where you would
expect. When you navigate to '..' (parent folder), the selection should show the
folder you *used* to be in.

Muttrc
------

None

See Also
--------

-   NeoMutt project

Known Bugs
----------

-   Limited to IMAP folders
-   Always on
-   Should only select folder when folder is sorted alphabetically

Credits
-------

-   Haakon Riiser \<haakon.riiser@fys.uio.no\>
-   Richard Russon \<rich@flatcap.org\>

