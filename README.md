# tmax

A persistent, named-tab terminal session manager built on tmux. SSH-safe — sessions survive disconnects and reconnect instantly.

## Requirements

- `tmux`
- `bash`

## Quickstart

```bash
git clone https://github.com/avi-perl/tmax
cd tmax
./tmax install
source ~/.bashrc   # or ~/.zshrc
tmax
```

`tmax install` sets up the config and adds `tmax` to your `PATH` if it isn't already. `tmax` starts (or reattaches to) your session.

## Installation

Clone the repo and add it to your `PATH`:

```bash
git clone https://github.com/avi-perl/tmax
export PATH="$PATH:/path/to/tmax"
```

Or symlink the launcher:

```bash
ln -s /path/to/tmax/tmax ~/.local/bin/tmax
```

Run `tmax install` once after cloning, then `tmax` any time to attach.

## Usage

```
tmax              Start or attach to session
tmax install, -i  Set up config (run once after install, or after config changes)
tmax kill, -k     Kill the running session
tmax --help       Show help
```

## Keybindings

| Key | Action |
|-----|--------|
| `Alt+0` / `Alt+h` | Go to home tab |
| `Alt+1`–`9` | Jump to tab by number |
| `Alt+n` | New tab (prompts for name) |
| `Alt+r` | Rename current tab |
| `Alt+x` | Close current tab (confirm) / exit to shell from home |

### Home tab only

| Key | Action |
|-----|--------|
| `1`–`9` | Close tab by number (with confirm) |
| `q` | Detach and return to outer shell |

## How it works

tmax runs an isolated tmux session on its own socket (`-L tmax`) so it never conflicts with an existing tmux setup. On first start it generates a tmux config, creates a session with a `home` window, and launches the home TUI.

The home tab (`tmax-home`) is a bash loop that redraws every second, showing all open tabs with their assigned color and runtime. It hot-reloads automatically when the script file is modified.

Each tab gets a color assigned from a 9-color round-robin palette. Colors and creation timestamps are stored as tmux window options (`@tmax_color`, `@tmax_start`).

## Files

| File | Purpose |
|------|---------|
| `tmax` | Main CLI — session management, config generation |
| `tmax-home` | Home tab TUI renderer |
