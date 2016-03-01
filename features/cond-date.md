Conditional Dates Patch
=======================

Use rules to choose date format

Patch
-----

To check if Mutt supports "Conditional Dates", look for "patch-cond-date" in the mutt version.

**Dependencies**
-   mutt-1.5.24
-   [[nested-if patch|nested-if]]

Introduction
------------

The "cond-date" patch allows you to construct $index\_format expressions based on the age of the email.

Mutt's default `$index_format` displays email dates in the form: abbreviated-month day-of-month — "Jan 14".

The format is configurable but only per-mailbox. This patch allows you to configure the display depending on the age of the email.

**Potential Formatting Scheme**

| Email Sent        | Format  | Example |
|:------------------|:--------|:--------|
| Today             | `%H:%M` | 13:23   |
| This Month        | `%a %d` | Thu 17  |
| This Year         | `%b %d` | Dec 10  |
| Older than 1 Year | `%m/%y` | 06/14   |

For an explanation of the date formatting strings, see `strftime(3).`

By carefully picking your formats, the dates can remain unambiguous and compact.

Mutt's conditional format strings have the form: (whitespace introduced for clarity)

    %? TEST ? TRUE & FALSE ?

The examples below use the test "%[" — the date of the message in the local timezone. They will also work with "%(" — the local time that the message arrived.

The date tests are of the form:

    %[nX? TRUE & FALSE ?

-   "n" is an optional count (defaults to 1 if missing)
-   "X" is the time period

**Date Formatting Codes**

| Letter | Time Period |
|:-------|:------------|
| y      | Years       |
| m      | Months      |
| w      | Weeks       |
| d      | Days        |
| H      | Hours       |
| M      | Minutes     |

**Date Tests**

| Test   | Meaning              |
|:-------|:---------------------|
| `%[y`  | This year            |
| `%[1y` | This year            |
| `%[6m` | In the last 6 months |
| `%[w`  | This week            |
| `%[d`  | Today                |
| `%[4H` | In the last 4 hours  |

### Example 1

We start with a one-condition test.

**Example 1**

| Test   | Date Range | Format String | Example    |
|:-------|:-----------|:--------------|:-----------|
| `%[1m` | This month | `%[%b %d]`    | Dec 10     |
|        | Older      | `%[%Y-%m-%d]` | 2015-04-23 |

The $index\_format string would contain:

    %?[1m?%[%b %d]&%[%Y-%m-%d]?

Reparsed a little, for clarity, you can see the test condition and the two format strings.

    %?[1m?        &           ?
          %[%b %d] %[%Y-%m-%d]

### Example 2

This example contains three test conditions and four date formats.

**Example 2**

| Test  | Date Range | Format String | Example |
|:------|:-----------|:--------------|:--------|
| `%[d` | Today      | `%[%H:%M ] `  | 12:34   |
| `%[m` | This month | `%[%a %d]`    | Thu 12  |
| `%[y` | This year  | `%[%b %d]`    | Dec 10  |
|       | Older      | `%[%m/%y ]`   | 06/15   |

The $index\_format string would contain:

    %<[y?%<[m?%<[d?%[%H:%M ]&%[%a %d]>&%[%b %d]>&%[%m/%y ]>

Reparsed a little, for clarity, you can see the test conditions and the four format strings.

    %<[y?                                       &%[%m/%y ]>  Older
         %<[m?                        &%[%b %d]>             This year
              %<[d?         &%[%a %d]>                       This month
                   %[%H:%M ]                                 Today

This a another view of the same example, with some whitespace for clarity.

    %<[y? %<[m? %<[d? AAA & BBB > & CCC > & DDD >

    AAA = %[%H:%M ]
    BBB = %[%a %d]
    CCC = %[%b %d]
    DDD = %[%m/%y ]


Variables
---------

The "cond-date" patch doesn't have any config of its own. It modifies the behavior of the format strings.

Muttrc
------

```bash
# Example Mutt config file for the 'index-color' feature.
#
# The default index_format is:
#       '%4C %Z %{%b %d} %-15.15L (%?l?%4l&%4c?) %s'
#
# We replace the date field '%{%b %d}', giving:

set index_format='%4C %Z %<[y?%<[m?%<[d?%[%H:%M ]&%[%a %d]>&%[%b %d]>&%[%m/%y ]> %-15.15L (%?l?%4l&%4c?) %s'

# Test  Date Range  Format String  Example
# --------------------------------------------
# %[d   Today       %[%H:%M ]      12:34
# %[m   This month  %[%a %d]       Thu 12
# %[y   This year   %[%b %d]       Dec 10
# -     Older       %[%m/%y ]      06/15

# vim: syntax=muttrc
```

See Also
--------

-   [[nested-if patch|nested-if]]
-   `strftime(3)`

Known Bugs
----------

Date parsing doesn't quite do what you expect. "1w" doesn't mean the "in the last 7 days", but "*this* week". This doesn't match the normal Mutt behaviour: for example `~d>1w` means emails dated in the last 7 days.

Credits
-------

-   Aaron Schrab \<aaron@schrab.com\>
-   Eric Davis \<edavis@insanum.com\>
-   Richard Russon \<rich@flatcap.org\>

