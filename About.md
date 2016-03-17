## What is NeoMutt?

A place to gather all the patches against Mutt.

A place for all the developers to gather.
Especially those who have made changes to Mutt, but haven't had those changes
accepted.

Hopefully this will build the community and reduce duplicated effort.

### "NeoMutt"?

NeoMutt is just a name.  When [FlatCap](https://github.com/flatcap) created the
project, he needed a name that was unused on GitHub.

### Is it a Fork?

It's not a fork of Mutt.

It's a large set of feature patches (big and small) that apply to Mutt-1.5.24.

## Why?

- Reduce duplication
- Get patches in a state to be accepted upstream

Many hundreds of Mutt users have taken the time to patch Mutt to add features.
Unfortunately, it's usually the same patches as everyone else and effort is
wasted.

Also, there are some heroic developers who have been maintaining multi-thousand
line patches:

- Notmuch patch >4 years
- Sidebar patch >10 years
- NNTP patch >15 years

This is insane.

## What's been done so far?

### Additions to Mutt

[[Sidebar]] has been completely overhauled, merging features, fixing bugs,
tidying code and documenting the results.

[[Notmuch]] has been brought up-to-date, against Mutt-1.5.24.  It has been split
out of the [mutt-kz repo](https://github.com/karelzak/mutt-kz) and refactored
slightly.

Eleven smaller [[Features|Features#minor-features]] have been tidied and
documented.

Stable features will be pushed into branches in the
[NeoMutt repo](https://github.com/neomutt/neomutt).

### Blue Sky

NeoMutt also has a couple of speculative ideas:

- Redesigning Mutt's [architecture](https://github.com/neomutt/arch#arch)
- Redesigning Mutt's [gui](https://github.com/neomutt/panel-manager#panel-manager)

**Note:** These are just toys (for now).

## What's next?

- More Features - These still need tidying up
    * Compressed Folders
    * Keywords
    * NNTP

- Yet More Features
    * There are a few more features that may be appealing to a larger audience.

- Lots of bugfixes
    * The downstream Distros have a lot of bugfixes that need integrating

- Better Sidebar Integration
    * Sidebar and Notmuch should work better together
    * NNTP would really benefit from using Sidebar

- Getting Changes Accepted Upstream

