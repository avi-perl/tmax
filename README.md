# tmax

A persistent, named-tab terminal session manager built on tmux. SSH-safe — sessions survive disconnects and reconnect instantly.

## Requirements

- `tmux` 3.2+
- `bash`

## Quickstart

```bash
git clone https://github.com/avi-perl/tmax
cd tmax
./tmax install
source ~/.bashrc   # or ~/.zshrc
tmax
```

`tmax install` generates the config, adds `tmax` to your `PATH`, and sets up shell integration. `tmax` starts (or reattaches to) your session.

## Usage

```
tmax              Start or attach to session
tmax install      Set up config (run once after cloning, or after config changes)
tmax kill         Kill the running session and all tabs
tmax --help       Show help
```

## Navigation

### Tab menu

Press `Alt+h` or click `☰` in the status bar to open the tab menu — a popup overlay showing all open tabs with their color, status, and uptime.

| Input | Action |
|-------|--------|
| `1`–`9` | Jump to tab by number |
| click tab row | Jump to that tab |
| `q` / click `✕` / click outside | Close menu |

### Keybindings (from any tab)

| Key | Action |
|-----|--------|
| `Alt+h` / click `☰` | Open tab menu |
| `Alt+1`–`9` | Jump to tab by number |
| `Alt+n` | New tab (prompts for name) |
| `Alt+r` | Rename current tab |
| `Alt+x` | Close current tab (with confirm) |

## Tab status indicators

Each tab shows a status indicator in the menu and status bar:

| Indicator | Meaning |
|-----------|---------|
| `▶︎` green | Command running |
| `✓` green | Command finished (unvisited) |
| `■` red | Command failed (exit code ≠ 0) |

Status indicators require shell integration, which `tmax install` sets up automatically.

## How it works

tmax runs an isolated tmux session on its own socket (`-L tmax`) so it never conflicts with an existing tmux setup. On first start it generates a config and creates a session with a single shell window.

Each tab gets a unique color from a 9-color palette. The tab menu (`tmax-home`) is a bash loop that redraws every ~0.2s as a tmux popup — it hot-reloads automatically when the script file is modified.

Colors and creation timestamps are stored as tmux window options (`@tmax_color`, `@tmax_start`).

## Files

| File | Purpose |
|------|---------|
| `tmax` | Main CLI — session management, config generation |
| `tmax-home` | Tab menu TUI (runs as a popup) |
