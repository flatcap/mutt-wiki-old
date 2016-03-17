Skip-Quoted Patch
=================

Patch
-----

**Dependencies**
-   mutt-1.5.24

Introduction
------------

The 'S' (skip-quoted) command scrolls the pager past the quoted text (usually
indented with '> '.  Setting `skip_quoted_offset` leaves some lines of quoted
text on screen for context.

Muttrc
------

```bash
# Example Mutt config file for the 'skip-quoted' feature.

# The 'S' (skip-quoted) command scrolls the pager past the quoted text (usually
# indented with '> '.  Setting 'skip_quoted_offset' leaves some lines of quoted
# text on screen for context.

# Show three quoted lines before the reply
set skip_quoted_offset = 3

# vim: syntax=muttrc
```

See Also
--------

-   NeoMutt project

Known Bugs
----------

None

Credits
-------

-   David Sterba \<dsterba@suse.cz\>

