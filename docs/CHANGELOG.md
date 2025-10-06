# Changelog

>[!NOTE]
>*SnapBack* was started in April 2024 and has been in regular use on a number of systems since shortly thereafter.  
>Since these systems are hardly representative for "the wider public", 0.95.0 was chosen as the initial public version number.
It will be bumped to 1.0.0, and proper [Semantic Versioning](https://semver.org/spec/v2.0.0.html) used thereafter,
once wider feedback got digested and any significant "environmental myopia" based flaws resolved.

<!--
## VERSION
- Nothing yet.
### Added
### Changed
### Depracated
### Removed
### Fixed
### Security
### Contributors
-->


## Unreleased

### Added
- *Active* snapshots are now also detected in alternative fashion, not relying on *Snapper* to properly indicate them,
and not limited to system root ones.
- When the `btrfs` utility is present, snapshots currently mounted anywhere (not just at their std. targets)
are now identified and skipped from deletion in custom prunings.
- The `statedir` got an additional `alast` subdir, to buffer *last archived* info.
- Snapshot creations are now disabled when the subvol (not limited to the system root one) currently is an *active* snapshot,
i.e. is found to have a snapshot mounted instead of the std. subvol root.  
When needed, this can be changed  
  \- per global default, by setting `Global.snapshot.df_create_resnap` to `true` or `1`,  
  \- per job, by setting the `resnap` attribute to `true` or `1` in its `snapshot.create` (or `archive.create.snap` for `useown` style archiving jobs), or  
  \- per run, temporarily overriding with `--resnap` or `--noresnap`. or by setting `cfALLOW_RESNAP` to `0` or `1` in the environment.  
Such cases raise a warning when skipped per a `false` setting. With `true` or when overridden to either mode per the command line or environment,
they are reported at info level.
- Preparations for planned snapshot pruning enhancements.

### Changed
- Archiving now populates and uses the new `alast` (see above) as a *last archived* cache.
- Snapshot creations are now delayed when needed for unique epochal times (required for planned pruning enhancements).
- (internal) Streamlined the `btrfs` based alternative (not relying on *Snapper*) *default* snapshot detection.
- (internal) Reformatted some code that kept confusing VS Codium.
- (internal) Streamlined some of the archiving handler's details.

### Fixed
- When archiving from "classic" paths, archive times were not set to always equal the ones indicated per (our) naming placeholders.
- Registering runs via `--at` no longer chokes when invoking via a relative path.

## 0.95.3

### Security
- Ensured `cfGURUMODS` may only be used when running as `root`.


## 0.95.2

*Revoked & re-released 2025-09-13, see [#2][2]*

### Added
- New pruning method `native` as an agnostic alternative to the explicit native ones (`borg`/`snapper`).
- Guru feature: special `cfGURUMODS` for *pre-init* code inclusion.
- Guru feature: special `custom` job class.

### Changed
- `archive.create` config: `pattern` & `exclude.pattern` may now also be given as sequences ([#1][1]).
- Invocation info line: unit infos are now suppressed for tty sessions, and
  - ignoring non-service/timer and `user@UID.service` units,
  - suffix-stripped.
- Reworded some error outputs.
- (internal) Modified some namings.
- (internal) Job config processing finally uses class specific delegates.
- (internal) Job var filters are now more specific.

### Fixed
- `cfCFG` was not properly normalized & checked when given per the environment.
- Invocation info line did not give the correct unit name.
- **FATAL** archive naming foulup introduced in 824440a6e6574fcf43b8b45b1501c5467f8dddc8 ([#2][2]).


[1]: https://codeberg.org/rpnid/snapback/issues/1
[2]: https://codeberg.org/rpnid/snapback/issues/2


## 0.95.1

### Added
- New `X` *xverb* flag for extra outputs not fitting into other categories.
- Some more extra/debugging outputs.

### Changed
- Exit status codes: now giving more specific ones for some general cases.
- Job attribute checks: general cosmetics & prepping for improving `archive.create.*pattern` config matters.  
Blimey: these are atm crafted for single entries only. Not an essential quirk, as `*patternfile` is there and more common for multiple ones - but clearly deserving improvement.

### Fixed
- **SEVERE**: PID locks were effectively deactivated after a recent (pre-pub) change.


## 0.95.0
- First public release.

