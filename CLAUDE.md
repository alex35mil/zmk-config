# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a ZMK (Zephyr-based Mechanical Keyboard) configuration repository for a Corne split keyboard (named "Chocofi") with Nice!Nano v2 controllers and Nice!View displays.

## Essential Commands

### Update Firmware
```bash
# Prerequisites: Set environment variables
export GITHUB_USER="alex35mil"
export GITHUB_REPO="zmk-config"
export GITHUB_TOKEN="github_pat_XXXXXXXX"

# Flash firmware (downloads latest from GitHub Actions)
scripts/update left    # Flash left side
scripts/update right   # Flash right side
```

## Architecture

The repository uses a modular configuration approach:

- `config/corne.keymap` - Main keymap file with 14 layers (English/Russian support)
- `config/modules/` - Modular configuration files:
  - `behaviors.dtsi` - Custom key behaviors
  - `combos.dtsi` - Key combinations
  - `hrms.dtsi` - Homerow mods configuration
  - `mouse.dtsi` - Mouse emulation
  - `ru.dtsi` - Russian language support
  - `apps/` - Application-specific bindings

## Key Dependencies

This repository uses urob's ZMK fork (specified in `config/west.yml`) which provides enhanced features like mouse support and additional behaviors.

## Development Workflow

1. Edit configuration files (primarily `corne.keymap` or module files)
2. Commit and push changes
3. GitHub Actions automatically builds firmware (~2.5 minutes)
4. Flash using `scripts/update left/right`

## Important Notes

- The keyboard requires bootloader mode for flashing (double-tap reset)
- Both halves must be flashed separately
- Build artifacts expire after 90 days on GitHub
- Mouse support is enabled (`CONFIG_ZMK_MOUSE=y`)
- Uses custom Nice!View display theme (nice-view-gem)
