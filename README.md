BFG Repo-Cleaner [![Build Status](https://travis-ci.org/rtyley/bfg-repo-cleaner.svg?branch=master)](https://travis-ci.org/rtyley/bfg-repo-cleaner)
================

_Removes large or troublesome blobs like git-filter-branch does, but faster - and written in Scala_ - [Fund the BFG](https://j.mp/fund-bfg)

```
$ bfg --strip-blobs-bigger-than 1M --replace-text banned.txt repo.git
```

The BFG is a simpler, faster ([10 - 720x](https://docs.google.com/spreadsheet/ccc?key=0AsR1d5Zpes8HdER3VGU1a3dOcmVHMmtzT2dsS2xNenc) faster)
alternative to `git-filter-branch` for cleansing bad data out of your Git repository:

* Removing **Crazy Big Files**
* Removing **Passwords, Credentials** & other **Private data**

Main documentation for The BFG is here : **https://rtyley.github.io/bfg-repo-cleaner/**

# Modifications in this fork

This fork includes some changes and enhancements on `master` that at the time of writing are not included in `rtyley/bfg-repo-cleaner:master`:

| PR | Issue | Branch | Title | Notes |
| -- | ----- | ------ | ----- | ----- |
| [#130](https://github.com/rtyley/bfg-repo-cleaner/pull/130) | [#115](https://github.com/rtyley/bfg-repo-cleaner/issues/115) | `javabrett:no-loose-no-gc` | Improvement for issue "Don't auto-run git gc" | Prevents `git gc` from auto-running when there are no existing loose/unpacked objects.  Assists with multiple runs of bfg where you might have manually run `git gc` between runs. |
| [#137](https://github.com/rtyley/bfg-repo-cleaner/pull/137) | | `javabrett:unbound-file-matcher-options` | Unbound (allow multiple) file matcher options | Allow multiple arguments for file-glob style options ``--delete-files``, ``--delete-folders``, ``--filter-content-including`` and ``--filter-content-excluding``.  This allows multiple cleaning operations for these to be performed in a single batch-run. |
| [#140](https://github.com/rtyley/bfg-repo-cleaner/pull/140) | | | | |
| [#145](https://github.com/rtyley/bfg-repo-cleaner/pull/145) | | | | |
| [#147](https://github.com/rtyley/bfg-repo-cleaner/pull/147) | | | | |
| [#149](https://github.com/rtyley/bfg-repo-cleaner/pull/149) | | | | |
| [#151](https://github.com/rtyley/bfg-repo-cleaner/pull/151) | | | | |
| [#155](https://github.com/rtyley/bfg-repo-cleaner/pull/155) | | | | |
| | | | | |

* [PR #140](https://github.com/rtyley/bfg-repo-cleaner/pull/140) to split the `--private` switch into three new options: `--no-formerly-log-text`, `--no-formerly-commit-footer` and `--no-replace-blobs` to allow explicit control of privacy options, and make them inactive by-default.  `--private` activates all three options.
* [PR #145](https://github.com/rtyley/bfg-repo-cleaner/pull/145) to improve some CLI error-output
* [PR #147](https://github.com/rtyley/bfg-repo-cleaner/pull/147) adds a --prune-empty-commits option
* [PR #149](https://github.com/rtyley/bfg-repo-cleaner/pull/149) protect protected (dirt) blobs in other (earlier) non-protected trees
* [PR #151](https://github.com/rtyley/bfg-repo-cleaner/pull/151) always output BFG version string in reports
* [PR #155](https://github.com/rtyley/bfg-repo-cleaner/pull/155) print detail of bare/non-bare repo
* This change documentation.

This master branch is built via:

Some merge-prep:

    GIT_EDITOR=: git merge --no-ff unbound-file-matcher-options
    GIT_EDITOR=: git merge --no-ff privacy-options
    # resolve, test-fix = merge1

    GIT_EDITOR=: git merge --no-ff prune-empty-commits-test-fix
    # resolve, no conflicts = merge2

    GIT_EDITOR=: git merge --no-ff blob-protection-history
    # resolve = merge3

then:

    GIT_EDITOR=: git merge --no-ff no-loose-no-gc
    GIT_EDITOR=: git merge --no-ff cli-error-messages
    GIT_EDITOR=: git merge --no-ff replace-orig-head-38
    GIT_EDITOR=: git merge --no-ff repo-bare-message
    GIT_EDITOR=: git merge --no-ff show-header-version
    GIT_EDITOR=: git merge --no-ff merge3
    GIT_EDITOR=: git merge --no-ff doc

**Please consider this fork terminal** - the master branch will be regularly modified and **reset or rebased to upstream without warning**, re-writing history.  If you are interested in using or modifying these changes, please support the pull-requests in upstream or take/merge those yourself.
