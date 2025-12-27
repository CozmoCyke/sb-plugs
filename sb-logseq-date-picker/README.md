# SB Logseq-style Date Picker (OrbitCal-based)

A tiny Library plug for [SilverBullet](https://silverbullet.md) that brings a **Logseq-like `/date` picker**:

- Floating, draggable, resizable calendar widget (OrbitCal)
- Click on a day → inserts a formatted date at the editor cursor
- Format configurable via `config.set { logseqDatePicker = { format = "…" } }`

---

## Features

- `/date` slash command (configurable name)
- Floating calendar window:
  - dark theme
  - month navigation
  - “today” highlight
  - click month/year label to jump back to current month
- Remembers its screen position using `localStorage`
- Works with SilverBullet’s `js.import` + `space-lua`

---

## Installation

1. In SilverBullet, run **`Library: Install`**.
2. Paste the URL of this plug’s `PLUG.md`, for example:

   ```text
   https://github.com/<your-username>/sb-logseq-date-picker/blob/main/PLUG.md
