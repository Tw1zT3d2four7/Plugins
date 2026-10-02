[Back to All Plugins](../../README.md)

# PWS - Pirate Weatharr Station

**Version:** `1.4.2` | **Author:** dexdeadly | **Last Updated:** Oct 01 2026, 19:45 UTC

TV-style weather channels powered by the Pirate Weather API & NOAA. Runs up to three stations, each with its own location and Dispatcharr channel.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](https://spdx.org/licenses/MIT.html) [![Repository](https://img.shields.io/badge/GitHub-Repository-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/dexdeadly/pirate-weatharr-station/)

## Downloads

### Latest Release

- **Download:** [`pirate-weatharr-station-latest.zip`](https://github.com/Tw1zT3d2four7/Plugins/releases/download/pirate-weatharr-station-1.4.2/pirate-weatharr-station-1.4.2.zip)
- **Built:** Oct 02 2026, 18:18 UTC
- **Source Commit:** [`3c4dd61`](https://github.com/Tw1zT3d2four7/Plugins/commit/3c4dd6126c9c7c2bdc12f8e9c33fd8295b3f1c18)

**Checksums:**
```
MD5:    1998819e6011a1f35904d41776643097
SHA256: 380c998bc0463b317f49f8756579ea41ab1233fbb86e8c15effe1827c60963e0
```

### All Versions

| Version | Download | Built | Commit | MD5 | SHA256 |
|---------|----------|-------|--------|-----|--------|
| `1.4.2` | [Download](https://github.com/Tw1zT3d2four7/Plugins/releases/download/pirate-weatharr-station-1.4.2/pirate-weatharr-station-1.4.2.zip) | Oct 02 2026, 18:18 UTC | [`3c4dd61`](https://github.com/Tw1zT3d2four7/Plugins/commit/3c4dd6126c9c7c2bdc12f8e9c33fd8295b3f1c18) | 1998819e6011a1f35904d41776643097 | 380c998bc0463b317f49f8756579ea41ab1233fbb86e8c15effe1827c60963e0 |
| `1.3.2` | [Download](https://github.com/Tw1zT3d2four7/Plugins/releases/download/pirate-weatharr-station-1.3.2/pirate-weatharr-station-1.3.2.zip) | Sep 30 2026, 03:30 UTC | [`878b01c`](https://github.com/Tw1zT3d2four7/Plugins/commit/878b01c6f9a5f53c8c9c9e1e78994b5d7fc69d07) | 0a2369bfb13318e04ccc14e00e8a605f | 40bc77a571270d47205d4ec5cb74b172352c2465845dfa59e574e1ca26a3165b |

---

**Source:** [Browse Plugin](https://github.com/Tw1zT3d2four7/Plugins/tree/main/plugins/pirate-weatharr-station)

**Metadata:** [View full manifest](./manifest.json)

---

## Plugin README

# Pirate Weatharr Station

A self-hosted, TV-style weather channel for Dispatcharr. PWS pulls forecast data from the Pirate Weather API, renders it as a looping broadcast, and publishes the result as a channel.

📖 **[Read the full User Guide](https://github.com/dexdeadly/pirate-weatharr-station/README.md)** — setup steps, settings reference, and troubleshooting for every feature below.

## Pages

The channel cycles through eight pages (nine with a surf spot set), about 14 seconds each:

| Page | Contents |
|---|---|
| Current Conditions | Oversized temperature, condition icon, high/low, sun times, eight metric tiles |
| 12-Hour Trend | Temperature curve with precipitation-chance and cloud-cover series |
| 7-Day Forecast | Day cards with icons, highs/lows, a shared temperature range bar, plus precipitation, humidity, wind, gusts, cloud cover and UV per day |
| Live Radar | Animated NEXRAD/MRMS radar from NOAA over an OpenStreetMap base, with a dBZ legend and a source credit |
| Regional Conditions | Current temperatures at nearby cities, plotted on a map |
| Forecast Highs | Tomorrow's highs at those same cities |
| Extended Forecast | Narrative panels for today and tomorrow with an eight-value stat grid, feels-like, accumulation, visibility and moon phase |
| Surf Report | Only when a surf spot is set. Estimated surf height and rating, primary/secondary swell, wind, water temperature, next tides and a 5-day wave outlook. See [Surf report](#surf-report) |
| Almanac | Sunrise/sunset, dawn/dusk, a phase-accurate moon icon, UV, ozone, accumulations, fire index |


## Requirements

- Dispatcharr v0.25.0 or later

## Documentation

Full setup instructions, settings reference, and troubleshooting: [https://github.com/jstevenscl/tickarr/blob/master/docs/USERGUIDE.md](https://github.com/dexdeadly/pirate-weatharr-station/README.md)

## Source

https://github.com/dexdeadly/pirate-weatharr-station
