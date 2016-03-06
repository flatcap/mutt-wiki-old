Quasi-Delete Patch
==================

Mark emails that should be hidden, but not deleted

Patch
-----

To check if Mutt supports "Quasi-Delete", look for "patch-quasi-delete" in the mutt version.

**Dependencies**
-   mutt-1.5.24

Introduction
------------

The "quasi-delete" function marks an email that should be hidden from the index, but NOT deleted.

On its own, this patch isn't very useful. It forms a useful part of the notmuch plugin.

Functions
---------

**Quasi-Delete Functions**

| Menus       | Default Key | Function         | Description                           |
|:------------|:------------|:-----------------|:--------------------------------------|
| index,pager | (none)      | `<quasi-delete>` | delete from mutt, don't touch on disk |

Muttrc
------

```bash
# Example Mutt config file for the 'quasi-delete' feature.

# The 'quasi-delete' function marks an email that should be hidden
# from the index, but NOT deleted.
bind index,pager Q quasi-delete

# vim: syntax=muttrc
```

See Also
--------

-   NeoMutt project
-   [[notmuch patch|notmuch]]

Known Bugs
----------

None

Credits
-------

-   Karel Zak \<kzak@redhat.com\>
-   Richard Russon \<rich@flatcap.org\>

