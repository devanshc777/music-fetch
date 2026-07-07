---
name: music-fetch
description: Download audio tracks from YouTube (or other yt-dlp-supported sites) into Devansh's music inbox for DJ practice in dj-holo. Use when the user asks to "download this song/track", "get audio from this link", "fetch music", "grab tracks for djing", or wants royalty-free/NCS music pulled locally. Saves to C:\Personal\inbox\music as m4a/webm ready for browser decode.
---

# music-fetch — pull audio into the music inbox

Downloads audio via the **yt-dlp inside yt-vault's venv** (no global install needed).
Target folder: `C:\Personal\inbox\music\` — dj-holo's library accepts these via drag-drop/ADD TRACKS.

## Licensing rule

Prefer royalty-free sources: NoCopyrightSounds (NCS), Free Music Archive, artists' own CC uploads.
Copyrighted tracks: personal practice only — never redistribute, never publish recorded mixes of them.

## Download one track

```powershell
Set-Location C:\Dev\python\projects\yt-vault
uv run yt-dlp --js-runtimes node -f "bestaudio[ext=m4a]/bestaudio" `
  -o "C:\Personal\inbox\music\%(title)s.%(ext)s" `
  --no-playlist "<URL>"
```

No ffmpeg on this machine → do NOT use `-x`/`--extract-audio` or `--audio-format mp3`
(those need ffmpeg). Native `bestaudio` (m4a/webm/opus) decodes fine in the browser.

## Search then download (no URL given)

```powershell
Set-Location C:\Dev\python\projects\yt-vault
uv run yt-dlp --js-runtimes node "ytsearch5:<query> NCS" --get-title --get-id   # list candidates
# then download by id:
uv run yt-dlp -f "bestaudio[ext=m4a]/bestaudio" -o "C:\Personal\inbox\music\%(title)s.%(ext)s" "https://www.youtube.com/watch?v=<ID>"
```

## After download

- Tell the user the saved path(s).
- For DJ use: open dj-holo (`C:\Dev\fullstack\dj-holo`, `npm run dev`, :5199) → LIBRARY → ADD TRACKS → pick from `C:\Personal\inbox\music`.
- Finished recorded mixes belong in `C:\Personal\exports\mixes\` (move from Downloads).

## Troubleshooting

- Always pass `--js-runtimes node` — machine has no deno; without it YouTube extraction warns/degrades.

- 403/429: add `--cookies-from-browser firefox` (Chrome DPAPI fails on this machine).
- Age-gated: same cookies flag.
- If `uv` missing in the project: run `uv sync` in `C:\Dev\python\projects\yt-vault` once.
