# AHK Input Mapper for MECCHA CHAMELEON

A local desktop application for remapping keybinds in MECCHA CHAMELEON and managing game settings, including mouse Y-axis inversion and an ultrawide aspect ratio fix.

> **Note**: This is a community tool. It is not affiliated with or endorsed by the MECCHA CHAMELEON developers. Use at your own risk.

## Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [Remapping Keybinds](#remapping-keybinds)
  - [Using AutoHotkey Scripts](#using-autohotkey-scripts)
  - [Mouse Y-Inversion](#mouse-y-inversion)
  - [Ultrawide Aspect Ratio Fix](#ultrawide-aspect-ratio-fix)
- [Quick Reference](#quick-reference)
- [File Locations](#file-locations)
- [Known Limitations](#known-limitations)
- [License](#license)
- [Contributing](#contributing)

## Features

- **Rebind Keybinds**: Remap keyboard and mouse inputs with a clean interface
- **Linked Movement**: Edit WASD movement once and apply across all contexts (First Person & Mover)
- **Generate AutoHotkey Scripts**: Create working `.ahk` scripts that intercept your new keys and send the original ones the game listens for
- **Mouse Y-Inversion**: Toggle mouse Y-axis inversion directly from the app with read-only file protection
- **Ultrawide Aspect Ratio Fix**: Toggle a fix for FOV/stretching issues on ultrawide monitors, also with read-only file protection
- **Load/Save Scripts**: Open and re-edit previously created remap scripts

## Installation

### Requirements

- Windows 10 or later
- [AutoHotkey](https://www.autohotkey.com)

- ## Usage

### Remapping Keybinds

1. Click any key chip to rebind it by pressing a new key, clicking a mouse button, or using the mouse wheel
2. The tool focuses on the controls players actually remap: **Movement (WASD)**, **Interact**, **Jump**, **Crouch**, **Dash**, **Shoot**, **Aim**, **Paint / Mode Change**, **Body Pose**, **Whistle / Taunt**, **Voice Chat (Talk/Hear)**, **Text Chat**, and **Toggle Player Names**. Each control has one default key; a small amber dot marks any you've changed.

   > **How it works:** the generated AutoHotkey script intercepts the key you pick and sends the game's *default* key for that control, so the game never needs to know anything changed. That's why the tool doesn't touch or depend on the game's own config files.

3. Click **Load…** to open a previously created `.ahk` script for editing
4. Click **Create** to save a new script, or **Save** to overwrite a loaded one

> **Controller users:** This tool covers keyboard and mouse only. Since MECCHA CHAMELEON is on Steam, controller remapping is best handled through Steam Input (right-click the game → Manage → Controller layout), which is purpose-built for it.

### Using AutoHotkey Scripts

**Important**: MECCHA CHAMELEON does not currently read keybind configs at runtime, so AutoHotkey is the workaround.

1. **Install AutoHotkey** from [autohotkey.com](https://www.autohotkey.com) if you haven't already — any version works, the app detects it automatically
2. After clicking **Create**, the `.ahk` file downloads/saves
3. **Edit the process name** in the script if needed:
   - Open the `.ahk` file in Notepad
   - Find the line: `#IfWinActive, ahk_exe MecchaChameleon.exe`
   - Replace `MecchaChameleon.exe` with the actual game process name (check Task Manager → Details while the game is running)
   - Save the file
4. **Run the script**: Double-click it while the game is running
5. **Stop it**: Right-click the AHK tray icon → Exit

### Mouse Y-Inversion

The app can create/modify `Game.ini` to invert mouse look:

1. Find the **Game Settings** panel at the bottom
2. Toggle **Mouse Y-Axis Inversion** on/off
3. Optionally check **Make Game.ini read-only** to prevent accidental edits
4. The file is saved to:
   ```
   %LOCALAPPDATA%\Chameleon\Saved\Config\Windows\Game.ini
   ```

The setting uses `InputPitchScale=-2.5` (inverted) or `InputPitchScale=2.5` (normal).

### Ultrawide Aspect Ratio Fix

The app can create/modify `Engine.ini` to fix FOV and stretching issues on ultrawide monitors:

1. Find the **Game Settings** panel at the bottom
2. Toggle **Fix Ultrawide Aspect Ratio** on/off
3. The toggle offers the same read-only file protection as the mouse inversion setting
4. The file is saved to:
   ```
   %LOCALAPPDATA%\Chameleon\Saved\Config\Windows\Engine.ini
   ```

The setting uses `AspectRatioAxisConstraint=AspectRatio_MaintainYFOV`.

## Quick Reference

- **Click a key chip**: Rebind that key
- **+ Add**: Bind multiple keys to the same action
- **×**: Remove a binding
- **Reset**: Revert all changes to the original defaults
- **Load…**: Open a previously created script for editing
- **Create / Save**: Save a new script, or overwrite the loaded one

- ## File Locations

- **AHK Scripts**: Saved to your chosen location via file dialog
- **Game.ini**: `%LOCALAPPDATA%\Chameleon\Saved\Config\Windows\Game.ini`
- **Engine.ini**: `%LOCALAPPDATA%\Chameleon\Saved\Config\Windows\Engine.ini`
- **App Config**: Standard Electron app data locations (OS-specific)

## Known Limitations

- Mouse-axis bindings (wheel, look) can't be remapped via AutoHotkey (no keyboard equivalent)
- Controller/gamepad remapping is not covered — use Steam Input for that
- Game.ini and Engine.ini settings apply on next game launch, not immediately
- Read-only protection may not work if Windows permissions prevent it

## License

MIT

## Contributing

Found a bug? Want to request a feature? Open an issue or a pull request — contributions are welcome.
