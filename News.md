## <a name="2016-03-28"></a>2016-03-28 - NeoMutt Release: NotMuch, IfDef

These patches apply to **Mutt-1.5.24.**

New to NeoMutt this release:
- [[Skip-Quoted|skip-quoted]] Skip Quoted Text
- [[Limit-Current-Thread|limit-current-thread]] Limit Index View to Current Thread

[[Skip-Quoted|skip-quoted]] shows some context when using the `<skip-quoted>`
function.

[[Limit-Current-Thread|limit-current-thread]] allows you to limit the index view
to just the current thread.

These new features are the work of David Sterba (kdave).

**[Download NeoMutt Patches](https://github.com/neomutt/neomutt/releases/download/neomutt-20160328/neomutt-patches-20160328.tar.gz)**

"neomutt-20160328.patch" is all the patches rolled into one.

<sub>([Richard Russon](https://github.com/flatcap))</sub>

---

## <a name="2016-03-25"></a>2016-03-25 - Sidebar Intro

Added a [Sidebar Intro](sidebar-intro) - A Gentle Introduction to the Sidebar
(with pictures).

<sub>([Richard Russon](https://github.com/flatcap))</sub>

---

## <a name="2016-03-20"></a>2016-03-20 - NeoMutt Release: Bugfix Release

These patches apply to **Mutt-1.5.24.**

New to NeoMutt this release:
- Numerous [small bugfixes](https://github.com/neomutt/neomutt/wiki/bug-fixes)
- TravisCI integration

**[Download NeoMutt Patches](https://github.com/neomutt/neomutt/releases/download/neomutt-20160320/neomutt-patches-20160320.tar.gz)**

"neomutt-20160320.patch" is all the patches rolled into one.

<sub>([Richard Russon](https://github.com/flatcap))</sub>

---

## <a name="2016-03-19"></a>2016-03-19 - Bug-fixes Page

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

