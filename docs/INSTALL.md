# SnapBack Initial Installation

## Automated

There is no automated installation.

## Manual

### A. Preparation

1. Clone the *SnapBack* repository or download & extract the latest release.
2. Recommended: get the [documentation](../docs) as well.
3. See the [requirements](../README.md#requirements) and install any missing ones.

### B. Main Script

1. As `root`, just copy [`bin/snapback`](../bin) to the desired location, e.g. `/usr/local/bin`.
   - Exec permissions are uncritical, as the script restricts all critical operations to `uid 0`.
   - **Write permissions** you may wish to check and maybe correct.
2. Run `snapback --precheck` and see if this complains about missing things.  
Correct and repeat as needed.

### C. Extra Dirs & Initial Main Configuration

1. Choose & create a config directory, canonically recommended is `/etc/snapback`.
2. Copy [`etc/snapback.dist.yaml`](../etc) over, and rename or copy it to `snapback.yaml`.
3. Check and limit directory and file permissions.
>`snapback.yaml` should **not** be world read- or writeable, and *SnapBack* **will** nag in that case!  
> OTOH, you may not want to be `root` for everything. So consider adjusting the `group` settings right away.
4. Choose and create a `statedir`, again observing decent ownership & permissions:  
>This is a mandatory directory, for *SnapBack*'s own, stateful matters.  
>It may **neither** be a top level one, **nor** located within any inapt system path, like `/usr`.
>
>**Important:** The data kept in there is needed to **coordinate** snapshing and archiving, and thus it should of course **not** itself be affected by these (or their 'reverses'). So do assure its contents will survive any rollbacks and restores, or **at least** not be replaced with old data, e.g. by placing it on a subvolume that is not in any standard snapshot or backup plan.  
>
>This requirement is why it **needs** to be explicitely given, and cannot simply be autocreated or defaulted to somewhere in the `/var` tree.
1. In `snapback.yaml`, near the top, replace the commented value for `statedir` with this very path.
2. Run `snapback -c /etc/snapback --precheck` (modify for a different config location), and see if this gives any errors.  
Correct and repeat as needed.

**When done, *SnapBack* is essentially installed, and waiting to be configured for some actual work.**

The commented sample files in the [`etc/`](../etc) directory are there to aid. And then there is...  
... [the **documentation**](../docs)!

### D. Optional: [`systemd`](../systemd) Files

For using *SnapBack* as a `systemd` timer triggered service, the [`systemd/`](../systemd) directory contains commented sample files to start with,
including a `snapback.timer.d/times.conf` dropin compatible with the optional updating mechanism.

The sample service unit's `ExecStart` assumes
- `/usr/local/bin/snapback` for the script, and
- `/etc/snapback/snapback.yaml` for the configuration.

These are of course to be modified if other paths are used.

Note there is only a single dummy event (for *First Contact Day* in 2063) preconfigured to prevent `systemd` from nagging. So you may
safely enable `snapback.timer` right after deploying into e.g. `/etc/systemd/system` if you wish.

### Gadgets

Check the [`util/`](../util) subdir to see if there's something that may be of help.

