Compressed Folders Patch
========================

Read from/write to compressed mailboxes

Patch
-----

To check if Mutt supports "Compress Folders", look for "+USE\_COMPRESSED" in the mutt version.

**Dependencies**
-   mutt-1.5.24

Introduction
------------

The Compressed Folder patch allows Mutt to read mailbox files that are compressed. The patch adds three hooks to Mutt: `open-hook`, `close-hook` and `append-hook` (which is optional).

The Compressed Folder patch isn't limited to compressed files. It works well with encrypted files, too. In fact, if you can create a program/script to convert to and from your format, then Mutt can read it.

There are some examples of both compressed and encrypted files, later. For now, the documentation will just concentrate on compressed files.

There are three hooks defined ( open-hook, close-hookand append-hook) which define commands to uncompress and compress a folder and to append messages to an existing compressed folder respectively.

Commands
--------

open-hook pattern shell-command
close-hook pattern shell-command
append-hook pattern shell-command

> **Note**
>
> The command should return a non-zero exit status if it fails.

> **Note**
>
> The command should not delete any files.

The shell-command must contain two placeholders for filenames: `%f` and `%t`. These represent "from" and "to" filenames. It's a good idea to put quotes around these placeholders.

If you need the exact string "%f" or "%t" in your command, simply double up the "%" character, e.g. "%%f" or "%%t".

You do not have to provide all of the hooks.

| Open | Close | Append | Effect                                                                             | Useful if                                         |
|:-----|:------|:-------|:-----------------------------------------------------------------------------------|:--------------------------------------------------|
| Open |       |        | Folder is readonly                                                                 | The folder is just a backup                       |
| Open | Close |        | Folder is read/write, but the entire folder must be written if anything is changed | Your compression format doesn't support appending |
| Open | Close | Append | Folder is read/write and emails can be efficiently added to the end                | Your compression format supports appending        |
| Open |       | Append | Folder is readonly, but can be appended to                                         | You want to store emails, but never change them   |

### Example 1

    open-hook '\.gz$' "gzip -cd '%f' > '%t'"

When Mutt is asked to open a file, it first checks if there's a matching `open-hook`. The hook, above, will match any files whose name ends ".gz". That causes Mutt to run the `gzip` command to create a readable version.

### Open a compressed mailbox for reading

    open-hook regexp shell-command

    open-hook '\.gz$' "gzip -cd '%f' > '%t'"

### Write a compressed mailbox

    close-hook regexp shell-command

    close-hook '\.gz$' "gzip -c '%t' > '%f'"

This is used to close the folder that was open with the
open-hook
command after some changes were made to it. Temporary folder in this case is the folder previously produced by the
open-hook
command.
close-hook
is not called when you exit from the folder if the folder was not changed.

### Append a message to a compressed mailbox

append-hook regexp shell-command append-hook '\\.gz$' "gzip -c '%t' \>\> '%f'"
Usage:

When
append-hook
is used, the folder is not opened, which saves time, but this means that we can not find out what the folder type is. Thus the default (
$mbox\_type
) type is always supposed (i.e. this is the format used for the temporary folder). If the file does not exist when you save to it,
close-hook
is called, and not
append-hook
.
append-hook
is only for appending to existing folders. If the
command
is empty, this operation is disabled for this file type. In this case, the folder will be open and closed again (using
open-hook
and
close-hook
respectively) each time you will add to it.

### empty files

Note that Mutt will only try to use hooks if the file is not in one of the accepted formats. In particular, if the file is empty, mutt supposes it is not compressed. This is important because it allows the use of programs that do not have well defined extensions. Just use
.
as a regexp. But this may be surprising if your compressing script produces empty files. In this situation, unset
$save\_empty
, so that the compressed file will be removed if you delete all of the messages.

### security

Note:
the folder is temporary stored decrypted in the /tmp directory, where it can be read by your system administrator. So think about the security aspects of this.
Please note, that PGP does not support appending to an encrypted folder, so there is no append-hook defined.

In addition, the user can provide a script that gets a folder in an accepted format and appends its context to the folder in the user-defined format, which may be faster than converting the entire folder to the accepted format, appending to it and converting back to the user-defined format.

Muttrc
------

```bash
# Example Mutt config file for the 'compressed folders' feature.

# This feature adds three hooks to Mutt which allow it to
# work with compressed, or encrypted, mailboxes.

# The hooks are of the form:
#       open-hook   regexp "shell-command"
#       close-hook  regexp "shell-command"
#       append-hook regexp "shell-command"

# The 'append-hook' is optional.

# Hander for gzip compressed mailboxes

open-hook   '\.gz$'  "gzip -cd  '%f' >  '%t'"
close-hook  '\.gz$'  "gzip -c   '%t' >  '%f'"
append-hook '\.gz$'  "gzip -c   '%t' >> '%f'"

# Hander for bzip2 compressed mailboxes

open-hook   '\.bz2$' "bzip2 -cd '%f' >  '%t'"
close-hook  '\.bz2$' "bzip2 -c  '%t' >  '%f'"
append-hook '\.bz2$' "bzip2 -c  '%t' >> '%f'"

# Hander for xz compressed mailboxes

open-hook   '\.xz$'  "xz    -cd '%f' >  '%t'"
close-hook  '\.xz$'  "xz    -c  '%t' >  '%f'"
append-hook '\.xz$'  "xz    -c  '%t' >> '%f'"

# Hander for pgp encrypted mailboxes

open-hook   '\.pgp$' "pgp -f < '%f' > '%t'"
close-hook  '\.pgp$' "pgp -fe YourPgpUserIdOrKeyId < '%t' > '%f'"

# Hander for gpg encrypted mailboxes

open-hook   '\.gpg$' "gpg --decrypt < '%f' > '%t'"
close-hook  '\.gpg$' "gpg --encrypt --recipient YourGpgUserIdOrKeyId < '%t' > '%f'"

# vim: syntax=muttrc
```

See Also
--------

-   $folder\_hook

Known Bugs
----------

-   Patch cannot deal with filenames that contains quotes/apostrophes.

Credits
-------

-   Roland Rosenfeld \<roland@spinnaker.de\>
-   Alain Penders \<Alain@Finale-Dev.com\>
-   Christoph "Myon" Berg \<myon@debian.org\>
-   Evgeni Golov \<evgeni@debian.org\>
-   Richard Russon \<rich@flatcap.org\>

