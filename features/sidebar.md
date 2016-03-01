Sidebar Patch
=============

Overview of mailboxes

Patch
-----

To check if Mutt supports "Sidebar", look for "+USE\_SIDEBAR" in the mutt version.

**Dependencies**
-   mutt-1.5.24

Introduction
------------

Variables
---------

**Sidebar Variables**

| Name                    | Type    | Default                      |
|:------------------------|:--------|:-----------------------------|
| `sidebar_delim_chars`   | string  | `/.`                         |
| `sidebar_divider_char`  | string  | `|`                          |
| `sidebar_folder_indent` | boolean | `no`                         |
| `sidebar_format`        | string  | `%B%?F? [%F]?%* %?N?%N/?%4S` |
| `sidebar_indent_string` | string  | `  ` (two spaces)            |
| `sidebar_new_mail_only` | boolean | `no`                         |
| `sidebar_next_new_wrap` | boolean | `no`                         |
| `sidebar_refresh_time`  | number  | `60`                         |
| `sidebar_scrollbar`     | boolean | `no`                         |
| `sidebar_short_path`    | boolean | `no`                         |
| `sidebar_sort_method`   | enum    | `SORT_ORDER`                 |
| `sidebar_visible`       | boolean | `no`                         |
| `sidebar_whitelist`     | list    | (empty)                      |
| `sidebar_width`         | number  | `20`                         |

Functions
---------

**Sidebar Functions**

| Menus       | Default Key | Function                   | Description                                          |
|:------------|:------------|:---------------------------|:-----------------------------------------------------|
| index,pager | (none)      | `<sidebar-next>`           | Move the highlight to next mailbox                   |
| index,pager | (none)      | `<sidebar-next-new>`       | Move the highlight to next mailbox with new mail     |
| index,pager | (none)      | `<sidebar-open>`           | Open highlighted mailbox                             |
| index,pager | (none)      | `<sidebar-page-down>`      | Scroll the Sidebar down 1 page                       |
| index,pager | (none)      | `<sidebar-page-up>`        | Scroll the Sidebar up 1 page                         |
| index,pager | (none)      | `<sidebar-prev>`           | Move the highlight to previous mailbox               |
| index,pager | (none)      | `<sidebar-prev-new>`       | Move the highlight to previous mailbox with new mail |
| index,pager | (none)      | `<sidebar-toggle-visible>` | Make the Sidebar (in)visible                         |

Commands
--------

    sidebar\_whitelist mailbox [ mailbox... ]

Colors
------

**Sidebar Colors**

| Name                | Default Color  | Description                                                      |
|:--------------------|:---------------|:-----------------------------------------------------------------|
| `sidebar_divider`   | default        | The dividing line between the Sidebar and the Index/Pager panels |
| `sidebar_flagged`   | default        | Mailboxes containing flagged mail                                |
| `sidebar_highlight` | underline      | Cursor to select a mailbox                                       |
| `sidebar_indicator` | mutt indicator | The mailbox open in the Index panel                              |
| `sidebar_new`       | default        | Mailboxes containing new mail                                    |
| `sidebar_spoolfile` | default        | Mailbox that receives incoming mail                              |

If the
sidebar\_indicator
color isn't set, then the default Mutt indicator color will be used (the color used in the index panel).

Sort
----

**Sidebar Sort**

| Sort       | Description                |
|:-----------|:---------------------------|
| `alpha`    | Alphabetically by path     |
| `count`    | Total number of messages   |
| `flagged`  | Number of flagged messages |
| `name`     | Alphabetically by path     |
| `new`      | Number of new messages     |
| `path`     | Alphabetically by path     |
| `unsorted` | Do not resort the paths    |

Muttrc
------

