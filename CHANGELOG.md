# Changelog

## [0.1.0] - 2026-03-11

Initial release.

### Features

- Persistent named-tab session manager backed by tmux on an isolated socket
- Home tab TUI showing all open tabs with assigned colors and runtime (`hh:mm`)
- 9-color round-robin palette assigned per window
- Status bar always visible at top with tab names and clock
- Keybindings: `Alt+0-9` to jump tabs, `Alt+n` new, `Alt+r` rename, `Alt+x` close/exit
- Close tabs from home screen by pressing their number (`1`-`9`) with confirmation
- `q` / `Alt+x` on home tab detaches and returns to outer shell
- SSH-safe — sessions survive disconnects
- `claudmux reload` — regenerates config and hot-reloads into running session
- `claudmux kill` / `claudmux -k` — kill the running session
- `claudmux --help` — usage reference
- `claudmux-home` hot-reloads automatically when the script file is modified
- Flash-free TUI redraws using cursor repositioning instead of screen clear
