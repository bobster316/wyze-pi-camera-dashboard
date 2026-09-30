# Agent notes

This is the Pi-only copy of the main repository `go2rtc-wyze-monitor`
(local: `../go2rtc-wyze-monitor`). The full project handover is there:
`../go2rtc-wyze-monitor/HANDOVER-2026-09-28-CODEX.md`; the latest is
`../go2rtc-wyze-monitor/HANDOVER-2026-09-30-STOP-DELETE-SUMMARY.md`.

- Make Pi-side changes in the main repo first, then mirror them here.
  Here the red favicon is `src/favicon.svg` (main repo: `src/favicon-pi.svg`).
- Tests: `$env:NODE_OPTIONS=''; npm test`.
- Never commit `cameras.yaml`, `.env`, or generated `go2rtc.yaml` files.
- The owner may retire this repo in favour of the main one; do not archive
  or delete it without explicit approval.
