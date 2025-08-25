# GUIs as root

Helpers for GUIs to be elevated to root via `pkexec`.

## Important Notes

1. GUI elevation should normally **not** be done. When things are limited to the desktop user, this **is** for good reason!  
   But as always, there are exceptions to the rule. Like when wanting to use these GUIs als supplements to *SnapBack*.
2. When using these GUIs with *SnapBack*, do **not** expect things to integrate in perfect fashion!  
   In particular, the common ones crafted for `snapper` environments know **only** about its standard *cleanup algorithms*, and are **not** prepared to deal with  the custom tagging used by *SnapBack*.
3. The elevated GUIs need to be *well integrated* into the system, i.e. installed via std. packages or self-built. The wrapping used here is **not** supposed to work with *encapsulated* (like *Flatpak* or *Snap*) variants.

## GUIs

Two variants are given here:

1. A generic one which then requires only a small change to about any GUI's `*.desktop` file (or a copy thereof), and
2. a detailed *per-GUI* one for the following:

- [`vorta`](https://vorta.borgbase.com/), the popular [`borg`](https://www.borgbackup.org/) backup frontend.
- [`snapper-gui`](https://github.com/ricardomv/snapper-gui), the standard[^sngui] GUI for the common snapshot tool.

Which variant to use is a matter of taste and consideration. The generic one is simpler - but it is... generic.

## Files

#### 1. `bin/*`

The wrapper scripts come in pairs:

- `*-launcher` wraps the `pkexec` call and makes it pass env. infos via params over to the according, 'polkit-enabled'
- `*-wrapper`, which then sets the env. again before finally firing up the GUI, handing over any args remaining after shifting away the previously added transfer params.

These - as well as the GUI executable(s) - are expected to be in `PATH`.
The given `*.policy` definitions explicitely declare `*-wrapper` to be in `/usr/local/bin` and need to be modified in case another location is chosen.

**Variants:**

- **Generic:** Take the `gsu-*` scripts and live happily thereafter.
- **per-GUI:** Take the ones for the individual GUI(s).

#### 2. `policy/*`

The polkit action definition files for the according `*-wrapper`. The standard location for these is `/usr/share/polkit-1/actions`.

**Variants:**

- **Generic:** Take the `org.ACME.gsu-wrapper.pkexec.policy` and live happily thereafter.
- **per-GUI:** Take the one(s) for the individual GUI(s).

#### 3. `desktop/*`

The `*.desktop` files (for the according `*-launcher`). As users need to be sudoers anyway, security isn't a major placement aspect. But to avoid confusion, these should still be made available only to those who are in fact meant to use them. A good place is the users' private `~/.local/share/applications` directory.

**Variants:**

- **Generic:** Nothing to take from here! Just copy/modify the GUI's best suited `.desktop` file, prepending `gsu-launcher` to the `Exec` value, i.e. change it from e.g. `Exec=vorta` into `Exec=gsu-launcher vorta`.
- **per-Gui:** See the given `desktop/*` ones for the according GUI.

## Individual File Sets

#### 1. Generic

*For all:*

```
  policy/org.ACME.gsu-wrapper.pkexec.policy
  bin/gsu-launcher
      gsu-wrapper
```

#### 2. Per-GUI

*For Vorta:*

```
  desktop/com.borgbase.Vorta.desktop
  policy/com.borgbase.Vorta.pkexec.policy
  bin/vorta-launcher
      vorta-wrapper
```

*For Snapper Gui:*

```
  desktop/snapper-gui.desktop
  policy/org.snapper-gui.pkexec.policy
  bin/snapper-gui-launcher
      snapper-gui-wrapper
```


[^sngui]: Note `snapper-gui` is quite basic. An alternative is [`btrfs-assistant`](https://gitlab.com/btrfs-assistant/btrfs-assistant), giving more features - and it already comes with its own elevating mechanism.
