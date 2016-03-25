Sidebar
-------

The Sidebar shows a list of all your mailboxes. The list can be turned
on and off, it can be themed and the list style can be configured.

This part of the manual is suitable for beginners. If you already know
Mutt you could skip ahead to the main [Sidebar guide](sidebar). If you
just want to get started, you could use the sample [Sidebar
muttrc](sidebar#muttrc).

This version of Sidebar is based on Terry Chan's [2015-11-11
release](http://www.lunar-linux.org/mutt-sidebar/). It contains many
**[new features](#features)**, lots of **[bugfixes](#bug-fixes)** and a generous
helping of **new documentation** which you are already reading.

To check if Mutt supports “Sidebar”, look for the string `+USE_SIDEBAR`
in the mutt version.

```bash
mutt -v
```

**Let's turn on the Sidebar:**

```bash
set sidebar_visible
```

You will see something like this. A list of mailboxes on the left. A
list of emails, from the selected mailbox, on the right.

![sidebar example 1](intro/si1.png)

This user has four mailboxes: “Fruit”, “Cars”, “Animals” and “Seas”.

The current, open, mailbox is “Fruit”. We can also see information about
the other mailboxes. For example: The “Animals” mailbox contains, 1
flagged email, 2 new emails out of a total of 6 emails.

### Navigation

The Sidebar adds some new [functions](sidebar#functions) to Mutt.

The user pressed the “c” key to `<change-folder>` to the “Animals”
mailbox. The Sidebar automatically updated the indicator to match.

![sidebar example 2](intro/si2.png)

Let's map some functions:

```bash
bind index,pager \CP sidebar-prev       # Ctrl-Shift-P - Previous Mailbox
bind index,pager \CN sidebar-next       # Ctrl-Shift-N - Next Mailbox
bind index,pager \CO sidebar-open       # Ctrl-Shift-O - Open Highlighted Mailbox
```

Press “Ctrl-Shift-N” (Next mailbox) twice will move the Sidebar
**highlight** to down to the “Seas” mailbox.

![sidebar example 3](intro/si3.png)

> **Note**
>
> Functions \<sidebar-next\> and \<sidebar-prev\> move the Sidebar highlight.
> They do not change the open mailbox.

Press “Ctrl-Shift-O” (`<sidebar-open>`) to open the highlighted mailbox.

![sidebar example 4](intro/si4.png)

### Features

The Sidebar shows a list of mailboxes in a panel.

Everything about the Sidebar can be configured.

[**State of the Sidebar**](#sidebar-basics)
-   Visibility
-   Width

[**Which mailboxes are displayed**](#limiting-the-number-of-mailboxes)
-   Display all
-   Limit to mailboxes with new mail
-   Whitelist mailboxes to display always

[**The order in which mailboxes are displayed**](sidebar#sort)
-   Unsorted (order of mailboxes commands)
-   Sorted alphabetically
-   Sorted by number of new mails

[**Color**](#colors)
-   Sidebar indicators and divider
-   Mailboxes depending on their type
-   Mailboxes depending on their contents

[**Key bindings**](sidebar#functions)
-   Hide/Unhide the Sidebar
-   Select previous/next mailbox
-   Select previous/next mailbox with new mail
-   Page up/down through a list of mailboxes

**Misc**
-   [Formatting string for mailbox](#sidebar-format-string)
-   [Wraparound searching](sidebar#variables)
-   [Flexible mailbox abbreviations](#abbreviating-mailbox-names)
-   Support for Unicode mailbox names (utf-8)

### Display

Everything about the Sidebar can be configured.

**For a quick reference:**
-   [Sidebar variables to set](sidebar#variables)
-   [Sidebar colors to apply](sidebar#colors)
-   [Sidebar sort methods](sidebar#sort)

#### Sidebar Basics

The most important variable is `$sidebar_visible`. You can set this in
your “muttrc”, or bind a key to the function `<sidebar-toggle-visible>`.

```bash
set sidebar_visible                         # Make the Sidebar visible by default
bind index,pager B sidebar-toggle-visible   # Use 'B' to switch the Sidebar on and off
```

Next, decide how wide you want the Sidebar to be. 25 characters might be
enough for the mailbox name and some numbers. Remember, you can
hide/show the Sidebar at the press of button.

Finally, you might want to change the divider character. By default,
Sidebar draws an ASCII line between it and the Index panel If your
terminal supports it, you can use a Unicode line-drawing character.

```bash
set sidebar_width = 25                  # Plenty of space
set sidebar_divider_char = '│'          # Pretty line-drawing character
```

#### Sidebar Format String

`$sidebar_format` allows you to customize the Sidebar display. For an
introduction, read the Mutt manual about `index-format` including the section
about 'conditionals'.

The default value is `%B%?F? [%F]?%* %?N?%N/?%S`

-   `%B` - Mailbox name
-   `%?F? [%F]?` - If flagged emails `[%F]`, otherwise nothing
-   `%* ` - Pad with spaces
-   `%?N?%N/?` - If new emails `%N/`, otherwise nothing
-   `%S` - Total number of emails

**sidebar\_format**

| Format | Notes | Description                                                                                                            |
|:-------|:------|:-----------------------------------------------------------------------------------------------------------------------|
| %B     |       | Name of the mailbox                                                                                                    |
| %S     | \*    | Size of mailbox (total number of messages)                                                                             |
| %N     | \*    | Number of New messages in the mailbox                                                                                  |
| %F     | \*    | Number of Flagged messages in the mailbox                                                                              |
| %!     |       | “!”: one flagged message; “!!”: two flagged messages; “n!”: n flagged messages (for n \> 2). Otherwise prints nothing. |
| %d     | \* ‡  | Number of deleted messages                                                                                             |
| %L     | \* ‡  | Number of messages after limiting                                                                                      |
| %t     | \* ‡  | Number of tagged messages                                                                                              |
| %\>X   |       | Right justify the rest of the string and pad with “X”                                                                  |
| %|X    |       | Pad to the end of the line with “X”                                                                                    |
| %\*X   |       | Soft-fill with character “X”as pad                                                                                     |

\* = Can be optionally printed if nonzero
‡ = Only applicable to the current folder

Here are some examples. They show the number of (F)lagged, (N)ew and
(S)ize.

**sidebar\_format**

| Format                      | Example                   |
|:----------------------------|:--------------------------|
| `%B%?F? [%F]?%* %?N?%N/?%S` | `mailbox [F]         N/S` |
| `%B%* %F:%N:%S`             | `mailbox           F:N:S` |
| `%B %?N?(%N)?%* %S`         | `mailbox (N)           S` |
| `%B%* ?F?%F/?%N`            | `mailbox             F/S` |

#### Abbreviating Mailbox Names

`$sidebar_delim_chars` tells Sidebar how to split up mailbox paths. For
local directories use “/”; for IMAP folders use “.”

##### Example 1

This example works well if your mailboxes have unique names after the
last separator.

Add some mailboxes of diffent depths.

```bash
set folder="~/mail"
mailboxes =fruit/apple          =fruit/banana          =fruit/cherry
mailboxes =water/sea/sicily     =water/sea/archipelago =water/sea/sibuyan
mailboxes =water/ocean/atlantic =water/ocean/pacific   =water/ocean/arctic
```

Shorten the names:

```bash
set sidebar_short_path                  # Shorten mailbox names
set sidebar_delim_chars="/"             # Delete everything up to the last / character
```

The screenshot below shows what the Sidebar would look like **before** and
**after** shortening.

```
|fruit/apple                            |apple
|fruit/banana                           |banana
|fruit/cherry                           |cherry
|water/sea/sicily                       |sicily
|water/sea/archipelago                  |archipelago
|water/sea/sibuyan                      |sibuyan
|water/ocean/atlantic                   |atlantic
|water/ocean/pacific                    |pacific
|water/ocean/arctic                     |arctic
```

##### Example 2

This example works well if you have lots of mailboxes which are arranged
in a tree.

Add some mailboxes of diffent depths.

```bash
set folder="~/mail"
mailboxes =fruit
mailboxes =fruit/apple =fruit/banana =fruit/cherry
mailboxes =water
mailboxes =water/sea
mailboxes =water/sea/sicily =water/sea/archipelago =water/sea/sibuyan
mailboxes =water/ocean
mailboxes =water/ocean/atlantic =water/ocean/pacific =water/ocean/arctic
```

Shorten the names:

```bash
set sidebar_short_path                  # Shorten mailbox names
set sidebar_delim_chars="/"             # Delete everything up to the last / character
set sidebar_folder_indent               # Indent folders whose names we've shortened
set sidebar_indent_string="  "          # Indent with two spaces
```

The screenshot below shows what the Sidebar would look like **before** and
**after** shortening.

```
|fruit                                  |fruit
|fruit/apple                            |  apple
|fruit/banana                           |  banana
|fruit/cherry                           |  cherry
|water                                  |water
|water/sea                              |  sea
|water/sea/sicily                       |    sicily
|water/sea/archipelago                  |    archipelago
|water/sea/sibuyan                      |    sibuyan
|water/ocean                            |  ocean
|water/ocean/atlantic                   |    atlantic
|water/ocean/pacific                    |    pacific
|water/ocean/arctic                     |    arctic
```

Sometimes, it will be necessary to add mailboxes, that you don't use, to
fill in part of the tree. This will trade vertical space for horizonal
space (but it looks good).

#### Limiting the Number of Mailboxes

If you have a lot of mailboxes, sometimes it can be useful to hide the
ones you aren't using. `$sidebar_new_mail_only` tells Sidebar to only
show mailboxes that contain new, or flagged, email.

If you want some mailboxes to be always visible, then use the
`sidebar_whitelist` command. It takes a list of mailboxes as parameters.

```bash
set sidebar_new_mail_only               # Only mailboxes with new/flagged email
sidebar_whitelist fruit fruit/apple     # Always display these two mailboxes
```

### Colors

Here is a sample color scheme:

```bash
color sidebar_indicator default color17         # Dark blue background
color sidebar_highlight white   color238        # Grey background
color sidebar_spoolfile yellow  default         # Yellow
color sidebar_new       green   default         # Green
color sidebar_flagged   red     default         # Red
color sidebar_divider   color8  default         # Dark grey
```

There is a priority order when coloring Sidebar mailboxes. e.g. If a
mailbox has new mail it will have the `sidebar_new` color, even if it
also contains flagged mails.

| Priority | Color               | Description                                       |
|:---------|:------------------- |:--------------------------------------------------|
| Highest  | `sidebar_indicator` | Mailbox is open                                   |
|          | `sidebar_highlight` | Mailbox is highlighed                             |
|          | `sidebar_spoolfile` | Mailbox is the spoolfile (receives incoming mail) |
|          | `sidebar_new`       | Mailbox contains new mail                         |
|          | `sidebar_flagged`   | Mailbox contains flagged mail                     |
| Lowest   | (None)              | Mailbox does not match above                      |

### Bug-fixes

If you haven't used Sidebar before, you can ignore this section.

These bugs have been fixed since the previous Sidebar release:
2015-11-11.

-   Fix bug when starting in compose mode
-   Fix bug with empty sidebar\_divider\_char string
-   Fix bug with header wrapping
-   Correctly handle utf8 character sequences
-   Fix a bug in mh\_buffy\_update
-   Fix refresh -- time overflowed short
-   Protect against empty format strings
-   Limit Sidebar width to COLS
-   Handle unmailboxes \* safely
-   Refresh Sidebar after timeout

### Config Changes

If you haven't used Sidebar before, you can ignore this section.

Some of the Sidebar config has been changed to make its meaning clearer.
These changes have been made since the previous Sidebar release:
2015-11-11.

| Old Name                | New Name                 |
|:------------------------|:-------------------------|
| `$sidebar_delim`        | `$sidebar_divider_char`  |
| `$sidebar_folderindent` | `$sidebar_folder_indent` |
| `$sidebar_indentstr`    | `$sidebar_indent_string` |
| `$sidebar_newmail_only` | `$sidebar_new_mail_only` |
| `$sidebar_refresh`      | `$sidebar_refresh_time`  |
| `$sidebar_shortpath`    | `$sidebar_short_path`    |
| `$sidebar_sort`         | `$sidebar_sort_method`   |
| `<sidebar-scroll-down>` | `<sidebar-page-down>`    |
| `<sidebar-scroll-up>`   | `<sidebar-page-up>`      |


