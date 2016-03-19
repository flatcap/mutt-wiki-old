## <a name="2016-03-20"></a>2016-03-20 - Bug-fixes Page

Added a [[bug-fixes page|bug-fixes]] to list the changes to Mutt.

<sub>([Richard Russon](https://github.com/flatcap))</sub>

---

## <a name="2016-03-17"></a>2016-03-17 - NeoMutt Release: NotMuch, IfDef

These patches apply to **Mutt-1.5.24.**

New to NeoMutt this release:
- [[Notmuch|notmuch]] email search support.
- [[Ifdef|ifdef]] improvements

[[Notmuch|notmuch]] adds **fast** searching to local email.
This requires the installation of "notmuch".

[[Ifdef|ifdef]] adds new config functions `ifndef` and `finish` to allow
flexible configuration.

**[Download NeoMutt Patches](https://github.com/neomutt/neomutt/releases/download/neomutt-20160317/neomutt-patches-20160317.tar.gz)**

"neomutt-20160317.patch" is all the patches rolled into one.

<sub>([Richard Russon](https://github.com/flatcap))</sub>

---

## <a name="2016-03-07"></a>2016-03-07 - NeoMutt Release: "First **NeoMutt** release"

These patches apply to **Mutt-1.5.24.**

| Patch            | Description                              |
|:-----------------|:-----------------------------------------|
| [[bug-fixes]]    | **various bug fixes**                    |
| [[cond-date]]    | **use rules to choose date format**      |
| [[fmemopen]]     | **use memory buffers instead of files**  |
| [[ifdef]]        | **conditional config options**           |
| [[index-color]]  | **theme the email index**                |
| [[initials]]     | **expando for author's initials**        |
| [[nested-if]]    | **allow deeply nested conditions**       |
| [[progress]]     | **show a visual progress bar**           |
| [[quasi-delete]] | **mark emails to be hidden**             |
| [[sidebar]]      | **overview of mailboxes**                |
| [[status-color]] | **theming the status bar**               |
| [[tls-sni]]      | **negotiate for a certificate**          |
| [[trash]]        | **move 'deleted' emails to a trash bin** |

**[Download NeoMutt Patches](https://github.com/neomutt/neomutt/releases/download/neomutt-20160307/neomutt-patches-20160307.tar.gz)**

"neomutt-20160307.patch" is all the patches rolled into one.

<sub>([Richard Russon](https://github.com/flatcap))</sub>

