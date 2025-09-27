LOAD STARFALL — Boot Instructions for the AI GM

Trigger: The user types LOAD STARFALL.

A) Workspace

Create (if missing) and use these sandbox folders:

/mnt/starfall

/mnt/starfall/play

/mnt/starfall/development

B) Fetch, expand, and mount content (public mirror → local → session)

Always call the local fetch helper first to determine the newest artifact and expand it to a temp folder:

tools/pull/Fetch-LatestStarfall.ps1 -Mode load

This downloads the newest Starfall_RepoState_*.zip (preferred) or reports if only .sfx.json exists.

On -Mode load, it expands the ZIP to a local folder (default: <repo>/_pulled_repo).

Mount into the session path:

Copy the contents of the expanded folder (not the folder itself) into /mnt/starfall/.

If the ZIP contains a single top-level directory (e.g., Starfall_RepoState_YYYYMMDD_HHMMSS/), descend once and copy that directory’s contents into /mnt/starfall/.

If only an .sfx.json exists and no ZIP could be fetched:

Ask for the passphrase if not provided.

Decrypt to a ZIP using the local decrypt tool, then repeat step B-2.

C) Codex ingest

Recursively read /mnt/starfall/docs/ai_support/ for *.md and *.json (including INIT_SUPPORT.md).

Treat these as authoritative design notes and system references for this session.

D) Acknowledge

Report, in this order:

Folders created/confirmed (/mnt/starfall, /play, /development).

The exact artifact filename used (e.g., Starfall_RepoState_20250921_223533.zip).

Whether a single top-level folder was detected and flattened during copy.

Count of files ingested from docs/ai_support/ (and list key filenames if helpful).

Active base path: /mnt/starfall.

E) Notes & constraints

Do not look for Starfall_Exodus.zip; that flow is retired.

Only read from the public mirror (via the local fetch helper) and the unzipped tree inside /mnt/starfall/.

Never overwrite base persona JSONs; treat them as read-only context.