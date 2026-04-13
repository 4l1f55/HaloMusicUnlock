# HaloMusicUnlock - LSPosed Module

Unlocks ALL installed apps for the Meizu 21 Dynamic Halo music visualizer.
By default Flyme only supports a hardcoded list of CN/INTL music apps.
This module hooks the Settings app and injects every installed user app.

## Requirements
- Meizu 21 with Flyme (CN ROM)
- Rooted with KernelSU / SukiSU Ultra
- LSPosed installed via SukiSU Ultra modules

## Build Instructions

1. Install Android Studio
2. Clone/open this project
3. Build > Generate Signed APK (or just debug APK for testing)
4. Install APK on device

## Install Instructions

1. Install the APK on your Meizu 21
2. Open LSPosed Manager
3. Go to Modules
4. Find "Halo Music Unlock" and enable it
5. Check scope: make sure "Settings" (com.android.settings) is checked
6. Force stop Settings app
7. Open Settings > Display > Dynamic Halo > Music Light Effect > Supported Apps
8. All your installed apps should now appear!

## How It Works

Hooks `MusicLightAppSettingsFetcher` constructor in the Settings app.
After the hardcoded whitelist is built, injects all installed non-system apps
into the `mSupportAppList`. The Flyme service then reads this list and shows
the apps in the supported apps screen.

The `flyme_music_light_off_apps` Settings.System key stores disabled apps
as a comma-separated string. Enabled apps are not stored anywhere —
they just need to be in the whitelist.

## Settings Keys Reference (for KSU module use)

```
# Toggle keys (0/1)
flyme_music_light_on
flyme_notification_light_on
flyme_breathe_light_on
flyme_charging_light_on
flyme_incall_light_on
flyme_volume_adjust_light_on
flyme_game_light_on
flyme_game_king_glory_light_on
flyme_game_peace_elite_light_on
flyme_power_on_light_on
flyme_aicy_voice_light_on
flyme_red_envelope_assistant_light_on
flyme_light_timing_on
flyme_light_timing_mode          # 0=always, 1=scheduled

# Color keys (int ARGB)
flyme_notification_light_color

# Disabled music apps (comma-separated package names)
flyme_music_light_off_apps

# System property
persist.vendor.meizu.breathe.light   # "0" or "1"
```
