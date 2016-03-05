Nested If Patch
===============

Allow complex nested conditions in format strings

Patch
-----

To check if Mutt supports "Nested If", look for "patch-nested-if" in the mutt version.

**Dependencies**
-   mutt-1.5.24

Introduction
------------

Mutt's format strings can contain embedded if-then-else conditions. They are of the form:

    %?VAR?TRUE&FALSE?

If the variable "VAR" has a value greater than zero, print the "TRUE" string, otherwise print the "FALSE" string.

e.g.
%?S?Size: %S&Empty?
Which can be read as:

    if (%S > 0) {
        print "Size: %S"
    } else {
        print "Empty"
    }


These conditions are useful, but in Mutt they cannot be nested within one another. This patch uses the notation `%<VAR?TRUE&FALSE>` and allows them to be nested.

The `%<...>` notation was used to format the current local time. but that's not really very useful since mutt has no means of refreshing the screen periodically.

A simple nested condition might be: (Some whitespace has been introduced for clarity)

    %<x? %<y? XY & X > & %<y? Y & NONE > >  Conditions
         %<y? XY & X >                      x>0
              XY                            x>0,y>0
                   X                        x>0,y=0


    %<x? %<y? XY & X > & %<y? Y & NONE > >  Conditions
                         %<y? Y & NONE >    x=0
                              Y             x=0,y>0
                                  NONE      x=0,y=0


Equivalent to:

    if (x > 0) {
        if (y > 0) {
            print 'XY'
        } else {
            print 'X'
        }
    } else {
        if (y > 0) {
            print 'Y'
        } else {
            print 'NONE'
        }
    }


Examples:

    set index_format='%4C %Z %{%b %d} %-25.25n %s%> %<M?%M Msgs &%<l?%l Lines&%c Bytes>>'

    if a thread is folded
        display the number of messages (%M)
    else if we know how many lines in the message
        display lines in message (%l)
    else
        display the size of the message in bytes (%c)


    set index_format='%4C %Z %{%b %d} %-25.25n %<M?[%M] %s&%s%* %<l?%l&%c>>'

    if a thread is folded
        display the number of messages (%M)
        display the subject (%s)
    else if we know how many lines in the message
        display lines in message (%l)
    else
        display the size of the message in bytes (%c)


Variables
---------

The
nested-if
patch doesn't have any config of its own. It modifies the behavior of the format strings.

Muttrc
------

```bash
# Example Mutt config file for the 'nested-if' feature.

# This patch uses the format: '%<VAR?TRUE&FALSE>' for conditional
# format strings that can be nested.

# Example 1
# if a thread is folded
#       display the number of messages (%M)
# else if we know how many lines in the message
#       display lines in message (%l)
# else display the size of the message in bytes (%c)
set index_format='%4C %Z %{%b %d} %-25.25n %s%> %<M?%M Msgs &%<l?%l Lines&%c Bytes>>'

# Example 2
# if a thread is folded
#       display the number of messages (%M)
#       display the subject (%s)
# else if we know how many lines in the message
#       display lines in message (%l)
# else
#       display the size of the message in bytes (%c)
set index_format='%4C %Z %{%b %d} %-25.25n %<M?[%M] %s&%s%* %<l?%l&%c>>'

# vim: syntax=muttrc
```

See Also
--------

-   NeoMutt project
-   [[cond-date patch|cond-date]]
-   $index\_format
-   $status\_format

Known Bugs
----------

Patch overwrites $\<fmt\> handler in
$index\_format

Credits
-------

-   David Champion \<dgc@uchicago.edu\>
-   Richard Russon \<rich@flatcap.org\>

