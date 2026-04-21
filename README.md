**Domino Script AI**

An AI-powered script generator for HCL Domino administrators.
Describe what you need in plain English and get production-ready scripts instantly - no scripting expertise required.

Live demo: <https://kbmsg.github.io/domino-scripts/>

Version #: 45 April 21, 2026

**What It Does**

Domino Script AI uses the Anthropic Claude API to generate complete, commented, error-handled scripts for common HCL Domino administration tasks. It supports four output languages and covers nine administration categories, from server management to DAOS archiving.

Scripts are generated fresh on demand, tailored to your selected Domino version, target server, and task description.

**Getting Started**

**Prerequisites**

You need a free Anthropic API key to use this tool.

- Go to [console.anthropic.com](https://console.anthropic.com/)
- Sign up or log in
- Navigate to **API Keys** and create a new key
- Copy the key - it starts with sk-ant-

**Running the App** (Tested with v9 and newer, but should work for earlier versions as well)

**Option A - Use the hosted version** Open <https://kbmsg.github.io/domino-scripts/> in any modern browser.

**Option B - Run locally**

- Download index.html from this repository
- Open it directly in your browser - no web server or installation needed

**Entering Your API Key**

At the top of the page, paste your Anthropic API key into the **API Key** field and click **Save Key**. A green confirmation badge confirms it has been accepted. The key is stored in your browser's session storage only - it is never sent anywhere except directly to Anthropic's API, and it is stored locally now when you close the tab. However, if you clear your cache, you will need to replace the api key. I suggest you copy it to a text file for future usage.

**Interface Overview**

**API Key Bar**

The dark strip at the very top of the page. Enter your sk-ant-... key here before generating scripts. The eye icon toggles visibility of the key. The key persists for the duration of your browser session.

**Left Sidebar**

**Script Categories**

Nine category buttons filter the context sent to the AI, improving the relevance of generated scripts. Click a category before describing your task.

| **Category**             | **Covers**                                               |
| ------------------------ | -------------------------------------------------------- |
| Server Management        | Start/stop tasks, server configuration, console commands |
| Database Admin           | Compacting, fixup, quotas, database properties           |
| Mail & Routing           | Mail routing, dead mail, mailbox management              |
| Security & ACL           | Access control lists, ID certificates, encryption        |
| Replication              | Push/pull replication, replication schedules, conflicts  |
| User & Directory         | Onboarding, offboarding, group management, NAB edits     |
| Performance & Monitoring | Stats, log parsing, task monitoring, diagnostics         |
| DAOS & Archiving         | DAOS configuration, NLO management, archiving policies   |
| Agents & Scheduling      | Agent scheduling, agent log review, triggering agents    |

**Quick Templates**

Eight pre-built prompts that load a complete task description, category, and language with a single click. Use these as starting points or run them as-is.

| **Template**           | **What It Generates**                                                         |
| ---------------------- | ----------------------------------------------------------------------------- |
| Compact all databases  | Compacts fragmented NSF files and logs before/after sizes                     |
| Clear dead mail        | Removes dead mail older than 7 days from mail.box                             |
| Dump ACL to file       | Exports every database ACL to a CSV file                                      |
| Force replication push | Pushes all databases to a named replica server                                |
| Offboard user          | Removes a user from groups, renames their mail file, sends admin confirmation |
| Check cert expiry      | Reports ID certificates expiring within 60 days                               |
| Set mail quotas        | Applies size quotas to mail files exceeding a threshold                       |
| Parse notes.log        | Extracts and groups ERROR/FAULT entries from the last 24 hours                |

**Output Type**

Select the scripting language before generating. The file extension on the Save button updates to match.

| **Language**            | **Use Case**                                      |
| ----------------------- | ------------------------------------------------- |
| LotusScript             | General-purpose automation via Notes Object Model |
| Domino Console Commands | Direct server console instructions                |
| Java (Notes API)        | Enterprise integrations using the Notes Java API  |
| Formula Language        | Views, fields, agents, and simple computed values |

**Main Panel**

**Request Console**

**Server** - Select a server you have added in the My Servers panel (right sidebar). The selected server name is included in the prompt sent to the AI so the script can reference it directly. Leave blank for a generic script.

**Domino Version** - Choose your exact Domino release from the dropdown, including fix packs. The AI tailors API usage, command syntax, and feature availability to this version. Versions supported range from IBM Domino 9.0 through HCL Domino 14.5.

**Describe what you need** - Type a plain English description of the task. Be as specific as you like - the more detail you provide, the more accurate the output. You can reference field names, thresholds, file paths, or conditions.

Good examples:

- _Find all databases larger than 2 GB, log their paths and sizes, then email me a summary_
- _Remove a selected user from all groups in names.nsf and rename their mail file with an EXIT- prefix_
- _Check for ERROR entries in notes.log from the last 24 hours and group them by type_

Press **Ctrl+Enter** (or **Cmd+Enter** on Mac) to generate without reaching for the mouse.

**Generate Script** - Sends your request to the Claude API. Generation typically takes 5-15 seconds depending on script complexity.

**Clear** - Resets the prompt field and output area.

**Output Panel**

Displays the generated script with syntax highlighting. A plain-English explanation of what the script does, its prerequisites, and how to run it appears below the code.

**Copy** - Copies the full script to your clipboard.

**Save File** - Downloads the script as a file with the correct extension for the selected language (.lss, .java, .txt).

**Save to Library** - Saves the script to your local script library (right sidebar) so you can reload it later without regenerating.

**Right Sidebar**

**My Servers**

Add your Domino server names here (e.g. MAIL01/ACME). Saved servers appear in the Server dropdown in the Request Console and persist across sessions using browser storage. Click the **✕** next to any server to remove it.

**Saved Scripts**

Scripts saved via the **Save to Library** button appear here, newest first. Each entry shows the script title (derived from your prompt), language, server, and date saved. Click any entry to reload it into the output panel. Click **✕** to delete it. Saved scripts persist in browser storage across sessions.

**Important Notes**

**Console command accuracy** - The AI is instructed to only use documented HCL/IBM Domino console commands and will flag any command it cannot fully verify with a ⚠ VERIFY comment. Always test console command scripts in a non-production environment first.

**No data leaves your browser** - Your API key and saved scripts are stored only in your browser (session storage and local storage respectively). No usage data, prompts, or scripts are collected by this application.

**API costs** - Each script generation makes one call to the Anthropic API. Typical scripts use 1,000-3,000 tokens. At current Anthropic pricing this is a fraction of a cent per generation. Monitor your usage at [console.anthropic.com](https://console.anthropic.com/).

**Repository Structure**

domino-scripts/

└── index.html # The entire application - single self-contained file

└── README.md # This file

**Contributing**

Pull requests are welcome. If you have a useful Quick Template to suggest or find a bug, please open an issue. But I am not a developer, so you may be better off fixing it for yourself, and letting me know what you did 😊

**License**

MIT - free to use, modify, and distribute.
