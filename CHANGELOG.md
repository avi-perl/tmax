# Changelog

## [0.2.0] - 2026-03-11

### Changed
- Project renamed from `claudmux` to `tmax`
- `reload` command renamed to `install` (alias `-i`)

### Added
- `tmax install` adds tmax to `PATH` in the user's shell rc file if not already present
- `tmax install` now serves as the canonical setup command (config + PATH + hot-reload)
- Quickstart section in README

### Fixed
- `Alt+x` on home tab now detaches instead of showing a warning
- Removed flashing on home tab refresh (cursor repositioning instead of screen clear)
- Home tab no longer shows header/subtitle, just the tab list

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
- `tmax reload` — regenerates config and hot-reloads into running session
- `tmax kill` / `tmax -k` — kill the running session
- `tmax --help` — usage reference
- `tmax-home` hot-reloads automatically when the script file is modified
- Flash-free TUI redraws using cursor repositioning instead of screen clear
