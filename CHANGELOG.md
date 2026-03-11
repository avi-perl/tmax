# Changelog

## [0.4.0] - 2026-03-11

### Added
- Thin colored strip below the tab bar that always matches the active tab's color, updating on tab switch, new tab, and tab close
- `sync-current-color` subcommand — queries the session's current window and updates the strip color
- `session-window-changed` hook drives strip color updates (covers implicit window changes after kill)

### Changed
- Tab pill colors reversed: letter label now has the darker background, tab name has the primary color background
- Tab colors are now unique — new windows pick a random unused color from the palette; no two tabs share a color
- `assign-color` targets `session:index` explicitly so new windows always receive the correct color (fixes race where options were set on the wrong window)
- Thin space separator between tabs instead of no separator

## [0.3.0] - 2026-03-11

### Changed
- Status bar tabs now render as two-zone pills: colored badge with the letter label, darker body with the tab name
- Home tab pill shows only the `⌂` icon — no name body
- Busy indicator replaced: 🔴 emoji → red `✸` character (works in all terminal fonts)
- Removed `│` pipe separators between tabs in the status bar
- Removed "Open tabs" heading from the home TUI

### Added
- `DARK_COLORS` palette — each tab color has a paired darker shade used for the pill body
- `@tmax_dark_color` window option set alongside `@tmax_color` on every window
- `tmax install` backfills `@tmax_dark_color` and the `⌂` label on existing windows

### Fixed
- Home TUI flash reduced: entire frame is now built in a subshell before any terminal output, then written atomically; redraws are skipped entirely when the frame is unchanged

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
