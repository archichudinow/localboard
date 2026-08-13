# localboard

A single-file, server-free whiteboard you open from a local folder. It behaves
like a lightweight Miro: infinite canvas, pan/zoom, drop images from your
computer, and draw/sketch over them.

## Sharing model — channels
Collaboration works through a **shared folder of JSON files**, one per person:

- Everyone opens the same `index.html` and clicks **Connect folder** (Chrome/Edge),
  granting access to a shared/synced folder (network drive, Dropbox, Drive, OneDrive).
- Each person **claims one channel** = one `board-<name>.json` file, and only ever
  writes to that file. Everyone else's channels render **read-only**.
- Because no two people write the same file, there are **no write conflicts**.
- The board you see is the **union** of every `board-*.json` in the folder.

## Sync
- After the one-time folder grant, the script **auto-saves** your channel on every
  edit and **auto-pulls** everyone else's channels on a timer (~2.5s).
- The **Synchronise** button forces an immediate save + pull.

## Browser support
- **Folder sync:** Chrome or Edge (File System Access API).
- **Safari / Firefox:** use **Export / Import** to move your channel JSON manually.
- Works best served over http(s)/localhost; from a raw `file://` path the folder
  API can be flaky depending on the browser version.

## Use
1. Open `index.html`.
2. Drop images, draw with the pen, scroll to zoom, Space-drag to pan.
3. Click **Connect folder** → pick the shared folder → **claim a channel**.
4. Edit away — it auto-syncs. Others appear as read-only layers.
