# Zen32-HA-Blueprint

Home Assistant automation blueprints for Zooz Z-Wave scene controllers and switches.

## Overview

This repository contains Home Assistant automation blueprints for controlling and monitoring Zooz Z-Wave devices, including scene controllers and switches with LED state tracking capabilities.

## Requirements

- Home Assistant 2024.6.0 or later
- Z-Wave JS integration configured
- Compatible Zooz Z-Wave devices

## Blueprints

### 1. ZEN32 and ZEN35 Scene and State (Z-Wave JS)

**File:** `ZEN32-control-track.yaml`  
**Version:** 2026.2.0  
**Supported Devices:**
- Zooz ZEN32
- Zooz ZEN32 800LR
- Zooz ZEN35

**Features:**
- Button press triggers with scene support
- LED state tracking for entity states (on/off/unavailable)
- Configurable LED colors and brightness per button
- Multi-press support (1x, 2x, 3x, 4x, 5x) for all buttons
- Hold and release actions for all buttons
- Advanced Nighttime LED Scheduling: Dim, turn off, or override LED colors (e.g., Red for night vision) during specified hours or via entity state.
- Nighttime Entity Support: Use a toggle, binary sensor, sun, or a template sensor to trigger Night Mode (supports 'on', 'below_horizon', 'true', 'night').
- Logic Inversion: Toggle to invert night entity logic if you only have a Daytime entity.
- Untracked LED Silencing: Optionally force LEDs of buttons with no assigned entity to "Always Off."
- Relay control configuration (Parameter 19)
- LED reporting configuration (Parameter 20)
- Support for 3-way switch scene control (Scene 6) - requires 800 series or firmware 10.40+ on 700 series
- Tracks multiple entity types:
  - Lights, switches, fans
  - Covers (garage doors, blinds)
  - Climate controls
  - Alarm control panels
  - Locks
  - Media players
  - Binary sensors
  - Input booleans
  - Automations
  - scripts
  - people
  - device trackers

**Button Layout:**
- Button 0: Relay button (big button) - Scene 5
- Button 1: Top left button - Scene 1
- Button 2: Top right button - Scene 2
- Button 3: Bottom left button - Scene 3
- Button 4: Bottom right button - Scene 4
- Button 5: 3-way switch (if configured) - Scene 6

**LED Configuration:**
Each button can be configured with:
- Off state behavior (Always off, Always on, On during daytime)
- Off color (White, Blue, Green, Red, Magenta, Yellow, Cyan)
- Off brightness (Low, Medium, Bright)
- On state behavior
- On color
- On brightness
- Unavailable state behavior, color, and brightness

**Nighttime Settings:**
- Configure start and stop times for nighttime LED behavior
- Optional Nighttime State Entity: Use an entity to override time-based scheduling.
- Global Night Overrides: Force a specific color and brightness level for all active LEDs during Night Mode.
- Scenes continue to work during nighttime
- Entity state changes are properly handled during nighttime transitions

### 2. ZEN37 Z-Wave JS Scene Controller

**File:** `Zen37-ZwaveJS-blueprint.yaml`  
**Supported Devices:**
- Zooz ZEN37
- Zooz ZEN37 800LR

**Features:**
- Scene control for ZEN37 800LR wall remotes
- Support for multiple devices
- Multi-press support (1x, 2x, 3x, 4x, 5x) for both buttons
- Hold and release actions for both buttons

**Button Layout:**
- Button 1: Up/On button
- Button 2: Down/Off button

### 3. Zooz ZEN71 Scene Blueprint

**File:** `ZEN71-scene-blueprint.yaml`  
**Version:** 2024.9.1-2  
**Supported Devices:**
- Zooz ZEN71
- Zooz ZEN71 800LR

**Features:**
- Scene control for ZEN71 switches
- LED tracking functionality
- Support for 3-way and 4-way switch setups (multiple device selection)

## Installation

1. Copy the desired blueprint YAML file to your Home Assistant `blueprints/automation/` directory, or
2. Import the blueprint directly from the GitHub repository URL in Home Assistant:
   - Go to **Settings** → **Automations & Scenes** → **Blueprints**
   - Click **Import Blueprint**
   - Enter the GitHub raw URL for the blueprint file

**GitHub Repository URLs:**
- ZEN32/ZEN35: `https://github.com/rwalker777/Zen32-HA-Blueprint/blob/main/ZEN32-control-track.yaml`
- ZEN71: `https://github.com/rwalker777/Zen32-HA-Blueprint/blob/main/ZEN71-scene-blueprint.yaml`

## Usage

### ZEN32/ZEN35 Blueprint

1. Create a new automation using the blueprint
2. Select your Zooz ZEN32 or ZEN35 device
3. Configure relay control parameters (Parameter 19 and 20)
4. Set up nighttime schedule or Nighttime State Entity (optional)
5. For each button:
   - Configure scene actions (single press, multi-press, hold, release)
   - Select entity to track (optional)
     - If no entity is tracked, use "Turn Off Untracked LEDs" to keep the button dark.
   - Configure LED behavior for on/off/unavailable states
   - Set LED colors and brightness
6. Configure 3-way switch scene control (if applicable)

### ZEN37 Blueprint

1. Create a new automation using the blueprint
2. Select your Zooz ZEN37 device(s)
3. Configure actions for each button press type (1x, 2x, 3x, 4x, 5x, hold, release)

### ZEN71 Blueprint

1. Create a new automation using the blueprint
2. Select your Zooz ZEN71 device(s)
3. Configure LED tracking and scene actions

## Notes

- For ZEN32/ZEN35: Configure any additional Z-Wave parameters directly on the device page in Home Assistant
- Optimization: This blueprint uses a modular design to refresh LEDs instantly upon automation reload or Home Assistant restart.
- Race Condition Guard: Includes a 60-second startup delay to ensure the Z-Wave mesh is ready before syncing LED states.
- Nighttime LED behavior: When an entity changes state during nighttime, LEDs will properly reflect the new state and apply any nighttime color/brightness overrides.
- For 3-way switch support on ZEN32/ZEN35, the 3-way switch must be set to momentary mode

## Troubleshooting

- Ensure your Z-Wave JS integration is properly configured
- Verify device firmware versions meet requirements (especially for 3-way switch support)
- Check that device parameters are set correctly
- Review Home Assistant logs for any automation errors

## Contributing

Contributions and improvements are welcome! Please feel free to submit issues or pull requests.

## License

This project is open source and available for use in Home Assistant installations.
