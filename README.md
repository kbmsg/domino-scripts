# Domino Script AI

An AI-powered script generator for HCL Domino administrators.
Describe what you need in plain English and get production-ready scripts instantly - no scripting expertise required.

Live code for you to use: [https://kbmsg.github.io/domino-scripts/](https://kbmsg.github.io/domino-scripts/)

Version #: 80 May 19, 2026 — now with Ollama, OpenRouter, and Claude AI options. DRAPI save to Domino is now available.

---

## What It Does

Domino Script AI uses the Anthropic Claude API, OpenRouter, or Ollama to generate complete, commented, error-handled scripts for common HCL Domino administration tasks. It supports four output languages and covers nine administration categories, from server management to DAOS archiving.

Scripts are generated fresh on demand, tailored to your selected Domino version, target server, and task description. It now includes the DRAPI option so you can save your scripts directly to your environment in an NSF file. Details below.

---

## Getting Started

### Prerequisites

You need a free Anthropic API key, Ollama installed locally, or an OpenRouter account to use this tool.

**Anthropic:**
- Go to [console.anthropic.com](https://console.anthropic.com/)
- Sign up or log in
- Navigate to **API Keys** and create a new key
- Copy the key — it starts with `sk-ant-`

**Ollama:**
- Install Ollama from [ollama.com](https://ollama.com)
- Run `OLLAMA_ORIGINS=* ollama serve` in your terminal
- Pull a model with `ollama pull llama3`
- Switch the toggle to Ollama, enter the model name, click Save
- Supports llama3, mistral, codellama and any other installed model
- All settings persist across refreshes — provider choice, URL, and model name saved to localStorage

**OpenRouter:**
- Go to [openrouter.ai](https://openrouter.ai) and create a free account
- Generate an API key — it starts with `sk-or-`
- Switch the toggle to OpenRouter, enter your key and a model name (e.g. `openai/gpt-4o`, `google/gemini-pro`)
- Click Save

### Running the App
*(Tested with v9 and newer, but should work for earlier versions as well)*

**Option A — Use the hosted version**
Open [https://kbmsg.github.io/domino-scripts/](https://kbmsg.github.io/domino-scripts/) in any modern browser.

**Option B — Run locally**
- Download `index.html` from this repository
- Open it directly in your browser — no web server or installation needed

### Entering Your API Key

At the top of the page, paste your API key into the appropriate field and click **Save Key**. A green confirmation badge confirms it has been accepted. The key is stored in your browser's local storage only — it is never sent anywhere except directly to the selected AI provider. If you clear your browser cache you will need to re-enter it. I suggest copying it to a text file for future use.

---

## Interface Overview

### API Key Bar

The dark strip at the very top of the page. Select your AI provider (Anthropic, OpenRouter, or Ollama) using the toggle, then enter the relevant credentials. Settings persist across sessions.

---

### Left Sidebar

#### Script Categories

Nine category buttons filter the context sent to the AI, improving the relevance of generated scripts. Click a category before describing your task.

| Category | Covers |
|---|---|
| Server Management | Start/stop tasks, server configuration, console commands |
| Database Admin | Compacting, fixup, quotas, database properties |
| Mail & Routing | Mail routing, dead mail, mailbox management |
| Security & ACL | Access control lists, ID certificates, encryption |
| Replication | Push/pull replication, replication schedules, conflicts |
| User & Directory | Onboarding, offboarding, group management, NAB edits |
| Performance & Monitoring | Stats, log parsing, task monitoring, diagnostics |
| DAOS & Archiving | DAOS configuration, NLO management, archiving policies |
| Agents & Scheduling | Agent scheduling, agent log review, triggering agents |

#### Quick Templates

Eight pre-built prompts that load a complete task description, category, and language with a single click. Use these as starting points or run them as-is.

| Template | What It Generates |
|---|---|
| Compact all databases | Compacts fragmented NSF files and logs before/after sizes |
| Clear dead mail | Removes dead mail older than 7 days from mail.box |
| Dump ACL to file | Exports every database ACL to a CSV file |
| Force replication push | Pushes all databases to a named replica server |
| Offboard user | Removes a user from groups, renames their mail file, sends admin confirmation |
| Check cert expiry | Reports ID certificates expiring within 60 days |
| Set mail quotas | Applies size quotas to mail files exceeding a threshold |
| Parse notes.log | Extracts and groups ERROR/FAULT entries from the last 24 hours |

---

### Main Panel

#### Request Console

**Server** — Select a server you have added in the My Servers panel (right sidebar). The selected server name is included in the prompt sent to the AI so the script can reference it directly. Leave blank for a generic script.

**Domino Version** — Choose your exact Domino release from the dropdown, including fix packs. The AI tailors API usage, command syntax, and feature availability to this version. Versions supported range from IBM Domino 9.0 through HCL Domino 14.5.1.

**Describe what you need** — Type a plain English description of the task. Be as specific as you like — the more detail you provide, the more accurate the output. You can reference field names, thresholds, file paths, or conditions.

Good examples:
- *Find all databases larger than 2 GB, log their paths and sizes, then email me a summary*
- *Remove a selected user from all groups in names.nsf and rename their mail file with an EXIT- prefix*
- *Check for ERROR entries in notes.log from the last 24 hours and group them by type*

Press **Ctrl+Enter** (or **Cmd+Enter** on Mac) to generate without reaching for the mouse.

**Generate Script** — Sends your request to the selected AI provider. Generation typically takes 5–15 seconds, depending on script complexity.

**Clear** — Resets the prompt field and output area.

---

### Output Panel

Displays the generated script with syntax highlighting. A plain-English explanation of what the script does, its prerequisites, and how to run it appears below the code.

**Copy** — Copies the full script to your clipboard.

**Save File** — Downloads the script as a file with the correct extension for the selected language (`.lss`, `.java`, `.txt`).

**Save to Library** — Saves the script to your local browser script library (right sidebar) so you can reload it later without regenerating.

**Save to Domino** — Saves the script directly to your HCL Domino server in `scripts.nsf` so you can share scripts among your team and maintain documentation. Requires DRAPI to be configured — see the Save to Domino section below.

---

### Right Sidebar

#### My Servers
Add your Domino server names here (e.g. `MAIL01/ACME`). Saved servers appear in the Server dropdown in the Request Console and persist across sessions using browser storage. Click the **✕** next to any server to remove it.

#### Saved Scripts
Scripts saved via the **Save to Library** button appear here, newest first. Each entry shows the script title (derived from your prompt), language, server, and date saved. Click any entry to reload it into the output panel. Click **✕** to delete it. Saved scripts persist in browser storage across sessions.

#### Output Type
Select the scripting language before generating. The file extension on the Save button updates to match.

| Language | Use Case |
|---|---|
| LotusScript | General-purpose automation via Notes Object Model |
| Domino Console Commands | Direct server console instructions |
| Java (Notes API) | Enterprise integrations using the Notes Java API |
| Formula Language | Views, fields, agents, and simple computed values |

#### Save to Domino
Enter your DRAPI server URL, username, password, NSF path, and scope name to save generated scripts directly to your Domino server. See the Save to Domino section below for full setup instructions.

---

## Save to Domino (DRAPI)

Generated scripts can be saved directly to an HCL Domino document library database called `scripts.nsf` on your Domino server. This requires HCL Domino REST API (DRAPI) to be installed and configured.

### Prerequisites

- HCL Domino REST API v1.1.3 or later installed on your Domino server
- A database called `scripts.nsf` with a form called **Script** containing these fields:
  - `ScriptTitle` — Text
  - `ScriptBody` — Text or Rich Text
  - `ScriptLanguage` — Text
  - `ScriptCategory` — Text
  - `ScriptServer` — Text
  - `ScriptDate` — Text
  - `ScriptVersion` — Text
- A DRAPI schema and scope configured for `scripts.nsf`
- CORS configured in DRAPI to allow requests from `https://kbmsg.github.io`

### Setting Up the DRAPI Schema and Scope

**1. Verify DRAPI is running** — on your Domino server console, type `show tasks`. You should see `restapi` listed. If not, run `load restapi`.

**2. Open the Admin UI** at `https://yourserver:8880` and log in with your Domino credentials.

**3. Create a Schema** — click Database Management → Add Schema → Create Schema. Select `scripts.nsf`, name the schema `scripts`, and enable the Script form with all seven fields listed above.

**4. Create a Scope** — click Scopes → Add Scope. Set the scope name to `scripts` (lowercase), link it to the `scripts` schema, set Maximum Access to Editor, and make sure Active is ticked.

**5. Configure CORS** — in your Domino data directory, open `keepconfig.d\cors.json` and make sure it contains valid regex entries. Since DRAPI v1.1.3, CORS uses Java Regular Expressions:

```json
{
  "CORS": {
    "^https:\\/\\/kbmsg\\.github\\.io$": true,
    "^https?:\\/\\/localhost(?:\\:\\d+)?$": true
  }
}
```

If you are hosting the app on your own domain instead of GitHub Pages, replace the first entry with your domain. For example for `mycompany.com`:

```json
{
  "CORS": {
    "^https:\\/\\/mycompany\\.com(?:\\:\\d+)?$": true,
    "^https?:\\/\\/.*\\.mycompany\\.com(?:\\:\\d+)?$": true,
    "^https?:\\/\\/localhost(?:\\:\\d+)?$": true
  }
}
```

The pattern `.*\\.mycompany\\.com` covers all subdomains. The `(?:\\:\\d+)?` part makes the port number optional. Note that dots must be escaped as `\\.` and forward slashes as `\\/` inside JSON regex strings.

After saving, restart DRAPI:
```
tell restapi quit
load restapi
```

**6. Test the connection** — open the browser console on your GitHub Pages site and run:
```javascript
(async () => {
  const r = await fetch('https://yourserver:8880/api/v1/auth', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ username: 'yourshortname', password: 'yourpassword' })
  });
  const b = await r.json();
  console.log(r.status, b);
})();
```
A Status 200 with a `bearer` token confirms everything is working.

### Using the Save to Domino Feature

The **🗄️ Save to Domino** panel appears in the right sidebar. Fill in the connection settings and click **Save Connection Settings** — the URL, username, database path, and scope name are saved to localStorage. The password is never saved and must be entered each session.

| Field | Description |
|---|---|
| DRAPI Server URL | Full URL including port, e.g. `https://yourserver:8880` |
| Username | Your Domino short name or internet address |
| Password | Your Domino password — entered each session, never stored |
| Database (NSF path) | Path to the database, e.g. `scripts.nsf` |
| Scope name | The DRAPI scope name, e.g. `scripts` |

Once a script has been generated, click the **🗄️ Save to Domino** button in the output panel. The app authenticates against your DRAPI server and saves the script as a document with all seven fields populated. On success, it shows the document UNID confirming the save.

---

## Important Notes

**Console command accuracy** — The AI is instructed to only use documented HCL/IBM Domino console commands and will flag any command it cannot fully verify with a `⚠ VERIFY` comment. Always test console command scripts in a non-production environment first.

**No data leaves your browser** — Your API keys and saved scripts are stored only in your browser's local storage. No usage data, prompts, or scripts are collected by this application. The password for Domino is never stored anywhere.

**API costs** — Each script generation makes one call to your chosen AI provider. Typical scripts use 1,000–3,000 tokens. At current Anthropic pricing, this is a fraction of a cent per generation. Monitor your usage at [console.anthropic.com](https://console.anthropic.com/).

---

## Repository Structure

```
domino-scripts/
├── index.html    # The entire application — single self-contained file
└── README.md     # This file
```

---

## Contributing

Pull requests are welcome. If you have a useful Quick Template to suggest or find a bug, please open an issue. But I am not a developer, so you may be better off fixing it yourself and letting me know what you did 😊

---

## License

MIT — free to use, modify, and distribute.
