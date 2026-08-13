# localboard

A single-file, server-free whiteboard you keep on your desktop or in a bookmark.
It behaves like a lightweight Miro: infinite canvas, pan/zoom, drop images from
your computer, and draw/sketch over them — and a few people can share one board
through a common folder.

## How sharing works — seats in a shared folder
- Everyone points the app at the **same folder** once (a shared drive or a
  cloud-synced folder like Dropbox/Drive/OneDrive).
- On open you're prompted to **claim a seat**. Each seat is one
  `board-<seat>.json` file, and you only ever write to your own — so there are
  **no write conflicts**. The board you see is the **union** of every seat.
- **Presence:** while your tab is open it writes a tiny `presence-<seat>.json`
  heartbeat every few seconds. A seat shows as **busy** only while its heartbeat
  is fresh, so when you close the tab your seat **frees up** (within ~8s) for
  whoever wants to join next.
- Everything auto-syncs: your edits save automatically and the board pulls
  everyone else's seats about once a second (only re-reading files that changed).

## Flow
1. Keep `index.html` on your desktop or as a bookmark and open it.
2. First time: **Select shared folder** (Chrome/Edge). It's remembered, so next
   time it reconnects on its own.
3. **Pick a free seat** (or create one with your name). Busy seats are disabled.
4. Drop images, draw with the pen, scroll to zoom, Space-drag to pan. You can
   only move/delete your own items; everyone else's are read-only.
5. Close the tab to leave — your seat frees automatically.

## Browser support
- Needs **Chrome or Edge** (File System Access API) for the shared folder.
- Works best served over http(s)/localhost; from a raw `file://` path the folder
  picker can be flaky depending on browser version.

## Notes
- On a cloud-synced folder, real latency = however long that service takes to
  sync the file between machines. On a local/LAN folder or two windows on one
  machine, updates are ~1s.
- Claiming a freed seat continues that seat's existing drawings (they stay part
  of the shared pool).
