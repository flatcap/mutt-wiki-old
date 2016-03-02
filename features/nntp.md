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

Reading news via NNTP

If compiled with *--enable-nntp* option, Mutt can read news from news server via NNTP. You can open a newsgroup with function \`\`change-newsgroup'' (default: \`\`i''). Default news server can be obtained from `$NNTPSERVER` environment variable or from `/etc/nntpserver` file. Like other news readers, info about subscribed newsgroups is saved in file by $newsrc variable. The variable $news\_cache\_dir can be used to point to a directory. Mutt will create a hierarchy of subdirectories named like the account and newsgroup the cache is for. Also the hierarchy is used to store header cache if Mutt was compiled with header cache support.

Variables
---------

**NNTP Variables**

| Name                    | Type    | Default                     |
|:------------------------|:--------|:----------------------------|
| `ask_follow_up`         | boolean | `no`                        |
| `ask_x_comment_to`      | boolean | `no`                        |
| `catchup_newsgroup`     | quad    | `ask-yes`                   |
| `followup_to_poster`    | quad    | `ask-yes`                   |
| `group_index_format`    | string  | `%4C %M%N %5s  %-45.45f %d` |
| `inews`                 | string  | (empty)                     |
| `mime_subject`          | boolean | `yes`                       |
| `newsgroups_charset`    | string  | `utf-8`                     |
| `newsrc`                | string  | `~/.newsrc`                 |
| `news_cache_dir`        | string  | `~/.mutt`                   |
| `news_server`           | string  | (empty)                     |
| `nntp_authenticators`   | string  | (empty)                     |
| `nntp_context`          | number  | `1000`                      |
| `nntp_listgroup`        | boolean | `yes`                       |
| `nntp_load_description` | boolean | `yes`                       |
| `nntp_pass`             | string  | (empty)                     |
| `nntp_poll`             | number  | `60`                        |
| `nntp_user`             | string  | (empty)                     |
| `post_moderated`        | quad    | `ask-yes`                   |
| `save_unsubscribed`     | boolean | `no`                        |
| `show_new_news`         | boolean | `yes`                       |
| `show_only_unread`      | boolean | `no`                        |
| `x_comment_to`          | boolean | `no`                        |

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

-   NeoMutt project
-   Compile-Time Features

Known Bugs
----------

Credits
-------

-   Vsevolod Volkov \<vvv@mutt.org.ua\>
-   Felix von Leitner \<leitner@fefe.de\>
-   Richard Russon \<rich@flatcap.org\>

