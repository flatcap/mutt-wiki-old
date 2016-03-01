Status Color Patch
==================

Custom rules for theming the status bar

Patch
-----

To check if Mutt supports "Status Color", look for "patch-status-color" in the mutt version.

**Dependencies**
-   mutt-1.5.24

Introduction
------------

The "status-color" patch allows you to theme different parts of the status bar (also when it's used by the index).

Unlike normal color commands, `color status` can now take up to 2 extra parameters (regex, num).

Commands
--------

    color status foreground background [ regex [ num ]]

With zero parameters, Mutt will set the default color for the entire status bar.

With one parameter, Mutt will only color the parts matching the regex.

With two parameters, Mutt will only color the num'th sub-match of the regex.

Colors
------

**Status Colors**

| Name   | Default Color | Description |
|:-------|:--------------|:------------|
| status | `reverse`     | Status bar  |

Muttrc
------

```bash
# Example Mutt config file for the 'status-color' patch.

# The 'status-color' patch allows you to theme different parts of
# the status bar (also when it's used by the index).

# For the examples below, set some defaults

set status_format='-%r-Mutt: %f [Msgs:%?M?%M/?%m%?n? New:%n?%?o? Old:%o?%?d? Del:%d?%?F? Flag:%F?%?t? Tag:%t?%?p? Post:%p?%?b? Inc:%b?%?l? %l?]---(%s/%S)-%>-(%P)---'
set index_format='%4C %Z %{%b %d} %-15.15L (%?l?%4l&%4c?) %s'
set sort=threads
set sort_aux=last-date-received

# 'status color' can take up to 2 extra parameters

# color status foreground background [ regex [ num ]]

# 0 extra parameters
# Set the default color for the entire status line

color status blue white

# 1 extra parameter
# Set the color for a matching pattern
# color status foreground background regexp

# Highlight New, Deleted, or Flagged emails

color status brightred white '(New|Del|Flag):[0-9]+'

# Highlight mailbox ordering if it's different from the default
# First, highlight anything (*/*)

color status brightred default '\([^)]+/[^)]+\)'

# Then override the color for one specfic case

color status default   default '\(threads/last-date-received\)'

# 2 extra parameters
# Set the color for the nth submatch of a pattern
# color status foreground background regexp num

# Highlight the contents of the []s but not the [] themselves

color status red default '\[([^]]+)\]' 1

# The '1' refers to the first regex submatch, which is the inner
# part in ()s

# Highlight the mailbox

color status brightwhite default 'Mutt: ([^ ]+)' 1

# Search for 'Mutt: ' but only highlight what comes after it

# vim: syntax=muttrc
```

See Also
--------

-   NeoMutt project
-   Compile-Time Features
-   Regular Expressions
-   Patterns
-   [[index-color patch|index-color]]
-   Color command

Known Bugs
----------

None

Credits
-------

-   David Sterba \<dsterba@suse.cz\>
-   Thomas Glanzmann \<thomas@glanzmann.de\>
-   Kirill A. Shutemov \<kirill@shutemov.name\>
-   Richard Russon \<rich@flatcap.org\>

