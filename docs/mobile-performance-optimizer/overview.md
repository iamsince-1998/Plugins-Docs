---
id: overview
title: Overview
sidebar_position: 1
---

# Mobile Performance Optimizer

Runtime optimization plugin for mobile projects.

It automatically tunes performance at runtime with:

- Auto scalability
- Auto FPS limiter
- Dynamic resolution toggling
- Thermal-state estimation

## Full Config System (UE4.27 to UE5.7 style workflow)

This plugin supports profile-based configuration from **Project Settings**:

- `Editor Preview Profile`
- `Android Profile`
- `iOS Profile`
- `Fallback Profile`

Open:

`Project Settings -> Plugins -> Mobile Performance Optimizer`

You can configure:

- General sampling and target FPS
- Low FPS trigger (`LowFPSThreshold`, required sample count)
- Heat trigger (`bEnableThermalTrigger`) with temperature thresholds
- Auto scalability ranges and thresholds
- FPS limiter per thermal state
- Dynamic resolution thresholds and screen percentage bounds
- Hardware/software auto-tuning (`bAutoTuneFromHardware`, `bAutoTuneFromDeviceProfileName`)
- Optional startup scalability
- Optional VSync policy
- Extra console commands on profile apply

This is designed to stay portable across UE4.27 through UE5.7 by using stable engine APIs and optional cvar passthrough.

## How It Works

The plugin runs a `UGameInstanceSubsystem` (`UMobilePerformanceOptimizerSubsystem`) on a timer.
Every evaluation tick, it:

1. Samples current FPS.
2. Tracks rolling average FPS.
3. Estimates thermal state from sustained FPS pressure.
4. Applies FPS cap policy.
5. Enables/disables dynamic resolution based on FPS thresholds.
6. Adjusts overall scalability level up/down with cooldown and hysteresis.
7. Applies selected runtime profile (editor preview vs mobile device).

## Installation

1. Copy plugin to:

```text
Plugins/MobilePerformanceOptimizer
```

2. Enable plugin in Unreal Editor:

`Edit -> Plugins -> Mobile Performance Optimizer -> Enabled`

3. Restart editor.

## Quick Setup

1. Play on device (or desktop preview if enabled).
2. Get subsystem in Blueprint:
   - `Get Game Instance Subsystem`
   - Class: `MobilePerformanceOptimizerSubsystem`
3. Call `Set Optimizer Enabled(true)` (enabled by default).
4. Optionally set target FPS via `Set Target FPS`.

## Runtime Profile Selection

- Android runtime: uses `Android Profile`
- iOS runtime: uses `iOS Profile`
- Non-mobile runtime:
  - Uses `Editor Preview Profile` when enabled
  - Otherwise uses `Fallback Profile`

### Runtime Testing Dropdown (Editor)

When running in editor, a toolbar dropdown is available in the Play toolbar:

- Label: `MPO: Auto` (or selected profile)
- Menu options: `Auto`, `Editor Preview`, `Android`, `iOS`, `Fallback`
- Changing the option during PIE immediately reloads and applies that profile to the optimizer subsystem

Within each selected profile, settings are auto-adjusted by detected hardware/software:

- Hardware signals: CPU cores + RAM
- Software signal: active UE Device Profile name (for example names containing `low`, `mid`, `high`, `epic`)

## Blueprint API

- `Set Optimizer Enabled(bool)`
- `Is Optimizer Enabled()`
- `Run Optimization Now()`
- `Set Target FPS(float)`
- `Get Target FPS()`
- `Get Runtime State()` (returns FPS, frame limit, scalability, dynamic-res state, thermal state)
- `Reload Config From Project Settings()`

## Default Runtime Policy

- Target FPS: `60`
- Evaluation interval: `1.0s`
- Thermal estimate:
  - `Normal` when avg FPS >= 95% target
  - `Warm` when avg FPS >= 80% target
  - `Hot` when avg FPS >= 65% target
  - `Critical` otherwise
- FPS limit by thermal:
  - Normal: `60`
  - Warm: `50`
  - Hot: `40`
  - Critical: `30`
- Dynamic resolution:
  - Enable below `50 FPS`
  - Disable above `57 FPS`
- Scalability:
  - Auto downshift when FPS < target - 4
  - Auto upshift when FPS > target + 8 and thermal is Normal
  - Cooldown between changes: `6s`

## Platform Behavior

- Android/iOS: runs by default.
- Desktop: runs only when `bRunInDesktopPIE` is true (default true for easy testing).

## Notes

- Thermal state is an estimated runtime state derived from sustained FPS behavior.
- If temperature sensor data is available on device, thermal state also uses real device temperature thresholds.
- This keeps the plugin portable across platforms and engine configurations.
- Default config file:
  - `Plugins/MobilePerformanceOptimizer/Config/DefaultMobilePerformanceOptimizer.ini`
