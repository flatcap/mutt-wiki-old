Fmemopen Patch
==============

Replace some temporary files with memory buffers

Patch
-----

To check if Mutt supports "fmemopen", look for "patch-fmemopen" in the mutt version.

**Dependencies**
-   mutt-1.5.24
-   `open_memstream()`, `fmemopen()` from glibc

Introduction
------------

The "fmemopen" patch speeds up some searches.

This patch changes a few places where Mutt creates temporary files. It replaces them with in-memory buffers. This should improve the performance when searching the header or body using the $thorough\_search option.

There are no user-configurable parts.

This patch depends on `open_memstream()` and `fmemopen()`. They are provided by glibc. Without them, Mutt will simply create temporary files.

Muttrc
------

None

See Also
--------

-   NeoMutt project
-   Compile-Time Features
-   `fmemopen(3)`

Known Bugs
----------

None

Credits
-------

-   Julius Plenz \<plenz@cis.fu-berlin.de\>
-   Richard Russon \<rich@flatcap.org\>

