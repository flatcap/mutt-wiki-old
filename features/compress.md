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

The Compressed Folder patch allows Mutt to read mailbox files that are compressed. But it isn't limited to compressed files. It works well with encrypted files, too. In fact, if you can create a program/script to convert to and from your format, then Mutt can read it.

The patch adds three hooks to Mutt: `open-hook`, `close-hook` and `append-hook`. They define commands to: uncompress a file; compress a file; append messages to an already compressed file.

There are some examples of both compressed and encrypted files, later. For now, the documentation will just concentrate on compressed files.

Commands
--------

    open-hook   pattern shell-command
    close-hook  pattern shell-command
    append-hook pattern shell-command

The shell-command must contain two placeholders for filenames: `%f` and `%t`. These represent "from" and "to" filenames. It's a good idea to put quotes around these placeholders.

If you need the exact string "%f" or "%t" in your command, simply double up the "%" character, e.g. "%%f" or "%%t".

**Not all Hooks are Required**

| Open | Close | Append | Effect                                                                             | Useful if                                         |
|:-----|:------|:-------|:-----------------------------------------------------------------------------------|:--------------------------------------------------|
| Open | -     | -      | Folder is readonly                                                                 | The folder is just a backup                       |
| Open | Close | -      | Folder is read/write, but the entire folder must be written if anything is changed | Your compression format doesn't support appending |
| Open | Close | Append | Folder is read/write and emails can be efficiently added to the end                | Your compression format supports appending        |
| Open | -     | Append | Folder is readonly, but can be appended to                                         | You want to store emails, but never change them   |

> **Note**
>
> The command:
> -   should return a non-zero exit status on failure
> -   should not delete any files

### Read from compressed mailbox

    open-hook regexp shell-command

If Mutt is unable to open a file, it then looks for `open-hook` that matches the filename.

If your compression program doesn't have a well-defined extension, then you can use `.` as the regexp.

#### Example of open-hook

    open-hook '\.gz$' "gzip -cd '%f' > '%t'"

-   Mutt finds a file, "example.gz", that it can't read
-   Mutt has an `open-hook` whose regexp matches the filename: `\.gz$`
-   Mutt uses the command `gzip -cd` to create a temporary file that it *can* read

### Write to a compressed mailbox

    close-hook regexp shell-command

When Mutt has finished with a compressed mail folder, it will look for a matching `close-hook` to recompress the file. This hook is optional.

> **Note**
>
> If the folder has not been modifed, the
> close-hook
> will not be called.

#### Example of close-hook

    close-hook '\.gz$' "gzip -c '%t' > '%f'"

-   Mutt has finished with a folder, "example.gz", that it opened with `open-hook`
-   The folder has been modified
-   Mutt has a `close-hook` whose regexp matches the filename: `\.gz$`
-   Mutt uses the command `gzip -c` to create a new compressed file

### Append to a compressed mailbox

    append-hook regexp shell-command

When Mutt wants to append an email to a compressed mail folder, it will look for a matching `append-hook`. This hook is optional.

Using the `append-hook` will save time, but Mutt won't be able to determine the type of the mail folder inside the compressed file.

Mutt will *assume* the type to be that of the `$mbox_type` variable. Mutt also uses this type for temporary files.

Mutt will only use the `append-hook` for existing files. The `close-hook` will be used for empty, or missing files.

#### Example of append-hook

    append-hook '\.gz$' "gzip -c '%t' >> '%f'"

-   Mutt wants to append an email to a folder, "example.gz", that it opened with `open-hook`
-   Mutt has an `append-hook` whose regexp matches the filename: `\.gz$`
-   Mutt knows the mailbox type from the `$mbox` variable
-   Mutt uses the command `gzip -c` to append to an existing compressed file

### Empty Files

Mutt assumes that an empty file is not compressed. In this situation, unset $save\_empty, so that the compressed file will be removed if you delete all of the messages.

### Security

Encrypted files are decrypted into temporary files which are stored in the $tmpdir directory. This could be a security risk.

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
# PGP does not support appending to an encrypted file

open-hook   '\.pgp$' "pgp -f < '%f' > '%t'"
close-hook  '\.pgp$' "pgp -fe YourPgpUserIdOrKeyId < '%t' > '%f'"

# Hander for gpg encrypted mailboxes
# gpg does not support appending to an encrypted file

open-hook   '\.gpg$' "gpg --decrypt < '%f' > '%t'"
close-hook  '\.gpg$' "gpg --encrypt --recipient YourGpgUserIdOrKeyId < '%t' > '%f'"

# vim: syntax=muttrc
```

See Also
--------

-   NeoMutt project
-   Compile-Time Features
-   Regular Expressions
-   $tmpdir
-   $mbox\_type
-   $save\_empty
-   folder-hook

Known Bugs
----------

-   The Compressed Folder hooks cannot deal with filenames that contains quotes/apostrophes.

Credits
-------

-   Roland Rosenfeld \<roland@spinnaker.de\>
-   Alain Penders \<Alain@Finale-Dev.com\>
-   Christoph "Myon" Berg \<myon@debian.org\>
-   Evgeni Golov \<evgeni@debian.org\>
-   Richard Russon \<rich@flatcap.org\>

