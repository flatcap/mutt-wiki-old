Trash Folder Patch
==================

Automatically move "deleted" emails to a trash bin

Patch
-----

To check if Mutt supports "Trash Folder", look for "patch-trash" in the mutt version.

If IMAP is enabled, this patch will use it

**Dependencies**
-   mutt-1.5.24
-   IMAP support

Introduction
------------

In Mutt, when you "delete" an email it is first marked deleted. The email isn't really gone until \<sync-mailbox\> is called. This happens when the user leaves the folder, or the function is called manually.

After `<sync-mailbox>` has been called the email is gone forever.

The $trash variable defines a folder in which to keep old emails. As before, first you mark emails for deletion. When \<sync-mailbox\> is called the emails are moved to the trash folder.

The `$trash` path can be either a full directory, or be relative to the $folder variable, like the `mailboxes` command.

> **Note**
>
> Emails deleted from the trash folder are gone forever.

Variables
---------

**Trash Variables**

| Name  | Type   | Default |
|:------|:-------|:--------|
| trash | string | (none)  |

Functions
---------

**Trash Functions**

| Menus       | Default Key | Function          | Description                                                 |
|:------------|:------------|:------------------|:------------------------------------------------------------|
| index,pager | (none)      | `<purge-message>` | really delete the current entry, bypassing the trash folder |

Muttrc
------

```bash
# Example Mutt config file for the 'trash' feature.

# This feature defines a new 'trash' folder.
# When mail is deleted it will be moved to this folder.

# Folder in which to put deleted emails

set trash="+Trash"
set trash="/home/flatcap/Mail/Trash"

# The default delete key 'd' will move an email to the 'trash' folder
# Bind 'D' to REALLY delete an email
bind index D purge-message

# Note: Deleting emails from the 'trash' folder will REALLY delete them.

# vim: syntax=muttrc
```

See Also
--------

-   NeoMutt project
-   folder-hook

Known Bugs
----------

None

Credits
-------

-   Cedric Duval \<cedricduval@free.fr\>
-   Benjamin Kuperman \<kuperman@acm.org\>
-   Paul Miller \<paul@voltar.org\>
-   Richard Russon \<rich@flatcap.org\>

