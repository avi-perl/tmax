# claudmux — dev notes

## Architecture

claudmux is two bash scripts:

- `claudmux` — CLI entry point. Generates `~/.config/claudmux/tmux.conf`, manages the tmux session lifecycle, and dispatches subcommands.
- `claudmux-home` — TUI loop that runs in tmux window 0. Redraws every second. Hot-reloads itself when the file changes (via mtime check + `exec`).

tmux runs on an isolated socket (`-L claudmux`) using session name `claudmux`. This prevents any collision with the user's own tmux.

## Key conventions

- Window 0 is always `home` — it cannot be closed, only detached from
- Window options `@claudmux_color` and `@claudmux_start` are set on every window via the `after-new-window` hook calling `claudmux assign-color`
- Colors are assigned round-robin from a 9-color palette by window index
- The tmux config is **generated** — never edit `~/.config/claudmux/tmux.conf` directly; edit `gen_conf()` in `claudmux` and run `claudmux reload`

## Making changes

| Change | How to apply |
|--------|-------------|
| Edit `claudmux-home` | Auto-applies within ~1s (hot-reload) |
| Edit keybindings / tmux config in `claudmux` | Run `claudmux reload` |
| Edit session startup logic in `claudmux` | Requires `claudmux kill && claudmux` |

## tmux vs claudmux responsibilities

**tmux provides:** sessions, windows, keybindings, status bar, persistence, mouse, detach/attach

**claudmux provides:** CLI (`start`/`kill`/`reload`), config generation, color assignment hook, home tab TUI, window timestamps
