# tmax — dev notes

## Architecture

tmax is two bash scripts:

- `tmax` — CLI entry point. Generates `~/.config/tmax/tmux.conf`, manages the tmux session lifecycle, and dispatches subcommands.
- `tmax-home` — Tab menu TUI. Normally invoked as a tmux popup (`display-popup -E`) with `TMAX_POPUP=1`. Redraws every ~0.2s. Hot-reloads itself when the file changes (via mtime check + `exec`).

tmux runs on an isolated socket (`-L tmax`) using session name `tmax`. This prevents any collision with the user's own tmux.

## Key conventions

- No dedicated home window — session starts directly on a plain shell (window 1, `base-index 1`)
- The tab menu opens as a popup via `Alt+h` or clicking `☰`; it is not a persistent window
- Window options `@tmax_color` and `@tmax_start` are set on every window via the `after-new-window` hook calling `tmax assign-color`
- Colors are assigned from a shuffled 9-color palette, avoiding duplicates
- The tmux config is **generated** — never edit `~/.config/tmax/tmux.conf` directly; edit `gen_conf()` in `tmax` and run `tmax install`

## Help docs

The `help|--help|-h` case in `tmax` is the canonical reference for users. **Any time a command is added, removed, or its behavior changes, update the help text to match.** Keep descriptions concrete — say what the command actually does, not just what it's called.

## Making changes

| Change | How to apply |
|--------|-------------|
| Edit `tmax-home` | Auto-applies within ~1s (hot-reload) |
| Edit keybindings / tmux config in `tmax` | Run `tmax install` |
| Edit session startup logic in `tmax` | Requires `tmax kill && tmax` |

## tmux vs tmax responsibilities

**tmux provides:** sessions, windows, keybindings, status bar, persistence, mouse, detach/attach

**tmax provides:** CLI (`start`/`install`/`kill`), config generation, color assignment hook, popup tab menu TUI, window timestamps
