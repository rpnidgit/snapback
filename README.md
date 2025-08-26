<br/>
<h1 align="center"><em>SnapBack</em></h1>
<p align="center">
A versatile, flexibly configurable wrapper & automation tool for<br/>
<a href="https://www.borgbackup.org/">Borg Backup</a> &
<a href="https://github.com/openSUSE/snapper">Snapper</a>
</p>
<br/>

## Features
- Unified job concept for both archiving and (btrfs) snapshot purposes
- Archiving from paths, own (transient or persistent), or existing btrfs snapshots
- Archiving with configurable path prefixes
- Supporting multiple repositories, and mixed `borg` versions
- More flexible snapshotting than with common `snapper` automations
- Adjustable pruning/cleanup logic for archives & snapshots
- Simple job scheduling using *[OnCalendar](https://www.freedesktop.org/software/systemd/man/252/systemd.time.html)* event specification format
- Versatile individual job selection, for immediate, undefined, or timed (`at`-alike) processing
- Automated backlogging of incomplete jobs after failure or signals
- Status overview
- Optional `systemd` timer setting from configured schedules
- Optional temp. automounting
- Hooks for custom scripts pre/post all essential operations
- Optional status notifications at end of runs (D-Bus and/or custom script)
- Flexible, YAML based configuration
- Minimum overhead, small footprint
- Few dependencies
- ...
- and the [documentation](docs) got the words ***Don't Panic!*** on it!

## Requirements
- **Linux** <sub><sup>(developed and primarily tested with Debian 12/13)</sup></sub>
- `bash` v5.0 or later, 5.1+ recommended
- common basic utilities <sub><sup>(for Debian: packages <code>coreutils, hostname, libc-bin, ncurses-bin, procps, util-linux</code>)</sup></sub>
- [`yq`](https://github.com/mikefarah/yq/) v4.44 or later <sub><sup>(Mike Farah's standalone one, <b>not</b> the eponymic <code>jq</code> wrapper)</sup></sub>, 4.47+ recommended
- *for job scheduling:*
  - `systemd-analyze` &nbsp;&nbsp;<sub><sup><code>◀systemd</code></sup></sub>
  - **or** a compatible replacement for its `calendar` command
- *for archiving*:
  - [`borg`](https://www.borgbackup.org/) v1.2.4 or later, 1.2.6+ recommended, [see notes](#borg-v2-notes) for v2
- *for snapshots:*
  - [`snapper`](https://github.com/openSUSE/snapper)
  - recommended: `btrfs` utility &nbsp;&nbsp;<sub><sup><code>◀deb:btrfs-progs</code></sup></sub>
- *for desktop notifications:*
  - D-Bus environment
  - `notify-send` utility &nbsp;&nbsp;<sub><sup><code>◀deb:libnotify-bin</code></sup></sub>

>[!NOTE]
>A `systemd` environment is not absolutely required, but strongly recommended.  
>Some features are otherwise not available, and unless you **really** want to do without *job scheduling*,
you need to find a compatible replacement for `systemd-analyze calendar`.

## Downsides
- **Needs root privileges** for meaningful operation.
- Does **not** come with a GUI, but requires you to properly configure what you want it to do, using YAML.
- Supports archiving **only** with `borg`.
- Supports snapshotting **only** with `btrfs` filesystems, and **only** in `snapper` fashion.
- Does **not** handle all `snapper` features, like pre/post snapshots, and is **not** planned to ever do so.
- Does **not** give any help mangling with `snapper` configurations.
- Facilitates **only** *creation & maintenance* of snapshots & backups, and does **not** by itself help with *restoring* from or doing other things with them.
- **Requires** repositories to exist *ready for use*, and does **not** help with any repo maintenance beyond compacting.
- Author is an aged, grumpy diva.

## [Documentation 🞂](docs)

## [Installation 🞂](docs/INSTALL.md)

## [Changelog 🞂](docs/CHANGELOG.md)

## Special Notes

### `Borg` v2 Notes

>[!IMPORTANT]
>- Support for the upcoming v2 is currently still **EXPERIMENTAL**.
>- v1 repos **require manual migration**.

The good news, as far as *SnapBack* is concerned: ***Don't Panic!***

- It (hopefully) handles most things automatically, dep. on the used client's version.
- Archive names for v2 repos are clearly recommended to be configured in "new" (and simpler) fashion, but it also accepts
the "classic" v1 way w/o making `borg` unhappy.
- No need to migrate everything in one run: repos may be *version tagged* for selecting from multiple `borg` executables.

