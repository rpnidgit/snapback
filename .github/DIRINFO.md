# `/.github`

This directory contains some stuff that is arranged for platform specific behaviour, differing
between `github` and `forgejo`/`gitea` hosted repos.

>[!WARNING]
>Apply changes here only with special care. This is slippery ground!

## README.md

This is a `github` specific version, overriding the one in the repo root.

**Important**
- observe the extra subdir level when linking from this one to other stuff,
- do **not** place images etc. just somewhere, but try to use `../docs/assets`,
- **never** link back to this one from other docs that are **not** `github` specific but link to the bare repo root whenever possible,
- when links from generic docs back **into** the main `README.md` cannot be avoided, use the root dir one.

## `ISSUE_TEMPLATE/`[^1]

Both `forgejo` and `gitea` read "their" dir contents **before continuing** and picking up templates from here as well.  
So templates given here are **always** used.

Only `config.yml`[^1] is ignored when another one was found before.  
This allows to provide platform specific settings for `blank_issues_enabled` and/or `contact_links`.

### Platform specific labels

These are ok to use. Unknown `labels` elements are ignored.

[^1]: `github` currently wants the dirname in uppercase, and the config as `config.yml` (**not** `config.yaml`).
