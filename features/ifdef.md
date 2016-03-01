Ifdef Patch
===========

Conditional config options

Patch
-----

To check if Mutt supports "ifdef", look for "patch-ifdef" in the mutt version.

**Dependencies**
-   mutt-1.5.24

Introduction
------------

The "ifdef" command tests whether Mutt understands the name of a variable, function of command. If it does, then it executes a config command.

This useful command allows you to share one config file between versions of Mutt that may have different features compiled in.

The command is of the form:

    ifdef <item> <config-command>

where "item" can be the name of a $variable, \<function\> or command.

Commands
--------

    ifdef item "config-command [args]"

Muttrc
------

```bash
# Example Mutt config file for the 'ifdef' feature.

# The 'ifdef' command tests whether Mutt understands the name of
# a variable, function of command.  If it does, then it executes a
# config command.

# This useful command allows you to share one config file between
# versions of Mutt that may have different features compiled in.

# The command is of the form:
#       ifdef item 'config-command params'
# where item is a Mutt variable, function or command
#
# If the 'trash' variable exists, set it.

ifdef trash 'set trash=~/Mail/trash'

# If the 'tag-pattern' function exists, bind a key to it.

ifdef tag-pattern 'bind index <F6> tag-pattern'

# If the 'imap-fetch-mail' command exists, read my IMAP config.

ifdef imap-fetch-mail 'source ~/.mutt/imap.rc'

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

-   Cedric Duval \<cedricduval@free.fr\>
-   Matteo F. Vescovi \<mfvescovi@gmail.com\>
-   Richard Russon \<rich@flatcap.org\>

