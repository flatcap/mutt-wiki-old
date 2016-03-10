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

The "ifdef" patch introduces three new commands to Mutt and allow you to share one config file between versions of Mutt that may have different features compiled in.

    ifdef  symbol config-command [args...]  # If a symbol is defined
    ifndef symbol config-command [args...]  # If a symbol is not defined
    finish                                  # Finish reading the current file

Here a symbol can be a $variable, \<function\>, command or compile-time symbol, such as "USE\_IMAP".

`finish` is particularly useful when combined with `ifndef`. e.g.

```bash
# Sidebar config file
ifndef USE_SIDEBAR finish
```

Commands
--------

    ifdef  symbol "config-command [args]"
    ifndef symbol "config-command [args]"
    finish

Muttrc
------

```bash
# Example Mutt config file for the 'ifdef' feature.

# This feature introduces three useful commands which allow you to share
# one config file between versions of Mutt that may have different
# features compiled in.

#   ifdef  symbol config-command [args...]
#   ifndef symbol config-command [args...]
#   finish

# The 'ifdef' command tests whether Mutt understands the name of
# a variable, function, command or compile-time symbol.
# If it does, then it executes a config command.

# The 'ifndef' command tests whether a symbol does NOT exist.

# The 'finish' command tells Mutt to stop reading current config file.

# If the 'trash' variable exists, set it.
ifdef trash 'set trash=~/Mail/trash'

# If the 'tag-pattern' function exists, bind a key to it.
ifdef tag-pattern 'bind index <F6> tag-pattern'

# If the 'imap-fetch-mail' command exists, read my IMAP config.
ifdef imap-fetch-mail 'source ~/.mutt/imap.rc'

# If the compile-time symbol 'USE_SIDEBAR' does not exist, then
# stop reading the current config file.
ifndef USE_SIDEBAR finish

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

