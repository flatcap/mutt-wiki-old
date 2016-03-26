Limit-Current-Thread Patch
==========================

Focus on one Email Thread

Patch
-----

**Dependencies**
-   mutt-1.5.24

Introduction
------------

This patch adds a new way of using the Limit Command. The
`<limit-current-thread>` function restricts the view to just the current thread.
Setting the limit (the `l` key) to "all" will restore the full email list.

Functions
---------

| Menus | Default Key | Function                 | Description                  |
|:------|:------------|:-------------------------|:-----------------------------|
| index | `<Esc> L`   | `<limit-current-thread>` | Limit view to current thread |

Muttrc
------

```bash
# Example Mutt config file for the 'limit-current-thread' patch.

# Limit view to current thread
bind index <esc>L limit-current-thread

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

