# Wyze Pi Camera Dashboard

A local four-camera dashboard for **Wyze Cam v4 cameras with RTSP-enabled
firmware**, running entirely on a Raspberry Pi 4 or Pi 5. View the grid or a
focused camera from any browser on your LAN and save manual clips. No Wyze
account, no cloud, no subscription, and no camera-management credentials are
needed by this application.

![Wyze Pi camera dashboard, four-camera grid](assets/wyze-monitor-four-camera-hero.png)

Companion video: *I Put 4 Wyze Cameras on One Raspberry Pi 5 (Local Dashboard)*.
There's also a [Windows desktop version](https://github.com/bobster316/go2rtc-wyze-monitor)
with native MP4 recording if you'd rather run this on a PC than a Pi.

## What it does

Displays all configured cameras in an adaptive grid, with HD/Eco stream
selection, per-camera reconnect, an enlarged main-stream view, and manual clip
recording (start, stop, download). Smooth30 optionally blends frames in the
viewing browser for a smoother-looking display; it does not add captured
detail — see [Performance](docs/PERFORMANCE.md) for what that setting actually
does and doesn't do.

```text
Wyze RTSPS/H.264 -> FFmpeg stream copy -> go2rtc -> WebRTC -> browser decode
```

Each camera compresses and forwards its own video; the Pi relays the
compressed stream without decoding it, and the viewing browser does the
decoding. That division of work is why four cameras pass through a Pi without
the Pi needing to decode four pictures itself.

## Requirements and limits

- Each camera must already provide a working local RTSP/RTSPS stream. This
  app cannot enable an RTSP feature your camera's firmware doesn't have —
  check that **before** buying hardware or planning cameras around it. See
  [camera firmware prerequisite](docs/CONFIGURATION.md#1-prepare-each-camera).
- Targets Raspberry Pi OS ARM32/ARM64, Lite or Desktop. Real tests cover Pi 4
  ARM32 and Pi 5 ARM64 with an external browser viewer. Four cameras were
  tested; other counts depend on your network and viewing device.
- This is a manual-clip local dashboard, not a continuous NVR: no automatic
  event recording, no motion detection, no searchable history. If you need
  those, you need a fuller recorder setup on top of or instead of this.
- Use it on a trusted LAN or behind a VPN — there is no login screen.

## What's tested, and what isn't

Confirmed: the four-camera workflow runs on a Pi 4 and a Pi 5, live viewing
and manual clip recording both work, and a second unrelated Docker service on
the same Pi stayed available during testing.

Not yet tested: overnight/continuous reliability, behavior across many
different viewing devices and changing network conditions, and a screen
connected directly to the Pi (this project forwards compressed streams to a
browser elsewhere on the network — decoding four streams for a directly
attached monitor is a different, untested workload). See
[Performance and test status](docs/PERFORMANCE.md) for the full breakdown.

## Getting started

- [Quick start](docs/QUICKSTART.md) — shortest path to a working dashboard.
- [From-scratch setup](docs/FROM-SCRATCH.md) — complete beginner build.
- [Raspberry Pi installation](raspberry-pi/README.md) — OS prep, Docker,
  installer wizard, SSH.
- [Pi compatibility matrix](raspberry-pi/COMPATIBILITY.md) — what's certified.
- [Camera and configuration reference](docs/CONFIGURATION.md).
- [Platform features and recording](docs/PLATFORM-FEATURES.md).
- [Architecture](docs/ARCHITECTURE.md) — the full stream path.
- [Troubleshooting](docs/TROUBLESHOOTING.md).
- [Operation, backup, recovery and removal](docs/OPERATIONS.md).
- [Privacy and security](SECURITY.md).

## License and credits

MIT licensed; see [LICENSE](LICENSE). Not affiliated with or endorsed by Wyze
Labs. Uses [go2rtc](https://github.com/AlexxIT/go2rtc) and FFmpeg.
`src/vendor/video-rtc.js` comes from go2rtc and retains its upstream
licensing. Firmware is obtained from Wyze and is not redistributed here.
