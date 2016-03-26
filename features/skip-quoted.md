Skip-Quoted Patch
=================

Leave some context visible

Patch
-----

**Dependencies**
-   mutt-1.5.24

Introduction
------------

When viewing an email, the `<skip-to-quoted>` function (by default the `S` key)
will scroll past any quoted text. Sometimes, a little context is useful.

By setting the `$skip_quoted_offset` variable, you can select how much of the
quoted text is left visible.

Variables
---------

| Name                 | Type   | Default |
|:---------------------|:-------|:--------|
| `skip_quoted_offset` | number | 0       |

Muttrc
------

```bash
# Example Mutt config file for the 'skip-quoted' patch.

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
-   Richard Russon \<rich@flatcap.org\>