```bash
# This is a complete list of sidebar-related configuration.

# --------------------------------------------------------------------------
# VARIABLES - shown with their default values
# --------------------------------------------------------------------------

# Should the Sidebar be shown?

set sidebar_visible = no

# How wide should the Sidebar be in screen columns?
# Note: Some characters, e.g. Chinese, take up two columns each.

set sidebar_width = 20

# Should the mailbox paths be abbreviated?

set sidebar_short_path = no

# When abbreviating mailbox path names, use any of these characters as path
# separators.  Only the part after the last separators will be shown.
# For file folders '/' is good.  For IMAP folders, often '.' is useful.

set sidebar_delim_chars = "/."

# If the mailbox path is abbreviated, should it be indented?

set sidebar_folder_indent = no

# Indent mailbox paths with this string.

set sidebar_indent_string = "  "

# Make the Sidebar only display mailboxes that contain new, or flagged,
# mail.

set sidebar_new_mail_only = no

# Any mailboxes that are whitelisted will always be visible, even if the
# sidebar_new_mail_only option is enabled.

sidebar_whitelist "/home/user/mailbox1"
sidebar_whitelist "/home/user/mailbox2"

# When searching for mailboxes containing new mail, should the search wrap
# around when it reaches the end of the list?

set sidebar_next_new_wrap = no

# The character to use as the divider between the Sidebar and the other Mutt
# panels.
# Note: Only the first character of this string is used.

set sidebar_divider_char = "|"

# Display the Sidebar mailboxes using this format string.

set sidebar_format = "%B%?F? [%F]?%* %?N?%N/?%4S"

# Sidebar will not refresh its list of mailboxes any more frequently than
# this number of seconds.  This will help reduce disk/network traffic.

set sidebar_refresh_time = 60

# Sort the mailboxes in the Sidebar using this method:
#       count    - total number of messages
#       flagged  - number of flagged messages
#       new      - number of new messages
#       path     - mailbox path
#       unsorted - do not sort the mailboxes

set sidebar_sort_method = "unsorted"

# --------------------------------------------------------------------------
# FUNCTIONS - shown with an example mapping
# --------------------------------------------------------------------------

# Move the highlight to the previous mailbox

bind index,pager \Cp sidebar-prev

# Move the highlight to the next mailbox

bind index,pager \Cn sidebar-next

# Open the highlighted mailbox

bind index,pager \Co sidebar-open

# Move the highlight to the previous page
# This is useful if you have a LOT of mailboxes.

bind index,pager <F3> sidebar-page-up

# Move the highlight to the next page
# This is useful if you have a LOT of mailboxes.

bind index,pager <F4> sidebar-page-down

# Move the highlight to the previous mailbox containing new, or flagged,
# mail.

bind index,pager <F5> sidebar-prev-new

# Move the highlight to the next mailbox containing new, or flagged, mail.

bind index,pager <F6> sidebar-next-new

# Toggle the visibility of the Sidebar.

bind index,pager B sidebar-toggle-visible

# --------------------------------------------------------------------------
# COLORS - some unpleasant examples are given
# --------------------------------------------------------------------------
# Note: All color operations are of the form:
#       color OBJECT FOREGROUND BACKGROUND

# Color of the current, open, mailbox
# Note: This is a general Mutt option which colors all selected items.

color indicator cyan black

# Color of the highlighted, but not open, mailbox.

color sidebar_highlight black color8

# Color of the divider separating the Sidebar from Mutt panels

color sidebar_divider color8 black

# Color to give mailboxes containing flagged mail

color sidebar_flagged red black

# Color to give mailboxes containing new mail

color sidebar_new green black

# --------------------------------------------------------------------------

# vim: syntax=muttrc
```

See Also
--------

-   Regular Expressions
-   Patterns
-   Color command
-   [[notmuch patch|notmuch]]

Known Bugs
----------

Unsorted isn't

Credits
-------

-   Justin Hibbits \<jrh29@po.cwru.edu\>
-   Thomer M. Gil \<mutt@thomer.com\>
-   David Sterba \<dsterba@suse.cz\>
-   Evgeni Golov \<evgeni@debian.org\>
-   Fabian Groffen \<grobian@gentoo.org\>
-   Jason DeTiberus \<jdetiber@redhat.com\>
-   Stefan Assmann \<sassmann@kpanic.de\>
-   Steve Kemp \<steve@steve.org.uk\>
-   Terry Chan \<tchan@lunar-linux.org\>
-   Tyler Earnest \<tylere@rne.st\>
-   Richard Russon \<rich@flatcap.org\>

