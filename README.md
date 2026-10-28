# PowerToys RunAcrylic

A Windows tray companion that changes the PowerToys Run window backdrop and provides an on-demand list of PowerToys Run plugin keywords (`kw`).

[Download the v3 source archive](./PowerToys-RunAcrylic-v3-source.zip).

## Features

- Acrylic, Mica, Off, and configurable see-through tint styles from the tray menu.
- Starts with PowerToys Run and exits with it; no Windows startup entry is required.
- Uses window events instead of continuous polling in the normal case.
- `kw` lists enabled plugin keywords; `kw <text>` filters them.
- Includes install and uninstall scripts and a script to generate the app/plugin icons.

Windows' see-through effect relies on an undocumented composition API and may fall back to Acrylic on unsupported systems. See-through levels can look similar against dark backgrounds.

## Requirements

- Windows 10/11 with Microsoft PowerToys Run installed.
- .NET 10 SDK to build and the .NET 10 Desktop Runtime to run the companion.
- Internet access for the initial NuGet restore.

## Build and install

Run PowerShell from the repository root:

```powershell
.\install.ps1
```

If PowerToys is running, close it first or use `.\install.ps1 -Force` to let the installer close and restart it. The installer places the plugin and companion under the current user's PowerToys Run plugin directory.

To uninstall:

```powershell
.\uninstall.ps1
```

Use `.\uninstall.ps1 -KeepSettings` to preserve the saved style and log. Review scripts before running them; `-Force` closes PowerToys and uninstall removes the RunAcrylic plugin and its local data.

## Source layout

- `RunAcrylic/`: WinForms tray companion and native window APIs.
- `Plugin/`: PowerToys Run plugin that starts the companion and implements `kw`.
- `tools/make-icons.py`: regenerates the icon files (requires Pillow).

The project targets .NET 10 for the companion and .NET 9 for the PowerToys plugin. The plugin package version is declared in its project file.

## Validation status

The source was compile-checked against stubs and includes 20 unit checks for style parsing, persistence, and log limits. The installer was reported to have worked in one Windows setup. Full integration testing across PowerToys and Windows versions, see-through behavior on all systems, and resource usage remain unverified.

## License

MIT. See [LICENSE](./LICENSE).
