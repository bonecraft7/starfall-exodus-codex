# Comment Conventions (for GPT)

**JSON**: put a top-level `_gpt_meta` block. Example:

```json
{
  "_gpt_meta": {
    "purpose": "Starfighter duel engine: lock sequences & assists",
    "owner": "Locke",
    "last_touched": "2025-09-21T17:10-07:00",
    "notes": ["Prototype, not final balance"]
  },
  "engine": { "name": "duel", "version": "0.1" }
}
