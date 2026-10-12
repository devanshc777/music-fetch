# music-fetch

A Claude Code skill that downloads audio tracks from YouTube (or any yt-dlp-supported site) into a
local music inbox, ready for browser decode in [dj-holo](https://github.com/devanshc777/dj-holo).
Reuses the yt-dlp installation inside [yt-vault](https://github.com/devanshc777/yt-vault)'s venv —
no global install.

"Grab this track" → m4a/webm lands in the inbox → drag into the deck.

## Behavior

- Saves audio-only (m4a/webm) at source quality
- Enforces a licensing rule: royalty-free / NCS / owned content for anything that leaves the machine
- Batch mode for pulling practice sets

## Install (Claude Code)

```bash
git clone https://github.com/devanshc777/music-fetch.git
```

Then link the clone into your skills folder.

Windows (PowerShell):

```powershell
New-Item -ItemType Junction -Path "$env:USERPROFILE\.claude\skills\music-fetch" -Target "<clone-path>"
```

macOS / Linux:

```bash
ln -s "<clone-path>" ~/.claude/skills/music-fetch
```

Part of a personal music-learning pipeline; the inbox path in `SKILL.md` assumes that setup — adjust to yours.

## License

MIT
