Keywords Patch
==============

Labels/Tagging for emails

Patch
-----

To check if Mutt supports “Keywords”, look for “patch-keywords” in the
mutt version.

**Dependencies**
-   mutt-1.5.24

Introduction
------------

Unify label/keyword handling.

Since x-labels were added to mutt in 2000, a number of other approaches
to what we now call “tagging” have also emerged. One of them was even
made standard in RFC 2822. This update unifies the handling of all these
strategies.

We start by changing mutt's internal keyword storage from a single
string which may contain whitespace to a list of discrete keywords. This
has advantages for keyword completion as well as for portabilty among
varying "standards" for keyword storage. This may represent a
significant change for existing mutt users who have set x-labels
containing spaces, and should be regarded with suspicion. The advantages
are significant, though.

Next we allow mutt to parse keywords into this internal list from any of
the following headers: X-Label (freeform), X-Keywords (space-delimited),
X-Mozilla-Keys (space-delimited), and Keywords (RFC 2822,
comma-space-delimited). Mutt remembers which headers it sourced keywords
from, and can rewrite those headers when saving messages for
compatibility with the mailer of origin.

(X-Label was specified as freeform text by mutt, its only known
implementation. X-Labels have been used both as a “tagging” device,
probably with space delimiting, and as a “memo” field, where
space-delimited parsing would ruin the semantics of the memo. By default
mutt will not split X-Labels at all. Set \$xlabel\_delimiter if your
needs vary.)

Finally we add two booleans: \$keywords\_legacy=true and
\$keywords\_standard=FALSE. When \$keywords\_legacy is true, mutt will
always save keyword to whatever original header it came from. When
\$keywords\_standard=true, mutt will save to the Keywords: header. If
both are true mutt saves to both; if neither is true, mutt saves only to
legacy headers to avoid complete loss of keywords.

Overall this represents convergence path for all competing
labelling/tagging/keywording systems toward one that is specified by
RFC.

You can change or delete the X-Label: field within Mutt using the
edit-label command, bound to the y key by default. This works for tagged
messages, too.

Variables
---------

Functions
---------

**Keyword Functions**

Menus         | Default Key   | Function         | Description
------------- | ------------- | ---------------- | ------------------------------------------
index,pager   | y             | `<edit-label>`   | add, change, or delete a message's label

Commands
--------

Colors
------

None

Sort
----

**Keywords Sort**

Sort      | Description
--------- | ---------------
`label`   | Sort by label

Muttrc
------

See Also
--------

Known Bugs
----------

Credits
-------

-   David Champion \<dgc@uchicago.edu\>
-   Richard Russon \<rich@flatcap.org\>
