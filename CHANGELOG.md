# Changelog

## [v0.1.4]

### Added
- Macro recording now shows a colored `● REC @<reg>` indicator in the status line instead of plain `REC`
- Whichkey action labels now fill the actual column pixel width (measured via `CalcTextSize`) instead of truncating at a fixed character count
- New bindings under `<space>o`: `of` SoloInFront, `og` ToggleGridLines, `oM` ToggleMasterMonoStereo, `oT` ToggleTrimContentBehindItems
- New bindings under `<space>t`: `ts` ToggleSoloTracks, `tS` ToggleSoloDefeat, `to` MoveTracksToFolder, `tw` MakeFolder, `ta` ShowAllTracks
- `build-install.sh`: build and install script with zig 0.14.x version guard (`-z` flag to override compiler path) and prefix-based install for the plugin and keybindings

### Fixed
- Macro recording: pressing `q` no longer fires immediately with no register — the engine waits for the register key before acting, while a bare press during recording still acts as the stop toggle
- `RepeatLastCommand` (`.`) now correctly replays `PlayMacro` by routing it through `meta.handle` instead of `runner.execute`; `PlayMacro` now sets `last_command` so `.` has something to replay

## [v0.1.3]

### Fixed
- macOS: text fields (track rename, etc.) no longer have their keys eaten by vim — on macOS the accelerator hook delivers a container HWND rather than the focused child control, so `GetFocus()` is now checked alongside `msg.hwnd`

## [v0.1.2]

### Added
- **macOS support**: plugin now loads correctly on macOS — REAPER passes NULL to `SWELL_dllMain` on macOS and the resolver is now retrieved from the app delegate via the ObjC runtime, matching WDL's own `swell-modstub.mm` pattern
- **Whichkey fold chevron**: `▼/▶` button at the start of the status line collapses the window to a single line and expands it back (window height resize not yet working)
- **Edit bindings action**: `ReaVim: Edit bindings` registered as a REAPER action (also bound to `<space>B`) — opens `bindings.ini` in the OS default editor, creating it from embedded defaults if absent

### Fixed
- Script floating windows (`reaper_imgui_context`, `Lua_LICE_gfx_standalone`) no longer have their keys eaten by vim — they are parented under the main HWND so the ancestry check incorrectly passed them through to the engine

### Changed
- Vim on/off state persists across restarts via `Data/Perken/reavim.ini`
- Bindings file consolidated to `Data/Perken/bindings.ini` (single location for both the loader and the edit action)

## [v0.1.0]

Initial release.
