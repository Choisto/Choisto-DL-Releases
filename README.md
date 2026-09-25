# Choisto DL

A Jellyfin plugin that downloads direct links, 1fichier, Torbox, magnets and .torrent files straight into your libraries.

**[Download the latest version](https://github.com/Choisto/Choisto-DL-Releases/releases/latest)** · Jellyfin 12.1 or later

<!-- Shown under the changelog on every release page. Keep each paragraph on one line: GitHub turns every line break in release notes into a visible one. -->

## What is Choisto DL?

A download manager built into Jellyfin. Paste a link, pick a library, and the server downloads the file, renames it the way Jellyfin expects and files it into the library.

## Features

**Downloads page in the main menu** (administrators only)
- Paste up to 200 links at once: one per line, or a block of text copied from a page. Links are picked out of the text, duplicates are skipped, and the ones that are refused stay in the field with the reason.
- Follow the queue live: progress, speed, pause, resume, cancel.
- The queue survives restarts and updates; an interrupted download picks up where it left off.

**Supported sources**
- **Direct HTTP / HTTPS links**, with interrupted transfers resumed.
- **1fichier**: through a Premium API key (full speed, several at once, resumable; *not tested against a live account*), or for free, as a guest or signed in to an account, with queues and waiting times handled automatically.
- **Torbox** (debrid service): links to the file hosts Torbox supports, **magnet links** and **.torrent files**. A torrent becomes one download per video (samples, subtitles and images are left out); once it is imported, the plugin removes the torrent from the Torbox account, but only if the plugin added it there.

**Smart series (with Torbox)**

A torrent sent to a TV shows library is not downloaded in full: it stays on Torbox and every episode shows up in Jellyfin straight away, streamed. Only the episode being watched and the next ones (3 by default) are kept on disk, for each viewer; watched episodes are freed after 7 days.

**Importing into libraries**
- Automatic renaming following Jellyfin's conventions, for example:
  - `The.Matrix.1999.1080p.BluRay.x264-GRP.mkv` → `The Matrix (1999)/The Matrix (1999).mkv`
  - `Breaking.Bad.S01E02.720p.HDTV.mkv` → `Breaking Bad/Season 01/Breaking Bad S01E02.mkv`
- **Archive extraction** for `.rar` (multi-volume included), `.zip` and `.7z`, with nothing to install.
- Library scan after an import, combined into one when several downloads finish together.
- An existing file is never overwritten.

**Reliability**
- Automatic retries on network errors (dropped connection, timeout, 5xx error…), waiting longer before each attempt.
- Files too small to be videos (20 MB by default), such as an error page saved under a film's name, are refused.

## Installation

Requires **Jellyfin 12.1** or later.

1. In Jellyfin, open **Dashboard → Plugins → Repositories** and add:
   ```
   https://github.com/Choisto/Choisto-DL-Releases/releases/latest/download/manifest.json
   ```
2. Install **Choisto DL** from the catalog, then restart the server.
3. Set the plugin up under **Dashboard → Plugins → Choisto DL** (1fichier and Torbox keys, working directory, concurrent downloads…), then open **Downloads** from the main menu.

Updates then show up directly in Jellyfin's catalog.
