[Back to All Plugins](../../README.md)

# Segmentarr

**Version:** `1.5.6` | **Author:** Tw1zT3d2four7 | **Last Updated:** Oct 09 2026, 13:08 UTC

HLS-segmenting stream profile for Dispatcharr: splits XC/URL provider streams into segments, repairs timestamp breaks, and delivers clean MPEG-TS through cvlc to a matching Output Profile.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](https://spdx.org/licenses/MIT.html) [![Repository](https://img.shields.io/badge/GitHub-Repository-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/Tw1zT3d2four7/Segmentarr)

## Downloads

### Latest Release

- **Download:** [`segmentarr-latest.zip`](https://github.com/Tw1zT3d2four7/Plugins/releases/download/segmentarr-1.5.6/segmentarr-1.5.6.zip)
- **Built:** Oct 09 2026, 13:09 UTC
- **Source Commit:** [`5ce5d3a`](https://github.com/Tw1zT3d2four7/Plugins/commit/5ce5d3aeba094c83240cac13465d50223712ab55)

**Checksums:**
```
MD5:    030ac155c0b3067dcbc1c776e1158d03
SHA256: aee5feff4b265ea7634e2818c0939ce3972e447224b025d896e52df016cdef7c
```

### All Versions

| Version | Download | Built | Commit | MD5 | SHA256 |
|---------|----------|-------|--------|-----|--------|
| `1.5.6` | [Download](https://github.com/Tw1zT3d2four7/Plugins/releases/download/segmentarr-1.5.6/segmentarr-1.5.6.zip) | Oct 09 2026, 13:09 UTC | [`5ce5d3a`](https://github.com/Tw1zT3d2four7/Plugins/commit/5ce5d3aeba094c83240cac13465d50223712ab55) | 030ac155c0b3067dcbc1c776e1158d03 | aee5feff4b265ea7634e2818c0939ce3972e447224b025d896e52df016cdef7c |
| `1.5.3` | [Download](https://github.com/Tw1zT3d2four7/Plugins/releases/download/segmentarr-1.5.3/segmentarr-1.5.3.zip) | Oct 08 2026, 12:43 UTC | [`7b210bd`](https://github.com/Tw1zT3d2four7/Plugins/commit/7b210bdadd88247a424d81be55b007f9b1e773f0) | 2bc883cd6f10ef1275280bd063e8469e | 7b8b333db86129782bb793883df426aad10116edfc9419fe35a0f9e2a3193693 |
| `1.5.2` | [Download](https://github.com/Tw1zT3d2four7/Plugins/releases/download/segmentarr-1.5.2/segmentarr-1.5.2.zip) | Oct 05 2026, 15:46 UTC | [`4b2c560`](https://github.com/Tw1zT3d2four7/Plugins/commit/4b2c56065014fc1744903c85bb5ced70a011052c) | 4616e3a5ad1d063b55d88a344b23f705 | 38fc0b11d3eb90f57eb83d02bc03de1d7d6342a926033d3fde012524f85b8fc2 |
| `1.5.1` | [Download](https://github.com/Tw1zT3d2four7/Plugins/releases/download/segmentarr-1.5.1/segmentarr-1.5.1.zip) | Oct 05 2026, 04:15 UTC | [`51a287d`](https://github.com/Tw1zT3d2four7/Plugins/commit/51a287db79b1a4106b386f1f838368880d9f844a) | 14f79f7f1ce1cb974370d29a0270dc5e | 89a0c2e87db442d131e5dc5d636568932ccf6f25232844076630c29777d73ec5 |
| `1.4.3` | [Download](https://github.com/Tw1zT3d2four7/Plugins/releases/download/segmentarr-1.4.3/segmentarr-1.4.3.zip) | Oct 03 2026, 12:49 UTC | [`8b3e810`](https://github.com/Tw1zT3d2four7/Plugins/commit/8b3e810d34d9141383dcc89ddf478302438a3a45) | 079caa71d61180ff2ff9a1cef0c56255 | 90a996e1a59c625e4994caaa88bd882351fd547462fa28e1e6e35477571cec92 |

---

**Maintainers:** Tw1zT3d2four7 | **Source:** [Browse Plugin](https://github.com/Tw1zT3d2four7/Plugins/tree/main/plugins/segmentarr)

**Metadata:** [View full manifest](./manifest.json)

---

## Plugin README

# Segmentarr

Hardware-free **stream stabilizer for [Dispatcharr](https://github.com/Dispatcharr/Dispatcharr)**. It cuts an unstable IPTV provider stream (Xtream Codes or plain URL) into short HLS segments, repairs timestamp corruption segment by segment, and delivers clean MPEG-TS to Dispatcharr through a final `cvlc` stage over `pipe:1`.

```
provider (XC / URL)
   |  ffmpeg: -c copy -f hls   (keyframe-aligned segments in /dev/shm)
   v
supervisor: validate -> resync -> drop corrupt packets -> stitch PCR/PTS/DTS
   |  ffmpeg finalizer (copy)
   v
cvlc (configurable caching)  ->  pipe:1
   v
Dispatcharr Output Profile (audio stage)  ->  clients
```

## What it fixes

- **Timestamp breaks** - backward or forward PCR/PTS/DTS jumps are stitched onto one continuous clock. Healthy streams pass through byte-identical.
- **Corruption** - misaligned bytes are resynced and transport-error packets are replaced with null packets.
- **Provider stalls** - cvlc's network cache smooths short provider hiccups.
- **Falling behind** - if the queue grows past the catch-up limit it jumps back to live.
- **Dead connections** - ffmpeg reconnects on drops, and the supervisor restarts ingest if segments stop arriving.

## Install

1. In Dispatcharr, open **Plugins**, find **Segmentarr**, and install it.
2. Open the plugin settings and choose your options.
3. Press **Apply & Synchronize**.
4. Restart any channel that is already playing.

Apply creates a `Segmentarr Profile - ...` stream profile and a matching `Segmentarr Output - ...` output profile, and makes both the defaults. Older unlocked Segmentarr profiles are replaced; locked ones are left alone.

> Segmentarr and [Profilarr](https://github.com/Tw1zT3d2four7/Profilarr) both set the same default stream and output profiles. Whichever one you press Apply on last owns them.

## Requirements

- `ffmpeg` and `python3` inside the Dispatcharr container
- `cvlc` (VLC) inside the container, unless **CVLC Network Cache** is set to Off
- A tmpfs at `/dev/shm` (falls back to `/tmp`)

## Settings

| Setting | Default | Effect |
|---|---|---|
| Segment Profile | Standard (2s) | Standard 2s, Low Latency 1s, or Resilient 4s (waits for two segments before starting). |
| CVLC Network Cache | 1000 ms | Caching for the final cvlc stage. Off removes cvlc. |
| Stall Timeout | 25s | Restart the provider connection if no segment appears for this long. |
| Max Catch-up Backlog | 20s | Queued media beyond this is dropped to jump back to live. |
| Timeline Gap Tolerance | 1s | Forward PCR jumps up to this are kept; larger breaks are stitched. |
| Reconnect Delay Ceiling | 5s | Longest backoff between provider reconnects. |
| Provider I/O Timeout | 15s | Provider connection treated as dead after this long without data. |
| Stream Probe Time | 3s | How much stream ffmpeg analyses before starting. |
| Audio Transcoding Override | AAC | Audio codec applied by the Output Profile (AAC, AC3, E-AC3, Opus, MP3, Copy). |

Video and audio are copied in the stream stage; audio is transcoded once, in the Output Profile. Settings are baked into the wrapper scripts at Apply time, so re-apply and restart the channel after changing any of them.

## Tradeoffs

- Adds roughly one segment plus a keyframe wait of latency, plus the CVLC cache.
- Segments live in RAM (`/dev/shm`); 30s of an 8 Mbps stream is about 30 MB.

## Source

[github.com/Tw1zT3d2four7/Segmentarr](https://github.com/Tw1zT3d2four7/Segmentarr) - MIT licensed.
