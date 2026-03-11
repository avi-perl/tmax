# claudmux

A persistent, named-tab terminal session manager built on tmux. SSH-safe — sessions survive disconnects and reconnect instantly.

## Requirements

- `tmux`
- `bash`

## Installation

Clone the repo and add it to your `PATH`:

```bash
git clone https://github.com/avi-perl/claudmux
export PATH="$PATH:/path/to/claudmux"
```

Or symlink the launcher:

```bash
ln -s /path/to/claudmux/claudmux ~/.local/bin/claudmux
```

## Usage

```
claudmux           Start or attach to session
claudmux reload    Regenerate config and hot-reload into running session
claudmux kill      Kill the running session
claudmux --help    Show help
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

claudmux runs an isolated tmux session on its own socket (`-L claudmux`) so it never conflicts with an existing tmux setup. On first start it generates a tmux config, creates a session with a `home` window, and launches the home TUI.

The home tab (`claudmux-home`) is a bash loop that redraws every second, showing all open tabs with their assigned color and runtime. It hot-reloads automatically when the script file is modified.

Each tab gets a color assigned from a 9-color round-robin palette. Colors and creation timestamps are stored as tmux window options (`@claudmux_color`, `@claudmux_start`).

## Files

| File | Purpose |
|------|---------|
| `claudmux` | Main CLI — session management, config generation |
| `claudmux-home` | Home tab TUI renderer |
