Index Color Patch
=================

Custom rules for theming the email index

Patch
-----

To check if Mutt supports "Index Color", look for "patch-index-color" in the mutt version.

**Dependencies**
-   mutt-1.5.24
-   [[status-color patch|status-color]]

Introduction
------------

The "index-color" patch allows you to specify colors for individual parts of the email index. e.g. Subject, Author, Flags.

First choose which part of the index you'd like to color. Then, if needed, pick a pattern to match.

Note: The pattern does not have to refer to the object you wish to color. e.g.

    color index_author red default "~smutt"

The author appears red when the subject (~s) contains "mutt".

Colors
------

All the colors default to `default`, i.e. unset.

The index objects can be themed using the `color` command. Some objects require a pattern.

    color index-object foreground background
    color index-object foreground background pattern

**Index Colors**

| Object            | Pattern | Highlights                                   |
|:------------------|:--------|:---------------------------------------------|
| `index`           | yes     | Entire index line                            |
| `index_author`    | yes     | Author name, %A %a %F %L %n                  |
| `index_collapsed` | no      | Number of messages in a collapsed thread, %M |
| `index_date`      | no      | Date field                                   |
| `index_flags`     | yes     | Message flags, %S %Z                         |
| `index_label`     | no      | Message label, %y %Y                         |
| `index_number`    | no      | Message number, %C                           |
| `index_size`      | no      | Message size, %c %l                          |
| `index_subject`   | yes     | Subject, %s                                  |

Muttrc
------

```bash
# Example Mutt config file for the 'index-color' feature.

# Entire index line

color index white black '.*'

# Author name, %A %a %F %L %n

# Give the author column a dark grey background

color index_author default color234 '.*'

# Highlight a particular from (~f)

color index_author brightyellow color234 '~fRay Charles'

# Message flags, %S %Z
# Highlight the flags for flagged (~F) emails

color index_flags default red '~F'

# Subject, %s
# Look for a particular subject (~s)

color index_subject brightcyan default '~s\(closes #[0-9]+\)'

# Number of messages in a collapsed thread, %M

color index_collapsed default brightblue

# Date field

color index_date green default

# Message label, %y %Y

color index_label default brightgreen

# Message number, %C

color index_number red default

# Message size, %c %l

color index_size cyan default

# vim: syntax=muttrc
```

See Also
--------

-   NeoMutt project
-   Regular Expressions
-   Patterns
-   $index\_format
-   Color command
-   [[Status-Color patch|status-color]]
-   [[Keywords patch|keywords]]

Known Bugs
----------

None

Credits
-------

-   Christian Aichinger \<Greek0@gmx.net\>
-   Christoph "Myon" Berg \<myon@debian.org\>
-   Elimar Riesebieter \<riesebie@lxtec.de\>
-   Eric Davis \<edavis@insanum.com\>
-   Vladimir Marek \<Vladimir.Marek@oracle.com\>
-   Richard Russon \<rich@flatcap.org\>

