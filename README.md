# cli-taskbar-calendar

Lightweight month/year popup calendars for taskbar integrations.

This project installs two commands:

- `taskbar-month-calendar`
- `taskbar-year-calendar`
- `taskbar-calendar-toggle`

Current confirmed runtime target is Hyprland. Window placement and geometry are handled by compositor/window-manager rules via window class.

## Current support status

- Confirmed working: Hyprland
- Untested: Sway
- Untested: KDE Plasma (X11/Wayland)

## Features

- Month and year popup views in Alacritty
- Arrow-key navigation
- Quick toggle between month/year views (`y` and `m`)
- `q` to close, `t` to jump to current date/year
- Config file + env vars + CLI flags with strict precedence
- Global show/hide option for week numbers

## Screenshots

### Month view

![Month calendar popup](examples/month_calendar.png)

### Year view

![Year calendar popup](examples/year_calendar.png)

## Runtime dependencies

- `bash`
- `util-linux` (provides `cal`)
- `alacritty`

No hard dependency on Waybar, Hyprland, Sway, KDE, or Python.

## Usage

### Month view

```bash
taskbar-month-calendar [OPTIONS] [MONTH] [YEAR]
```

### Year view

```bash
taskbar-year-calendar [OPTIONS] [YEAR]
```

### Options (both commands)

- `--columns <int>`
- `--lines <int>`
- `--class <string>`
- `--title <string>`
- `--week-numbers`
- `--no-week-numbers`
- `-h, --help`

## Configuration

Config file path:

```bash
~/.config/cli-taskbar-calendar/config
```

Format: shell-style `KEY=VALUE`.

Example:

```bash
CLI_TASKBAR_CAL_MONTH_COLUMNS=32
CLI_TASKBAR_CAL_MONTH_LINES=12
CLI_TASKBAR_CAL_YEAR_COLUMNS=80
CLI_TASKBAR_CAL_YEAR_LINES=28
CLI_TASKBAR_CAL_MONTH_CLASS="taskbar-month-calendar"
CLI_TASKBAR_CAL_YEAR_CLASS="taskbar-year-calendar"
CLI_TASKBAR_CAL_MONTH_TITLE="Taskbar Month Calendar"
CLI_TASKBAR_CAL_YEAR_TITLE="Taskbar Year Calendar"
CLI_TASKBAR_CAL_WEEK_NUMBERS=1
```

Precedence is always:

1. CLI flags
2. Environment variables
3. Config file
4. Built-in defaults

## Environment variables

- `CLI_TASKBAR_CAL_MONTH_COLUMNS`
- `CLI_TASKBAR_CAL_MONTH_LINES`
- `CLI_TASKBAR_CAL_YEAR_COLUMNS`
- `CLI_TASKBAR_CAL_YEAR_LINES`
- `CLI_TASKBAR_CAL_MONTH_CLASS`
- `CLI_TASKBAR_CAL_YEAR_CLASS`
- `CLI_TASKBAR_CAL_MONTH_TITLE`
- `CLI_TASKBAR_CAL_YEAR_TITLE`
- `CLI_TASKBAR_CAL_WEEK_NUMBERS` (`1|0`, `true|false`, `yes|no`, `on|off`)

## Week numbers

Week numbers are enabled by default.

- Enable: `--week-numbers` or `CLI_TASKBAR_CAL_WEEK_NUMBERS=1`
- Disable: `--no-week-numbers` or `CLI_TASKBAR_CAL_WEEK_NUMBERS=0`

## Waybar integration example

See [`examples/waybar-clock-snippet.jsonc`](examples/waybar-clock-snippet.jsonc).

## Taskbar-like toggle on X11

Use `taskbar-calendar-toggle` for a click-to-open / click-to-close behavior.
It uses `xdotool` when available to close existing calendar windows by class.

You can bind your panel/taskbar launcher button to:

```bash
taskbar-calendar-toggle
```

## Window manager rules

Use class-based rules for placement and sizing:

- month class: `taskbar-month-calendar`
- year class: `taskbar-year-calendar`

Examples:

- [`examples/hyprland-rules.conf`](examples/hyprland-rules.conf)
- [`examples/sway-criteria.conf`](examples/sway-criteria.conf)
- [`examples/kwin-rule-notes.md`](examples/kwin-rule-notes.md)

For now, treat Sway and KDE examples as untested templates.

## AUR packaging

AUR files are in [`packaging/aur`](packaging/aur).

Before publishing to AUR, update `source` owner and checksums in `PKGBUILD`.

## Validation status

No compatibility or clean-machine test claims are made in this repository yet.
Use your own validation checklist and promote support statements only after your approval.

## TODO

- Test Sway popup launch and month/year switching (`y`/`m`)
- Test KDE Plasma X11 popup launch and month/year switching (`y`/`m`)
- Test KDE window-rule behavior with both month and year classes
- Promote Sway/KDE from untested to confirmed only after validation
