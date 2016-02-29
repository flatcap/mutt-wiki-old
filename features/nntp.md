NNTP Patch
==========

Talk to a Usenet news server

Patch
-----

To check if Mutt supports "NNTP", look for "+USE\_NNTP" in the mutt version.

**Dependencies**
-   mutt-1.5.24

Introduction
------------

Variables
---------

Functions
---------

**NNTP Functions**

| Menus                  | Default Key | Function                      | Description                                    |
|:-----------------------|:------------|:------------------------------|:-----------------------------------------------|
| browser,index          | y           | `<catchup>`                   | mark all articles in newsgroup as read         |
| index,pager            | i           | `<change-newsgroup>`          | open a different newsgroup                     |
| pager                  | X           | `<change-vfolder>`            | open a different virtual folder                |
| compose                | o           | `<edit-followup-to>`          | edit the Followup-To field                     |
| compose                | N           | `<edit-newsgroups>`           | edit the newsgroups list                       |
| compose                | x           | `<edit-x-comment-to>`         | edit the X-Comment-To field                    |
| pager                  | +           | `<entire-thread>`             | read entire thread of the current message      |
| attachment,index,pager | F           | `<followup-message>`          | followup to newsgroup                          |
| pager                  | \`          | `<modify-labels>`             | modify (notmuch) tags                          |
| index,pager            | P           | `<post-message>`              | post message to newsgroup                      |
| browser                | g           | `<reload-active>`             | load list of all newsgroups from NNTP server   |
| browser                | s           | `<subscribe>`                 | subscribe to current mbox (IMAP/NNTP only)     |
| browser                | S           | `<subscribe-pattern>`         | subscribe to newsgroups matching a pattern     |
| browser                | Y           | `<uncatchup>`                 | mark all articles in newsgroup as unread       |
| browser                | u           | `<unsubscribe>`               | unsubscribe from current mbox (IMAP/NNTP only) |
| browser                | U           | `<unsubscribe-pattern>`       | unsubscribe from newsgroups matching a pattern |
| index,pager            | Alt-i       | `<change-newsgroup-readonly>` | open a different newsgroup in read only mode   |
| attachment,index,pager | Alt-F       | `<forward-to-group>`          | forward to newsgroup                           |
| index                  | (none)      | `<get-children>`              | get all children of the current message        |
| index                  | Alt-G       | `<get-parent>`                | get parent of the current message              |
| index,pager            | (none)      | `<imap-fetch-mail>`           | force retrieval of mail from IMAP server       |
| index,pager            | (none)      | `<imap-logout-all>`           | logout from all IMAP servers                   |
| pager                  | (none)      | `<modify-labels-then-hide>`   | modify labeld and then hide message            |
| index                  | (none)      | `<reconstruct-thread>`        | reconstruct thread containing current message  |
| pager                  | Alt-X       | `<vfolder-from-query>`        | generate virtual folder from query             |
| index                  | Ctrl-G      | `<get-message>`               | get message with Message-Id                    |

Commands
--------

Colors
------

None

Sort
----

None

Muttrc
------

See Also
--------

Known Bugs
----------

Credits
-------

-   Vsevolod Volkov \<vvv@mutt.org.ua\>
-   Felix von Leitner \<leitner@fefe.de\>
-   Richard Russon \<rich@flatcap.org\>

