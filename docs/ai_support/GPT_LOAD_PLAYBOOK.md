# GPT_LOAD_PLAYBOOK.md
1) Obtain Starfall_Save.zip (or .sfx.json for encrypted build).
2) Unpack to /mnt/starfall/_session/ (or local /mnt/data/starfall/_session).
3) Ensure subdirs: game_files/, _campaigns/, play/, development/, docs/, tools/.
4) Write _session_manifest.json with {created_utc, source_url, unpacked, focus, game_files_path}.
5) If Play focus: reconstruct state and produce PREVIOUSLY recap.
6) If Development: stage all edits under development/ with CHANGELOG.md and diffs. Never mutate game_files/ directly except during formal merges.

=======
# GPT LOAD PLAYBOOK — Starfall Exodus

## Trigger
User types: LOAD STARFALL

---

## Steps

1. Download latest save
   - Prefer `Starfall_Save.zip` from the public mirror:
     
         https://raw.githubusercontent.com/{owner}/{mirror-repo}/main/Starfall_Save.zip
     
   - If encryption is used, fetch `Starfall_Save.sfx.json` and request the passphrase once.

2. Unpack to session root

       /mnt/starfall/_session/
         ├── game_files/
         ├── _campaigns/
         ├── play/
         └── development/

3. Select focus
   - Ask: Play or Development?

4. Focus behaviors
   - Play Mode
     - `game_files/` = read-only reference.
     - Apply deltas from latest `_campaigns/<character>/data/session_XXXX/`.
     - Deliver recap: “PREVIOUSLY ON STARFALL EXODUS…”
   - Development Mode
     - `game_files/` = editable.
     - Write all edits as proposed patches in `/mnt/starfall/_session/development/`.
     - Maintain `/mnt/starfall/_session/development/CHANGELOG.md`.

5. Write manifest

       {
         "created_utc": "<iso>",
         "source_url": "<mirror url>",
         "unpacked": "/mnt/starfall/_session/",
         "focus": "play" | "development",
         "game_files_path": "/mnt/starfall/_session/game_files/"
       }
