The bug-fix branch has a set of fixes for Mutt that aren't in the upstream
branch yet.

---

### add strndup.c strnlen.c

No notes.

<sub>(Karel Zak - 2012-09-06 - [6fa23fa](https://github.com/neomutt/neomutt/commit/6fa23faa08b19e1748ca20505abddfb47293a906))</sub>

---

### fix spelling typo

> Change `dont` to `don't`.

> This issue was detected by Debian QA packaging.

<sub>(Víctor Manuel Jáquez Leal - 2013-10-17 - [2775962](https://github.com/neomutt/neomutt/commit/27759627f3dca77932317bd84763a44308b36ad3))</sub>

---

### More careful file writing for aliases and attachments

> Use fsync and check for errors when appending to alias file,
> saving attachments, and bouncing a message.  Still more checks are needed.
> Also preserve errno if safe_fsync_close fails.

<sub>(Sami Farin - 2013-10-16 - [b130e31](https://github.com/neomutt/neomutt/commit/b130e31f4525f47ad12c5b94f95590a87bd804ea))</sub>

---

### Bye srandom() and random()

> Prefer getrandom on Linux, use /dev/urandom otherwise to
> get entropy for MIME boundaries, message-id, Maildir filename,
> temporary filename.  Using MUTT_RANDTAG_LEN (currently 16) base32
> characters for boundaries and message-id.

<sub>(Sami Farin - 2013-10-16 - [c748eb8](https://github.com/neomutt/neomutt/commit/c748eb8bd73d96f630815ff6bf36431b0d091941))</sub>

---

### Remove TLS version notification

> The reason for this patch is that the "TLS connection" message adds an
> unnecessary, annoying, unskippable delay to _every_ mutt startup.

> (Almost as if its intention was to _discourage_ TLS usage...)

<sub>(Mantas Mikulėnas - 2013-10-18 - [d53c0bb](https://github.com/neomutt/neomutt/commit/d53c0bb24d98635f3264fc1a99d38ec10c071584))</sub>

---

### Use unlocked libc IO everywhere.

> Since mutt does not use threads, there is no reason it should use the
> locked variants of the FILE* IO functions. This checks if the unlocked
> functions are available, and if so enables them globally via mutt.h.

> Cuts load time for a 56k message, 1.8GB /var/mail mailbox from 14
> seconds to ~6 seconds, since we avoid acquiring and releasing a mutex
> for every character of input read.

> Before: 0m14.376s

    74.98%          mutt  libc-2.18.so        [.] _IO_getc
    11.87%          mutt  mutt                [.] mbox_parse_mailbox
     0.94%          mutt  [kernel.kallsyms]   [k] copy_user_generic_string
     0.83%          mutt  libc-2.18.so        [.] __strchr_sse2
     0.53%          mutt  libc-2.18.so        [.] __memcpy_sse2
     0.44%          mutt  libc-2.18.so        [.] _int_malloc

> After: 6 seconds

    68.92%     mutt  mutt                  [.] mbox_parse_mailbox
     2.25%     mutt  [kernel.kallsyms]     [k] copy_user_generic_string
     1.73%     mutt  libc-2.18.so          [.] __strchr_sse2
     1.24%     mutt  libc-2.18.so          [.] __memcpy_sse2
     1.17%     mutt  libc-2.18.so          [.] _int_malloc
     0.87%     mutt  libc-2.18.so          [.] __strspn_sse42

<sub>(David Wilson - 2013-10-22 - [5adde05](https://github.com/neomutt/neomutt/commit/5adde051f0ae67bfc8aeea0a26060c4e6b0685e4))</sub>

---

### Add browser sort by description, message count and new message count

> Now the browser can sort by mail folder description, (all) message count, and
> new message count.

<sub>(Tim Stoakes - 2012-09-16 - [366fa21](https://github.com/neomutt/neomutt/commit/366fa2139c811e71daabd8c3caf048e589467b48))</sub>

---

### fix %* index_format

 * mutt_wstr_trunc() does not reset mbrtowc() after error

 * mutt_wstr_trunc() compare signed and unsigned numbers to check for
   maxlen and maxwid limits and does not care about unprintable chars

> Addresses: https://github.com/karelzak/mutt-kz/issues/58

<sub>(Karel Zak - 2013-10-22 - [91d83c0](https://github.com/neomutt/neomutt/commit/91d83c045bfd3407e4c8f40e5504ba2ce588f6bd))</sub>

---

### build fix for po package name

No notes.

<sub>([Richard Russon](https://github.com/flatcap) - 2016-02-09 - [fdba601](https://github.com/neomutt/neomutt/commit/fdba601565a4bf22d3b3463352ff4024a90d1761))</sub>

---

### mute build warning

No notes.

<sub>([Richard Russon](https://github.com/flatcap) - 2016-02-17 - [0b53174](https://github.com/neomutt/neomutt/commit/0b5317404181a1f056ba3cd84489b25fbb651f8b))</sub>

---

### fedora: sync_helper crash fix

> Fedora adds this patch to fix a crash in sync_helper() (imap/imap.c)

> I can't find a matching bugzilla report, but the patch is can do no harm.

<sub>([Richard Russon](https://github.com/flatcap) - 2016-03-19 - [f071dc1](https://github.com/neomutt/neomutt/commit/f071dc1bb720a726be36e7d81ac6cb604a51fd33))</sub>

---

### fedora: document debug command line option

> Fedora adds a one-liner change to the docs to explain the "mutt -d"
> command line option.

<sub>([Richard Russon](https://github.com/flatcap) - 2016-03-19 - [1ef3480](https://github.com/neomutt/neomutt/commit/1ef3480147503951e30efc40c293c91b292350e3))</sub>

---

### debian: hurd build fix

> Hurd is missing a definition for PATH_MAX.

<sub>([Richard Russon](https://github.com/flatcap) - 2016-03-19 - [4b3a15d](https://github.com/neomutt/neomutt/commit/4b3a15d0b7500c9305c40b64fc9cb09c9549f9f2))</sub>

---

### quieten two compiler warnings

No notes.

<sub>([Richard Russon](https://github.com/flatcap) - 2016-03-18 - [a51af8e](https://github.com/neomutt/neomutt/commit/a51af8ea7fb9012fc940794bc428ad52da8fcb07))</sub>

