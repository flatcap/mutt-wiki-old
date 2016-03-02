Notmuch Patch
=============

Email search engine

Patch
-----

To check if Mutt supports "Notmuch", look for "+USE\_NOTMUCH" in the mutt version.

**Dependencies**
-   mutt-1.5.24
-   [[sidebar patch|sidebar]]
-   [[quasi-delete patch|quasi-delete]]
-   [[index-color patch|index-color]]
-   Notmuch libraries

Introduction
------------

Variables
---------

**Notmuch Variables**

| Name                | Type    | Default                                                           |
|:--------------------|:--------|:------------------------------------------------------------------|
| `nm_db_limit`       | number  | `0`                                                               |
| `nm_default_uri`    | string  | (empty)                                                           |
| `nm_exclude_tags`   | string  | (empty)                                                           |
| `nm_hidden_tags`    | string  | `unread,draft,flagged,passed,replied,attachment,signed,encrypted` |
| `nm_open_timeout`   | number  | `5`                                                               |
| `nm_query_type`     | string  | `messages`                                                        |
| `nm_record`         | boolean | `no`                                                              |
| `nm_record_tags`    | string  | (empty)                                                           |
| `nm_unread_tag`     | string  | `unread`                                                          |
| `vfolder_format`    | string  | `%6n(%6N) %f`                                                     |
| `virtual_spoolfile` | boolean | `no`                                                              |

Functions
---------

**Notmuch Functions**

| Menus       | Default Key | Function                    | Description                                    |
|:------------|:------------|:----------------------------|:-----------------------------------------------|
| index,pager | X           | `<change-vfolder>`          | open a different virtual folder                |
| index,pager | +           | `<entire-thread>`           | read entire thread of the current message      |
| index,pager | \`          | `<modify-labels>`           | modify (notmuch) tags                          |
| index,pager | (none)      | `<modify-labels-then-hide>` | modify labeld and then hide message            |
| index,pager | (none)      | `<sidebar-toggle>`          | toggle between mailboxes and virtual mailboxes |
| index,pager | Alt-X       | `<vfolder-from-query>`      | generate virtual folder from query             |

Commands
--------

**Notmuch Commands**

virtual-mailboxes description notmuch-URI { description notmuch-URI ...}
tag-transforms tag transformed-string { tag transformed-string ...}
tag-formats tag format-string { tag format-string ...}

Colors
------

Adds these to index-color patch:

**Index Colors**

| Object       | Pattern | Highlights                                   |
|:-------------|:--------|:---------------------------------------------|
| `index_tag`  | yes     | an individual message tag, %G, uses tag name |
| `index_tags` | no      | the transformed message tags, %g             |

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

-   Karel Zak \<kzak@redhat.com\>
-   Chris Mason \<clm@fb.com\>
-   Christoph Rissner \<cri@visotech.at\>
-   David Riebenbauer \<davrieb@liegesta.at\>
-   David Sterba \<dsterba@suse.cz\>
-   David Wilson \<dw@botanicus.net\>
-   Don Zickus \<dzickus@redhat.com\>
-   Eric Davis \<edavis@insanum.com\>
-   Jan Synacek \<jsynacek@redhat.com\>
-   Jeremiah C. Foster \<jeremiah@jeremiahfoster.com\>
-   Josh Poimboeuf \<jpoimboe@redhat.com\>
-   Kirill A. Shutemov \<kirill@shutemov.name\>
-   Luke Macken \<lmacken@redhat.com\>
-   Mantas Mikulėnas \<grawity@gmail.com\>
-   Patrick Brisbin \<pbrisbin@gmail.com\>
-   Philippe Le Brouster \<plb@nebkha.net\>
-   Raghavendra D Prabhu \<rprabhu@wnohang.net\>
-   Sami Farin \<hvtaifwkbgefbaei@gmail.com\>
-   Stefan Assmann \<sassmann@kpanic.de\>
-   Stefan Kuhn \<p_regius@gmx.ch\>
-   Tim Stoakes \<tim@stoakes.net\>
-   Vladimir Marek \<Vladimir.Marek@oracle.com\>
-   Víctor Manuel Jáquez Leal \<vjaquez@igalia.com\>
-   Richard Russon \<rich@flatcap.org\>

