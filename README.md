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
**Version:** 2025.10.0  
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
- Nighttime LED scheduling (dim or turn off LEDs during specified hours)
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
- LEDs can be dimmed or turned off during nighttime hours
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
4. Set up nighttime schedule (optional)
5. For each button:
   - Configure scene actions (single press, multi-press, hold, release)
   - Select entity to track (optional)
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
- The ZEN32/ZEN35 blueprint automatically updates device parameters when the automation is reloaded
- Nighttime LED behavior: When an entity changes state during nighttime, LEDs will properly reflect the new state (e.g., turning off when entity goes from on to off)
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
