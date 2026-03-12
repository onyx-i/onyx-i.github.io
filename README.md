# Music Player — GitHub Pages

A clean, dark-themed music player that hosts your MP3 files with album art and lyrics extracted directly from embedded ID3v2 tags. No backend needed — runs entirely on GitHub Pages.

## Quick Setup

1. **Create a GitHub repo** and enable GitHub Pages (Settings → Pages → Source: `main` branch)

2. **Copy these files** into the repo root:
   - `index.html` — the player
   - `tracks.json` — your track listing

3. **Create a `tracks/` folder** and add your `.mp3` files

4. **Edit `tracks.json`** to list your tracks:

```json
[
  {
    "file": "tracks/my-song.mp3",
    "title": "My Song",
    "artist": "Artist Name",
    "album": "Album Name"
  }
]
```

5. **Push and visit** `https://yourusername.github.io/your-repo-name/`

## How It Works

The player fetches each MP3 file and parses the ID3v2 binary header directly in the browser:

- **Album Art**: Extracted from the APIC frame embedded in your MP3. No separate image files needed.
- **Lyrics**: Extracted from the USLT (unsynchronized lyrics) frame embedded in your MP3. You can also override with a `.txt` file of the same name if you prefer.
- **Title / Artist / Album**: Uses whatever you put in `tracks.json` first, then falls back to the ID3 TIT2, TPE1, and TALB frames.

Since the player downloads the full MP3 to parse ID3 tags, thumbnails in the track list may take a moment to appear on slower connections.

## Optional: Lyrics .txt Override

If you'd rather supply lyrics as a separate text file instead of relying on the embedded ID3 tag:
- Add a `.txt` file with the same name as the MP3 (e.g. `tracks/my-song.txt`)
- Or specify it explicitly in tracks.json: `"lyrics": "tracks/my-song.txt"`

The `.txt` file takes priority over embedded lyrics.

## Features

- Embedded ID3v2 album art + lyrics extraction (no extra files needed)
- Dark, minimal UI with smooth animations
- Play/pause, prev/next, progress scrubbing, volume control
- Keyboard shortcuts: Space (play/pause), ←/→ (seek 5s)
- OS media controls integration (Media Session API) with album art
- Auto-advances to next track
- Mobile-responsive
- No dependencies, no build step — just static HTML/CSS/JS

## File Size Note

GitHub Pages repos have a soft limit of ~1 GB. Keep your MP3 collection reasonable, or consider using Git LFS for larger files.
