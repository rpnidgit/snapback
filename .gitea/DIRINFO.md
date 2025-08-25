# `/.gitea`

This directory contains stuff to be read and used **exclusively** by `forgejo` and `gitea` instances, allowing
a slight bit of platform specific behaviour.

>[!WARNING]
>Apply changes here only with special care. This is slippery ground!

## `issue_template/`

Both `forgejo` and `gitea` read the dir contents **before continuing** in `/.github` if that one is present as well.

Do **only** place templates in here that are not already given there, or this will give duplicates - regardless of how the files are named!

Useful is the way `config.yaml`/`config.yml` is digested: When found here, the `/.github` based one is ignored.  
So this allows to provide platform specific settings for `blank_issues_enabled` and/or `contact_links`.

