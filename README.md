# Enhanced Digital Stopwatch — FPGA Design

A multi-mode digital stopwatch implemented on an **Altera DE0 FPGA** using **Intel Quartus** (schematic design). Drives four 7-segment displays with live counters and supports configurable display modes, bidirectional counting, an adjustable start time, and per-digit brightness control.

---

## Features

- **Two display modes** — switchable live via an on-board switch:
  - `SS:ms` — seconds and milliseconds
  - `HH:MM` — hours and minutes
- **Bidirectional counting** — count up or count down, selectable live
- **Configurable start time** — load any custom start value (e.g., `01:00`) instead of always starting from `00:00`
- **Start / Stop / Reset** push-button controls, with Stop preserving the value on the display
- **Per-digit brightness control** on the 7-segment displays
- **Binary mirroring** — the rightmost `SS` digits are displayed in binary on LED0–LED7 in real time
- **Mode and direction indicators** on LED8 and LED9

---

## Hardware & Toolchain

- **Board:** Altera DE0 Development Board
- **Toolchain:** Intel Quartus Prime
- **Design style:** Schematic entry (`.bdf`) using LPM IP cores (`lpm_counter`, `lpm_compare`, `lpm_mux`)

---

## Controls

| Input | Function |
|-------|----------|
| `KEY0` | Start counting |
| `KEY1` | Stop (current value preserved on the display) |
| `KEY2` | Full reset |
| `SW8` | Count direction (up / down); also used to load a custom start time |
| `SW9` | Display mode — `SS:ms` when HIGH, `HH:MM` when LOW |
| `SW0–SW5` | Per-digit brightness control |

## Indicators

| Output | Meaning |
|--------|---------|
| `LED9` | ON = `SS:ms` mode, OFF = `HH:MM` mode |
| `LED8` | ON = counting up, OFF = counting down |
| `LED0–LED7` | Binary representation of the rightmost `SS` digits |
| `HEX0–HEX3` | Active digit display |

---

## Repository contents

This repository ships the project as a **Quartus Archive (`.qar`)** file. This single file bundles the entire project — schematic, settings, pin assignments, and all source — and is the native format Quartus uses for sharing complete projects.

- `stopwatch.qar` — Quartus archive of the full project
- `project_report.pdf` — full design write-up (block diagram, state machine, explanation of each control)
- `README.md` — this file

---

## How to open and run the project

To open this project you need **Intel Quartus Prime** (runs on Windows and Linux; not available for macOS).

1. Install Intel Quartus Prime from Intel's FPGA software download page.
2. Launch Quartus and go to **Project → Restore Archived Project…**
3. Select `stopwatch.qar` and choose a destination folder. Quartus will automatically unpack the project into that folder.
4. Open the restored project (`.qpf`). The top-level schematic (`.bdf`) will be visible in the Project Navigator.
5. Run **Processing → Start Compilation** (`Ctrl+L`).
6. Connect the DE0 board via USB Blaster.
7. Open **Tools → Programmer**, load the generated `.sof` bitstream, and click **Start**.
8. Use the KEYs and SWs listed above to operate the stopwatch.

---

## Author

**Bshar Hussein** — Computer Engineering student, Ruppin Academic Center
