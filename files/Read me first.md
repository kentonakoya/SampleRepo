# IT SOP Portal — Read me first

A self-contained IT Standard Operating Procedures portal.  
Upload the whole folder to SharePoint (or serve from GitHub Pages) and your team can read, run, and edit SOPs from one place — with a change log kept automatically.

---

## Folder structure

```
IT SOP Portal/
├─ index.html              ← the portal (open this)
├─ data/
│   ├─ sop-index.json      ← lightweight list of all SOPs (fast load)
│   ├─ change-log.json     ← auto-appended on every save
│   └─ sops/
│       ├─ SOP001.json     ← one file per SOP (loaded on demand)
│       ├─ SOP002.json
│       └─ …
└─ Read me first.md
```

---

## Three modes

| Mode | How to enter | What you can do |
|---|---|---|
| **Read** | Click any SOP in the sidebar | Read purpose, scope, steps, references, change history |
| **Run** | Click "Run as Checklist" | Tick off checklist items step by step; progress bar tracks completion |
| **Edit** | Click "Edit" on any SOP, or "New SOP" | Full form editor: metadata, steps, checklist items, references |

---

## Adding your own SOPs

Two ways:

**Option A — In the portal (easiest):** Click **New SOP** and fill in the form. The portal saves the JSON file automatically.

**Option B — Direct JSON:** Copy any existing file in `data/sops/`, rename it (e.g. `SOP006.json`), edit the content, and add a matching entry to `data/sop-index.json`. The structure is:

```json
{
  "id": "SOP006",
  "title": "Your SOP Title",
  "category": "Security",
  "owner": "IT Manager",
  "status": "Active",
  "version": "1.0",
  "reviewDate": "2026-06-30",
  "tags": ["tag1", "tag2"],
  "summary": "One sentence summary.",
  "purpose": "Why this SOP exists.",
  "scope": "Who it applies to.",
  "roles": [{ "role": "IT Helpdesk", "responsibility": "Does the thing." }],
  "steps": [
    {
      "id": 1,
      "title": "Step title",
      "description": "What to do.",
      "role": "IT Helpdesk",
      "notes": "Optional warning or tip.",
      "checklist": ["Item 1", "Item 2"]
    }
  ],
  "references": ["Reference 1", "Reference 2"],
  "changeHistory": [{ "version": "1.0", "date": "2025-07-01", "author": "You", "notes": "Initial version." }]
}
```

---

## Deploy to SharePoint (same as Risk Portal)

1. **Allow custom scripts** (SharePoint Admin, PowerShell):
   ```powershell
   Set-SPOSite -Identity "https://your-tenant.sharepoint.com/sites/YourSite" -DenyAddAndCustomizePages $false
   ```
2. **Upload the folder** — Upload → Folder → select `IT SOP Portal`
3. **Open `index.html`** from the SharePoint site URL (not by double-clicking)
4. **Set permissions** — Members can edit, Visitors are read-only

## Deploy to GitHub Pages

Commit the folder to a repository, enable GitHub Pages from the repo settings, and open the Pages URL. The portal runs in Local mode (saves to browser localStorage per user).

---

## Good to know

- **One file per SOP** keeps load times fast — the index loads instantly; individual SOPs are fetched only when opened.
- **Run mode is per-session** — checklist progress is stored in memory and resets on page reload. This is intentional (SOPs are procedures to follow, not persistent tasks).
- **Change log** records who created/updated/deleted each SOP and at what version.
- **Concurrent edits** — last save wins on the same SOP. The previous version is recoverable from SharePoint file version history.
- **Categories and statuses** are editable directly in each SOP's form — you're not locked into the defaults.

---

*Part of the Circle Gas IT operations toolkit. Companion to the Group Risk Portal.*
