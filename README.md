<div align="center">

# inputX

**Real-time performance & input monitoring for Windows, with a live keyboard heatmap, mouse/controller stats, and a clean dark dashboard.**

</div>

---

## About

inputX is a desktop dashboard that gives you a single, live view of how your PC and your inputs are performing — CPU, RAM, disk, network, GPU, running games, and a real-time heatmap of every key you press — all in one lightweight app that lives in your system tray.

It's built with PySide6 (Qt for Python) and `psutil`, and is designed to stay smooth and responsive even while it's sampling live system data in the background.

### Features

- **System dashboard** — live CPU, RAM, disk, and GPU usage with rolling history charts
- **Network monitor** — download/upload speed, ping, and local IP
- **Keyboard heatmap** — every keypress tracked and visualized in real time
- **Mouse analytics** — clicks, scroll, and distance traveled
- **Controller page** — connected gamepad input visualization
- **Game detection** — automatically recognizes 30+ popular games from running processes
- **System tray integration** — minimize to tray, quick page-jump menu, runs quietly in the background
- **Launch on startup** (Windows) — optional toggle in Settings

---

## Download (for regular users)

**Don't want to install Python or run any code?** Just grab the pre-built app:

👉 **[Download the latest `inputX.exe` from Releases](../../releases/latest)**

1. Go to the **Releases** page (link above)
2. Download `inputX.exe` from the latest release's **Assets**
3. Double-click to run — no installation, no terminal, no Python required

> ⚠️ Windows SmartScreen may show a warning since the exe isn't code-signed. Click **"More info" → "Run anyway"** if you trust the source.

The instructions below (cloning the repo, VS Code, virtual environments, etc.) are only needed if you want to **run or modify the source code yourself** — most users can skip straight to the Download section above.

---

## Requirements (for running from source)

- **Python 3.10+**
- **Windows 10/11** (primary target — startup-on-login and GPU detection use Windows-specific APIs; the dashboard itself runs on macOS/Linux too, with those two features disabled)
- [VS Code](https://code.visualstudio.com/) with the official **Python extension** (recommended, not required)

---

## Getting Started in VS Code (developers only)

### 1. Clone the repository

Open a terminal (or VS Code's integrated terminal: **Terminal → New Terminal**) and run:

```bash
git clone https://github.com/YOUR_USERNAME/inputx.git
cd inputx
code .
```

### 2. Create and activate a virtual environment

**Always use a virtual environment** for this project — it keeps inputX's dependencies isolated from your other Python projects and avoids version conflicts.

In the VS Code integrated terminal:

```bash
python -m venv venv
```

Activate it:

```bash
# Windows (PowerShell)
venv\Scripts\Activate.ps1

# Windows (Command Prompt)
venv\Scripts\activate.bat

# macOS / Linux
source venv/bin/activate
```

> Your terminal prompt should now show `(venv)` at the start of the line — that confirms it's active.

### 3. Point VS Code at the venv

Press **`Ctrl+Shift+P`** → type **`Python: Select Interpreter`** → choose the one inside `./venv` (it'll be labeled `('venv': venv)`). This makes sure VS Code's IntelliSense, debugger, and terminal all use the same environment.

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

### 5. Run the app

```bash
python main.py
```

**Or, in VS Code:** open `main.py` and press **`Ctrl+F5`** (Run Without Debugging).

> ⚠️ Use `Ctrl+F5`, **not** `F5`. `F5` attaches VS Code's debugger, which traces every line of Python and can noticeably slow the app down (and, since inputX runs a global keyboard/mouse hook, can cause input lag elsewhere on your system too). Use `F5` only when you actually need to debug.

---

## Project Structure

```
inputx/
├── main.py                  # App entry point, tray icon, window setup
├── requirements.txt
├── inputx_logo.png          # App icon (tray / taskbar / sidebar)
├── app/
│   ├── shell.py             # Sidebar + top header
│   ├── theme.py             # Colors, fonts, global stylesheet
│   ├── widgets.py           # Reusable UI components (cards, charts, etc.)
│   ├── startup.py           # Windows "launch on login" integration
│   ├── monitors/
│   │   └── system_monitor.py   # Background thread: CPU/RAM/disk/net/input polling
│   └── pages/
│       ├── dashboard.py
│       ├── mouse.py
│       ├── keyboard.py
│       ├── controller.py
│       ├── network.py
│       ├── games.py
│       └── settings.py
```

---

## Building a Standalone .exe Yourself (optional, developers)

If you'd rather build the exe on your own machine instead of downloading it from Releases:

```bash
pip install pyinstaller pillow
pyinstaller --noconsole --onefile --icon=inputx_logo.png --add-data "inputx_logo.png;." main.py
```

The packaged `.exe` will be in the `dist/` folder.

> Note: `dist/`, `build/`, and `venv/` should stay out of git (see `.gitignore`) — publish the built exe via **GitHub Releases** rather than committing it directly, since it's typically too large for a normal git push.

---

## Contributing

Issues and pull requests are welcome. Please open an issue first to discuss any major changes.

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
