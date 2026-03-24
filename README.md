# Don't Bonk

A single-file job search tracking dashboard. Kanban board, activity log, interview prep, and more — all stored locally in a JSON file you own.

**[Try the demo →](https://jobsearch.johnstokvis.com/demo.html)**

## Use it yourself

1. Download `index.html` and save it somewhere on your computer
2. Create a `data.json` file in the same folder containing just `{}`
3. Open `index.html` in Chrome or Edge (requires the [File System Access API](https://caniuse.com/native-filesystem-api))
4. Click **link data.json** in the top right and select your `data.json`
5. All changes save directly to that file — your data never leaves your computer

---

## Files

- `index.html` — the app. Open in any browser.
- `data.json` — all application data. This is the source of truth.
- `README.md` — this file.

---

## Using with Claude Cowork

Point Cowork at this folder. Then say things like:

- "Add a new application for Senior PM at Notion in the 'Feeling things out' column"
- "Mark the Meta application as rejected"
- "Move Webflow to the Offer column"
- "Add a note to the Stripe card: 'Had a call with the hiring manager today, went well'"
- "Update the Stripe salary to $275,000"
- "Show me all companies currently in the interviewing stages"
- "Which applications haven't had any activity in the last 30 days?"

Cowork should edit `data.json` directly. The app reads `data.json` on load — just refresh the browser after Cowork makes changes.

---

## Using with Claude Code

Open this folder in Claude Code. Then say things like:

- "Add a Priority field (High / Medium / Low) to each card"
- "Add a new column between 'Team matching' and 'Offer' called 'Final round'"
- "Change the color scheme to light mode"
- "Add a search bar to filter cards by company name"
- "Add a way to attach a resume version to each application"
- "Export all applications to a CSV"

Claude Code edits `index.html` directly.

---

## Data format (data.json)

```json
{
  "meta": {
    "lastUpdated": "Mar 19, 2026",
    "version": "1.0"
  },
  "columns": [
    { "id": "feeling", "label": "Feeling things out" },
    { "id": "applied", "label": "Application submitted" },
    { "id": "recruiter", "label": "Recruiter screen" },
    { "id": "hiring", "label": "Hiring manager interview" },
    { "id": "written", "label": "Written exercise" },
    { "id": "group", "label": "Group interview" },
    { "id": "team", "label": "Team matching" },
    { "id": "offer", "label": "Offer" },
    { "id": "rejected", "label": "Rejected" }
  ],
  "applications": [
    {
      "id": "c1",
      "status": "feeling", // column id
      "role": "Staff PM",
      "company": "Reddit",
      "salary": "$180,000",
      "bonus": "$20,000",
      "equity": "$50,000",
      "source": "In-network recruiter",
      "link": "https://...",
      "startDate": "Mar 19, 2026",
      "steps": ["Outbound", "Recruiter screen"], // completed interview steps
      "notes": [{ "date": "Mar 19, 2026", "text": "Had first recruiter call" }],
      "jobDescription": "Paste of JD or prep notes",
      "resources": ""
    }
  ]
}
```

### Valid status values (column ids)

`feeling` · `applied` · `recruiter` · `hiring` · `written` · `group` · `team` · `offer` · `rejected`

### Valid steps

`Outbound` · `Recruiter screen` · `Product sense interview` · `Written exercise` · `Group interview` · `Hiring manager interview` · `Team matching`

---

## Saving data

The app stores edits in `localStorage` automatically. To sync those edits back to `data.json`:

- Click **"export data.json ↓"** in any card's detail panel, then replace the file in this folder.
- OR let Cowork / Claude Code be the primary way you make edits — they write to `data.json` directly, and you just refresh the browser.

The cleanest workflow: **use Cowork/Claude Code for bulk edits, use the browser UI for quick daily updates + note-logging.**
