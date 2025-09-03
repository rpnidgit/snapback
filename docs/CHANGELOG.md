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

### Changed
- `archive.create` config: `pattern` & `exclude.pattern` may now also be given as sequences ([#1][1]).


[1]: https://codeberg.org/rpnid/snapback/issues/1


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

