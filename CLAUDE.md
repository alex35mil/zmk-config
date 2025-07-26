# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a ZMK (Zephyr-based Mechanical Keyboard) configuration repository for a Corne split keyboard (named "Chocofi") with Nice!Nano v2 controllers and Nice!View displays.

## Local Development Setup

### Prerequisites
- [mise](https://mise.jdx.dev/) for tool version management and environment auto-activation
- System dependencies: `cmake`, `dtc` (device tree compiler)

### First-time Setup
```bash
# Initialize local development environment
mise exec -- just init
```

This will:
- Create Python virtual environment
- Install West (Zephyr meta-tool)
- Download ZMK, modules, and dependencies
- Install Zephyr SDK
- Install Python requirements

### Essential Commands

#### Local Build & Flash
```bash
# Build firmware
mise exec -- just build          # Build both sides (default)
mise exec -- just build left     # Build left side only
mise exec -- just build right    # Build right side only

# Flash firmware (requires keyboard in bootloader mode)
mise exec -- just flash left     # Flash left side
mise exec -- just flash right    # Flash right side

# Utility commands
mise exec -- just clean          # Clean build artifacts
mise exec -- just clean-all      # Clean everything (workspace + venv)
mise exec -- just update         # Update ZMK and dependencies
mise exec -- just check          # Check environment setup
```

#### GitHub Actions (Legacy)
```bash
# Prerequisites: Set environment variables in .envrc
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

This repository uses **vanilla ZMK** (official zmkfirmware/zmk) with additional modules:
- `urob/zmk-helpers` - Convenience macros for ZMK configuration
- `nice-view-gem` - Custom Nice!View display theme

## Development Workflow

### Local Development (Recommended)
1. Edit configuration files (primarily `corne.keymap` or module files)
2. Build locally: `mise exec -- just build` (builds both sides)
3. Flash directly: `mise exec -- just flash left`

### GitHub Actions (Backup)
1. Edit configuration files
2. Commit and push changes
3. GitHub Actions automatically builds firmware (~2.5 minutes)
4. Flash using `scripts/update left/right`

## Important Notes

- The keyboard requires bootloader mode for flashing (double-tap reset)
- Both halves must be flashed separately
- Local builds are faster (~2 minutes) than GitHub Actions
- Mouse support is enabled (`CONFIG_ZMK_POINTING=y`)
- Uses custom Nice!View display theme (nice-view-gem)
- All features work with vanilla ZMK (mouse, display, helpers)
