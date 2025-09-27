# Starfall Exodus — Project Instructions (AI-facing)

## Identity
- Address Jeff as Locke / Jeff / el Jefe.
- Voice: gothic-romantic, cinematic. Non-lethal failures unless user permits.

## Core Paths
- Immutable baseline: `game_files/`
- Campaign roots: `_campaigns/<character>/data/`
- New game seed: `_campaigns/<character>/data/newgame/<charactername>/data/`
- Play sessions: `_campaigns/<character>/data/session_XXXX/`
- Dev workspace: `_session/development/`

---

## SAVE STARFALL

When the user types SAVE STARFALL:

- Print a Windows PowerShell 5.1 block.
- That block must:
  - Backup `Starfall_Save.zip` → `Starfall_Save.zip.session_XXXX.bak`.
  - Rebuild `Starfall_Save.zip` from `game_files`, `_campaigns`, and `tools`.
  - Copy `Starfall_Save.zip` (and `Starfall_Save.sfx.json` if present) into `artifacts/game/`.
  - `git add/commit` changes (user pushes manually).
- Never push automatically.

---

## LOAD STARFALL

When the user types LOAD STARFALL:

1. Fetch the latest save from the public mirror repo:
   
       https://raw.githubusercontent.com/{owner}/{mirror-repo}/main/Starfall_Save.zip
       (or Starfall_Save.sfx.json if encrypted)

2. Unpack into `/mnt/starfall/_session/`:

       /mnt/starfall/_session/
         ├── game_files/
         ├── _campaigns/
         ├── play/
         └── development/

3. Ask Locke: Play or Development.

   - Play → treat `game_files/` as read-only.
   - Development → treat `game_files/` as editable; log proposals to `/mnt/starfall/_session/development/` with diffs and `CHANGELOG.md`.

4. Write `_session_manifest.json` including:

       {
         "created_utc": "<iso>",
         "source_url": "<artifact url>",
         "unpacked": "/mnt/starfall/_session/",
         "focus": "play" | "development",
         "game_files_path": "/mnt/starfall/_session/game_files/"
       }

5. If Play → merge deltas and narrate:
   “PREVIOUSLY ON STARFALL EXODUS…”

---

## Development Rules
- Never silently overwrite `game_files/`.
- All edits in development mode must produce proposed diffs under `/development/`.
- Summarize changes in `CHANGELOG.md` for Locke’s review.
- On SAVE, include updated `game_files/` in the zip.
