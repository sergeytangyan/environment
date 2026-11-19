# Yazi config

Files:

- `yazi.toml` – custom previewers for archives (`.tar`, `.tar.gz`, `.tgz`, `.zip`)
- `keymap.toml` – extra keybindings (`!` shell here, `o` / `Shift+Enter` open-with menu)

## Required plugin: `piper`

`yazi.toml` runs its archive previewers through `piper`, which is **not** built
into Yazi. It is an official plugin from
[yazi-rs/plugins](https://github.com/yazi-rs/plugins/tree/main/piper.yazi) that
pipes a shell command's output into the preview pane. Without it, those
previews fail with a "plugin not found" error.

(`noop`, used for directories, is built in and needs nothing.)

The plugin is installed with `ya`, Yazi's package manager, which ships with
Yazi. The command is the same on every OS:

```sh
ya pkg add yazi-rs/plugins:piper
```

This downloads the plugin to `~/.config/yazi/plugins/piper.yazi/` and records
it in `~/.config/yazi/package.toml`. Restart Yazi afterwards.

> Yazi releases older than 25.5 use `ya pack -a yazi-rs/plugins:piper`
> instead. Check yours with `yazi --version`.

### Ubuntu

1. Install Yazi if you haven't already (it includes `ya`):

   ```sh
   sudo snap install yazi --classic
   ```

2. Install the command-line tools the previewers call. `tar` is already
   installed; `zipinfo` comes with the `unzip` package:

   ```sh
   sudo apt update
   sudo apt install unzip
   ```

3. Add the plugin:

   ```sh
   ya pkg add yazi-rs/plugins:piper
   ```

### macOS

1. Install Yazi with Homebrew (it includes `ya`):

   ```sh
   brew install yazi
   ```

2. `tar` (bsdtar) and `zipinfo` ship with macOS, so nothing else is
   needed. bsdtar's `tar -tvf` reads `.tar.gz`/`.tgz` without extra flags.

3. Add the plugin:

   ```sh
   ya pkg add yazi-rs/plugins:piper
   ```

## Check that it worked

```sh
ya pkg list                      # should list yazi-rs/plugins:piper
ls ~/.config/yazi/plugins/       # should contain piper.yazi
```

Then open Yazi and highlight a `.zip` or `.tar.gz` file. The preview pane
should show the archive's contents.

## On a new machine

If you copy this folder including `package.toml`, you don't need to add
plugins one at a time. Just run:

```sh
ya pkg install
```

## Updating

```sh
ya pkg upgrade
```
