# Sample Configuration Files

🚧 **FIXME:** Still lacking node config sample fragments for some common/generic use cases

---

#### `snapback.dist.yaml`:
A minimal initial configuration,
- showing **all** global options with comments, and
- giving just a dummy node config stub.


#### `*.borgexcl`:

Some example exclusion pattern files for *Borg*.

Note that exclusion patterns do impact archiving performance, and e.g. for the linux system root, they can often be **completely** avoided by
- telling *Borg* to stay in the same file system (*SnapBack* default), and
- using directory *tagfiles* to exclude any remaining ones.

For user homes they are difficult to avoid, as most of the discardable data is typically at locations deep inside a quite dynamic tree, and
*tagfiles* often cannot be used.
