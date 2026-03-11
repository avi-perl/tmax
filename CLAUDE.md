# tmax — dev notes

## Architecture

tmax is two bash scripts:

- `tmax` — CLI entry point. Generates `~/.config/tmax/tmux.conf`, manages the tmux session lifecycle, and dispatches subcommands.
- `tmax-home` — TUI loop that runs in tmux window 0. Redraws every second. Hot-reloads itself when the file changes (via mtime check + `exec`).

tmux runs on an isolated socket (`-L tmax`) using session name `tmax`. This prevents any collision with the user's own tmux.

## Key conventions

- Window 0 is always `home` — it cannot be closed, only detached from
- Window options `@tmax_color` and `@tmax_start` are set on every window via the `after-new-window` hook calling `tmax assign-color`
- Colors are assigned round-robin from a 9-color palette by window index
- The tmux config is **generated** — never edit `~/.config/tmax/tmux.conf` directly; edit `gen_conf()` in `tmax` and run `tmax install`

## Making changes

| Change | How to apply |
|--------|-------------|
| Edit `tmax-home` | Auto-applies within ~1s (hot-reload) |
| Edit keybindings / tmux config in `tmax` | Run `tmax install` |
| Edit session startup logic in `tmax` | Requires `tmax kill && tmax` |

## tmux vs tmax responsibilities

**tmux provides:** sessions, windows, keybindings, status bar, persistence, mouse, detach/attach

**tmax provides:** CLI (`start`/`install`/`kill`), config generation, color assignment hook, home tab TUI, window timestamps
