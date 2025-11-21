# Roblox Script Exporter GUI

Simple Windows front-end for the Roblox script exporter written for [Lune](https://lune-org.github.io/docs/). Drag a place file into the window, point it at your Lune executable once, and it mirrors the CLI exporter while showing a live log.

## Download the EXE

1. Grab the latest `RobloxScriptExporter.exe` from the GitHub Releases page.
2. Double‑click it. Windows SmartScreen may warn you because it’s unsigned; choose **More info → Run anyway** if you trust the file.
3. The GUI auto-installs its only Python dependency (`tkinterdnd2`) the first time you run it.
4. You still need **Lune** installed somewhere on the machine. If it isn’t on `PATH`, use the “Lune executable” field in the GUI to locate it the first time.

### Using the GUI

1. Drag a `.rbxl` into the “Place file” box or click **Browse…**.
2. (Optional) Pick an output folder. Leave blank to use the default `<place>-scripts` naming.
3. (Optional) Browse to a specific `lune.exe` if it isn’t already detected.
4. Click **Export Scripts** and watch the log. Results land in the folder you chose.

## Building the EXE yourself

```powershell
py -m pip install -r requirements.txt  # installs tkinterdnd2 + pyinstaller
py -m PyInstaller --onefile --noconsole --name RobloxScriptExporter --add-data "exporter.lua;." gui.py
```

The bundle uses the same auto-install logic, so end users don’t need Python—just the EXE and Lune.

## Repository layout

```
rbxl-exporter-gui/
├─ exporter.lua          # Original exporter logic (unchanged from CLI)
├─ gui.py                # Tk/TkinterDnD2 GUI wrapper
├─ run-gui.bat           # Convenience launcher for dev use
└─ README.md             # This document
```

## Troubleshooting

- **“Could not auto-install tkinterdnd2”** – Run `py -m pip install tkinterdnd2` manually, then relaunch.
- **“Could not start lune”** – Make sure [Lune](https://lune-org.github.io/docs/) is installed. Either add it to `PATH` or browse to the executable in the GUI.
- **Unicode errors in log** – Already handled: the subprocess is forced to UTF‑8 and replaces unsupported characters.
