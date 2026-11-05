# Command Center Design Spec

Generic build specification for a 3-dashboard, voice-driven business command center. Use this to build a new instance from scratch.

---

## What You Are Building

Three connected single-file HTML dashboards plus a voice layer, deployed to Cloudflare Pages. The whole system runs in any modern browser. No backend other than a tiny Cloudflare Worker for KV writes (optional).

```
┌──────────────────────────────────────────────────────────────────────┐
│                      COMMAND BRIDGE (center)                          │
│  ┌──────────────────┐  ┌────────────────────┐  ┌──────────────────┐  │
│  │  AI OPS COLUMN   │  │  REACTOR + BRAIN    │  │  AGENCY OPS COL  │  │
│  │  5-8 summary     │  │  + VOICE ASSISTANT  │  │  5-8 summary     │  │
│  │  panels          │  │  + GLOBAL SEARCH    │  │  panels          │  │
│  └──────────────────┘  └────────────────────┘  └──────────────────┘  │
│                                                                        │
│   Bottom toolbar: STOP, MIC, SEARCH, CONFIG, BRIEF, QUICK ACTIONS     │
│   Status bar: 8 connector status pills                                │
└──────────────────────────────────────────────────────────────────────┘
       click sun (left header)              click galaxy (right header)
              ↓                                       ↓
┌──────────────────────────────┐      ┌──────────────────────────────┐
│   AI OPS COMMAND CENTER       │      │  AGENCY OPS COMMAND CENTER   │
│   (full-screen iframe)        │      │  (full-screen iframe)        │
└──────────────────────────────┘      └──────────────────────────────┘
```

The Bridge is the center. AI Ops and Agency Ops are siblings opened in full-screen iframes from the Bridge OR direct URLs.

---

## Three URLs

Each dashboard deploys to its own subdomain:

- `https://[slug]-bridge.pages.dev`
- `https://[slug]-ai-ops.pages.dev`
- `https://[slug]-agency-ops.pages.dev`

Optional custom domains.

Optional Cloudflare Access in front of the URLs to restrict to specific email addresses.

---

## Project Folder Structure

```
command-center-template/
├── launch-bridge.html             # The Bridge (main file, can be renamed)
├── ai-ops.html                    # AI Ops dashboard
├── agency-ops.html                # Agency Ops dashboard
├── assets/
│   ├── sun.png                    # Left header sigil (AI Ops launcher), 64x64
│   ├── galaxy.png                 # Right header sigil (Agency Ops), 64x64
│   ├── logo.png                   # Center logo
│   └── fonts/                     # Optional brand fonts
├── deploy-bridge/                 # Cloudflare Pages deploy folder for Bridge
│   ├── index.html                 # Copy of launch-bridge.html
│   ├── assets/                    # Mirror of /assets
│   ├── data/
│   │   ├── state.json
│   │   └── client-briefs.json
│   ├── _headers                   # Cache-Control: no-store for /*.json
│   └── functions/
│       └── api/
│           └── client-notes.js    # Optional KV proxy
├── deploy-ai-ops/
│   ├── index.html
│   ├── data/state.json
│   └── _headers
├── deploy-agency-ops/
│   ├── index.html
│   ├── data/state.json
│   ├── data/client-briefs.json
│   └── _headers
├── auto-deploy.sh                 # Watches HTML files, deploys on save
├── com.bridge.autodeploy.plist    # launchd watcher for auto-deploy
└── README.md
```

---

## Brand Tokens (Customize Per Build)

All three dashboards share the same CSS variable block at the top of each `<style>`. Update once per dashboard at the top.

```css
:root {
  --bg: #02030a;                       /* deep space background */
  --panel: rgba(255, 255, 255, 0.04);  /* panel background */
  --border: rgba(255, 255, 255, 0.10); /* panel border */
  --text-1: #ffffff;                    /* primary text */
  --text-2: #c0c8e0;                    /* secondary text */
  --text-3: #6b7a99;                    /* tertiary text / labels */

  /* Brand accent colors (change per client) */
  --accent-1: #4dd9ff;                  /* cyan */
  --accent-2: #b86bff;                  /* violet */
  --accent-3: #ff6b35;                  /* orange (warm callout) */

  /* Status colors */
  --success: #00ff88;
  --warning: #ffba47;
  --danger:  #ff4d8a;
  --info:    #4dd9ff;

  /* Typography */
  --font-ui:   'Space Grotesk', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
  --font-num:  'Space Grotesk', sans-serif;
}
```

Switch dark/light by swapping `--bg`, `--panel`, `--border`, `--text-*`.

---

## Component 1: THE BRIDGE

The master HTML console. Single file. ~1000-3000 lines depending on panel count. No build step.

### Layout (CSS Grid)

```
grid-template-columns: 360px 1fr 360px;
grid-template-rows: auto 1fr auto;
padding: 10px 24px 110px;
```

Row 1: Header (3 columns wide).
Row 2: AI Ops column left, mission control center, Agency Ops column right.
Row 3: Bottom toolbar (fixed at viewport bottom).

### Header

Left side: clickable sun icon (64x64) that opens AI Ops in full-screen iframe.
Center: BUSINESS NAME + "COMMAND BRIDGE" title.
Right side: clickable galaxy icon (64x64) that opens Agency Ops in full-screen iframe.

```html
<header class="header">
  <a class="sun" onclick="openCommandCenterFullscreen('AI OPS', AI_OPS_URL)">
    <img src="./assets/sun.png" alt="AI Ops" />
  </a>
  <div class="brand brandL">AI OPS</div>
  <div class="hC-title">COMMAND <b>BRIDGE</b></div>
  <div class="brand brandR">AGENCY OPS</div>
  <a class="orb" onclick="openCommandCenterFullscreen('AGENCY OPS', AGENCY_OPS_URL)">
    <img src="./assets/galaxy.png" alt="Agency Ops" />
  </a>
</header>
```

### Left Column: AI Ops Summary Panels

5-8 panels showing summarized AI/system data. Each panel is clickable, opens the holographic workspace overlay with full content.

Standard panels:
1. **AI Overview** - tokens, agents running, skills loaded
2. **Active Agents** - named agents with status
3. **Knowledge Vault** - notes count, links, last sync
4. **Token Usage** - model breakdown
5. **Code Burn** - savings vs API rate

### Center Column: Mission Control

Contains in order top-to-bottom:
1. **Reactor SVG** - circular pulsing element, ~280x280, shows voice status
2. **Reactor status text** - "IDLE / LISTENING / AWAKE / SPEAKING / MUTED / ERROR"
3. **Brain canvas** - optional animated neural visualization, 344x372
4. **Global search input** - bound to Cmd+K, searches vault + clients + panels
5. **Atlas / voice status indicator**

### Right Column: Agency Ops Summary Panels

5-8 panels showing summarized business data. Each clickable, opens holographic workspace.

Standard panels:
1. **Business Overview** - priority pills across categories
2. **Today's Calendar** - upcoming meetings
3. **Communication** - unified inbox counts (email, DMs, missed calls)
4. **Client Tasks** - by priority, urgency badge if any
5. **Pipeline** - sales funnel snapshot
6. **Deliverables** - what's owed, in progress, shipped
7. **Onboarding** - new client tracker
8. **Client Health** - NPS + at-risk list

### Bottom Toolbar

Fixed at bottom. Three sections:

```html
<div class="bot">
  <div class="sysHealth" id="sysHealthLeft">
    <!-- 4 connector status pills: GHL, OBSIDIAN, CLAUDE, GMAIL -->
  </div>
  <div class="bridgeToolbar">
    <button onclick="atlasStop()">STOP</button>
    <button onclick="atlasToggleMic()">MIC</button>
    <button onclick="openSearch()">SEARCH</button>
    <button onclick="openConfig()">CONFIG</button>
    <button onclick="runMorningBriefing()">BRIEF</button>
    <button onclick="openContacts()">CONTACTS</button>
    <button onclick="openNotepad()">NOTES</button>
  </div>
  <div class="sysHealth" id="sysHealthRight">
    <!-- 4 more connector status pills: DRIVE, STRIPE, SLACK, CLOUDFLARE -->
  </div>
</div>
```

### Holographic Workspace Overlay

Fullscreen-ish modal that opens when you click any side panel. Shows the full content of that panel.

```html
<div id="holoWorkspace" class="holoWorkspace">
  <div class="holoHeader">
    <span id="holoTitle">PANEL</span>
    <button onclick="closeHolo()">CLOSE</button>
  </div>
  <div id="holoBody" class="holoBody"></div>
</div>
```

Positioned inset from edges (60px top, 60px left/right, 80px bottom). Cyan border. Closeable by clicking CLOSE, pressing ESC, or clicking outside the overlay.

### Fullscreen Command Center Overlay

When sun or galaxy is clicked, an iframe takes over the screen:

```html
<div id="cmdCenterFullscreen" class="ccFullscreen">
  <div class="ccfHeader">
    <span id="ccfTitle">COMMAND CENTER</span>
    <button onclick="closeCommandCenterFullscreen()">CLOSE</button>
  </div>
  <iframe id="ccfFrame" src="about:blank"></iframe>
</div>
```

### Config Panel

Settings modal. Triggered by gear button or CONFIG toolbar button.

Fields (all stored in localStorage, never hardcoded):
- Anthropic API key
- ElevenLabs API key
- ElevenLabs Voice ID
- OpenAI API key (optional fallback)
- Cloudflare Worker URL (optional)

```javascript
const launchState = {
  anthropicKey: localStorage.getItem('bridge_anthropic_key') || '',
  elevenlabsKey: localStorage.getItem('bridge_elevenlabs_key') || '',
  elevenlabsVoiceId: localStorage.getItem('bridge_elevenlabs_voice') || '',
  openaiKey: localStorage.getItem('bridge_openai_key') || '',
  workerUrl: localStorage.getItem('bridge_worker_url') || '',
};
```

**CRITICAL**: keys live in localStorage only. Never commit them. Never hardcode.

### Voice Assistant Layer

Browser SpeechRecognition + ElevenLabs streaming TTS + Anthropic streaming chat.

**Wake word matching**:
```javascript
const WAKE_PATTERN = /\b(hey|hi|hello|yo|okay|ok|alright)\s+(WAKEWORD|alias1|alias2)\b/i;
```
Require a greeting prefix. Bare wake word triggers too often during normal conversation.

**Echo cooldown**:
After Atlas finishes speaking, ignore wake words for 1800ms minimum (2500ms safer). Without this, the assistant triggers on its own voice and creates an infinite loop.

```javascript
launchState.echoCooldownUntil = Date.now() + 1800;
```

**Hard stop**:
Wired to STOP button, ESC key, SPACE key, and reactor click. All four:
- Cancel current TTS audio
- Cancel any queued sentences
- Set `launchState.muted = true`
- Set `launchState.ttsCancelled = true`
- Abort SpeechRecognition

Reactor click second time re-wakes.

**Streaming TTS**:
Speak each sentence as it arrives from the Anthropic streaming response. Do NOT wait for full response. Lower perceived latency.

```javascript
const match = sentenceBuffer.match(/^(.+?[.!?])\s+/);
if (match) {
  const sentence = match[1];
  sentenceBuffer = sentenceBuffer.slice(match[0].length);
  speakSentence(sentence);
}
```

Each `speakSentence()` MUST check `launchState.ttsCancelled` and `launchState.muted` at entry and return early if either is true.

**Banned phrase filter**:
Strip / silently skip these:
- "my apologies"
- "i apologize"
- "something went wrong"
- "as an ai"
- "as an assistant"

Without this, error catches loop ("My apologies, something went wrong, my apologies...").

**Reactor status states**:
- IDLE
- LISTENING (continuous wake-word detection)
- AWAKE (heard wake word, listening for command)
- THINKING (waiting for Anthropic response)
- SPEAKING (TTS playing)
- MUTED
- ERROR

Updates the `<span id="atlasState">` with a state class.

### Anthropic Streaming Call

```javascript
async function callAnthropic(userMessage) {
  const r = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'x-api-key': launchState.anthropicKey,
      'anthropic-version': '2023-06-01',
    },
    body: JSON.stringify({
      model: 'claude-sonnet-4-6',
      max_tokens: 300,
      system: SYSTEM_PROMPT,
      stream: true,
      messages: [{ role: 'user', content: userMessage }],
    }),
  });
  // Parse SSE stream, speak each sentence as it completes
}
```

### System Prompt Template

```
You are [WAKE_WORD], [BUSINESS_NAME]'s personal AI assistant.
You speak with [VOICE_STYLE].

LIVE BUSINESS STATE:
- Business: [BUSINESS_NAME]
- Industry: [INDUSTRY]
- Top metrics: [LIVE_KPIS]
- Team: [TEAM_LIST]

VOICE RULES:
- Reply in 1-2 short sentences. Hard cap: 30 words.
- Never apologize. Never say "something went wrong" or "as an AI".
- Address the user by [HONORIFIC] at most once per reply.
- Use contractions. Lead with the answer or action.

TOOLS YOU CAN CALL:
- open_panel(section_id)
- open_named_destination(name)
- show_org_chart() / show_financials() / show_marketing()
- create_task(kind, desc, owner, priority)

BANNED PHRASES:
- "my apologies", "something went wrong", "as an ai"
- "in today's fast-paced world", "game-changer", "synergy"
- Em dashes (use periods, commas, parentheses)
```

### Global Search (Cmd+K)

Bind to keyboard:
```javascript
document.addEventListener('keydown', (e) => {
  if ((e.metaKey || e.ctrlKey) && e.key === 'k') {
    e.preventDefault();
    document.getElementById('globalSearch').focus();
  }
});
```

Search across:
- Clients (from `client-briefs.json`)
- Panels (by title)
- Tasks
- Named destinations

Show matches in a dropdown below the input.

### Data Loading

```javascript
async function loadData() {
  const [state, briefs] = await Promise.all([
    fetch('./data/state.json?t=' + Date.now()).then(r => r.json()),
    fetch('./data/client-briefs.json?t=' + Date.now()).then(r => r.json()),
  ]);
  launchState.state = state;
  launchState.briefs = briefs;
  renderAllPanels();
}
setInterval(loadData, 30000);
loadData();
```

30-second auto-refresh. Cache-bust with `?t=Date.now()`.

---

## Component 2: AI OPS DASHBOARD

Standalone HTML dashboard. Read from `data/state.json`. Single file, no backend.

### state.json Schema

```json
{
  "meta": {
    "lastUpdated": "2026-06-10T10:30:00-04:00",
    "lastUpdateType": "morning",
    "source": "manual",
    "notes": "Top headline of the day (shows in What's New panel)"
  },
  "sheets": {
    "System Overview": [
      ["Component", "Status", "Notes"],
      ["Vault", "Live", "Wiki + clients + system"],
      ["Claude Desktop", "Connected", "Cowork mode active"]
    ],
    "Plugins": [
      ["Plugin", "Version", "Date Installed", "Notes"]
    ],
    "Skills Inventory": [
      ["Skill", "Category", "Status"]
    ],
    "Connectors Active": [
      ["Connector", "Account", "Permissions", "Date Connected"]
    ],
    "Agents": [
      ["Name", "Role", "Status"]
    ],
    "Build Roadmap": [
      ["Item", "Priority", "Owner", "ETA"]
    ],
    "Quick Stats": [
      ["Metric", "Value"]
    ]
  },
  "codeburn": {
    "plan": { "name": "Claude Max", "monthlyCost": 200 },
    "today": { "apiCost": 14.76, "calls": 85, "sessions": 9 },
    "sevenDays": { "apiCost": 819.78, "calls": 4774 },
    "thirtyDays": {
      "apiCost": 2105.97,
      "calls": 16556,
      "savings": 1905.97,
      "multiplier": 10.5
    }
  },
  "scheduledTasks": [
    {
      "taskId": "morning-briefing",
      "description": "Run morning briefing",
      "schedule": "0 7 * * *",
      "nextRunAt": "2026-06-11T07:00:00-04:00",
      "enabled": true
    }
  ]
}
```

### Required Panels

1. **Header** - business name, live clock (HH:MM:SS), last-updated stamp.
2. **What's New** - reads `meta.notes`, auto-bullets by `. ` or newline.
3. **KPI strip** - reads `sheets["Quick Stats"]` as label/value cards.
4. **CodeBurn strip** - reads `codeburn.*`, shows plan / today cost / 30d equivalent / savings + multiplier. Mint→cyan gradient.
5. **Sheet panels** - auto-rendered from `sheets` object. Each sheet becomes a `.panel` with table header + rows.
6. **Scheduled Tasks** - reads `scheduledTasks[]`.

### Auto-rendering Logic

```javascript
function renderSheets(sheets) {
  for (const [name, rows] of Object.entries(sheets || {})) {
    const headers = rows[0];
    const data = rows.slice(1);
    // build .panel with <h2>{name}</h2> and <table>
  }
}
```

This means new sheet keys in state.json automatically appear as new panels. No code changes required.

### Critical Behaviors

- 30-second `setInterval(load, 30000)` auto-refresh.
- Cache-bust on every fetch with `?t=Date.now()`.
- Graceful empty states ("No data yet" instead of crash).
- JSON validation failures show "Failed to load state.json" not a blank page.

---

## Component 3: AGENCY OPS DASHBOARD

Standalone HTML dashboard. Reads `data/state.json` + `data/client-briefs.json`.

### state.json Schema

```json
{
  "meta": { /* same shape as AI Ops */ },
  "company": {
    "Official Company Name": "...",
    "DBA": "...",
    "Address": "...",
    "Phone": "...",
    "Email": "...",
    "Website": "..."
  },
  "clients": [
    {
      "name": "Jane Doe",
      "business": "Jane's Business",
      "niche": "...",
      "status": "Active",
      "startDate": "2026-05-01",
      "mrr": 497,
      "completionPct": 65,
      "email": "...",
      "mobilePhone": "...",
      "website": "...",
      "subAccountUrl": "...",
      "driveFolderUrl": "...",
      "obsidianPath": "Wiki/clients/jane-doe/",
      "stages": [
        {
          "label": "Foundation",
          "items": [
            { "label": "Phone purchased", "status": "YES", "note": "" },
            { "label": "A2P approved", "status": "BLOCKED", "note": "Awaiting EIN" }
          ]
        }
      ],
      "ghlLocationId": "...",
      "linkedinUrl": "...",
      "instagramUrl": "...",
      "facebookUrl": "...",
      "youtubeUrl": ""
    }
  ],
  "clientTasks": [
    {
      "client": "Jane Doe",
      "desc": "Build contact form",
      "who": "Builder",
      "priority": "Urgent",
      "link": "",
      "notes": "Blocked on logo files",
      "status": "Open"
    }
  ],
  "agencyTasks": [
    {
      "desc": "Update pricing page",
      "who": "Founder",
      "priority": "High",
      "link": "",
      "notes": "",
      "onHold": false
    }
  ],
  "addOns": [
    {
      "Optional Add-On": "Funnel Build",
      "Price": "$997",
      "What you get": "...",
      "Great for": "...",
      "Category": "Funnels",
      "_note": "Optional tooltip note"
    }
  ],
  "plans": [
    {
      "title": "Essentials",
      "tier": 1,
      "audience": "...",
      "price": "$297/mo",
      "tagline": "...",
      "summary": "...",
      "features": ["...", "..."]
    }
  ],
  "coreFeatures": [
    {
      "Module / Feature": "...",
      "What it does": "...",
      "Sales one-liner": "...",
      "Tier": "Essentials+"
    }
  ],
  "a2p": [
    { "step": "EIN required", "detail": "..." }
  ],
  "calendar": {
    "upcoming": [
      {
        "title": "Strategy with Jane Doe",
        "datetime": "2026-06-12T14:00:00-04:00",
        "attendees": ["Founder", "Jane Doe"]
      }
    ]
  },
  "ghl": {
    "fetchedAt": "...",
    "locationId": "...",
    "pipelines": [
      {
        "id": "...",
        "name": "Sales Pipeline",
        "stages": ["New Lead", "Discovery", "Proposal", "Closed Won"],
        "opportunityCount": 23,
        "opportunitiesByStage": {
          "New Lead": 8,
          "Discovery": 5,
          "Proposal": 4,
          "Closed Won": 2
        }
      }
    ],
    "opportunities": []
  },
  "companyNotes": {
    "DBA": "Tooltip note for the DBA cell",
    "Phone": "Forwards to founder cell after hours"
  }
}
```

Priority values: `Urgent`, `High`, `Normal`, `Low`, `Done`.
Status values for clients: `Active`, `Paused`, `Prospect`, `Inactive`, `Dead`.
Stage item status values: `YES`, `NO`, `BLOCKED`, `NA`.

### client-briefs.json Schema

```json
{
  "fetchedAt": "...",
  "vaultRoot": "/path/to/Wiki/clients",
  "clients": {
    "Jane Doe": {
      "slug": "jane-doe",
      "snapshot": {
        "business": "...",
        "plan_amount": "$497/mo",
        "status": "Active",
        "email": "...",
        "phone": "..."
      },
      "summary": {
        "highlights": ["First call great", "Onboarding week 2"]
      },
      "files": {
        "profile": {
          "title": "Jane Doe",
          "content": "<full profile.md body>",
          "lines": 87
        },
        "conversations": {
          "title": "Conversations",
          "content": "<full conversations.md body>"
        },
        "tasks": {
          "title": "Tasks",
          "content": "<full tasks.md body>"
        }
      },
      "meetings": [
        { "date": "2026-06-05", "title": "Strategy call", "content": "..." }
      ],
      "lastUpdated": "2026-06-08",
      "mergedFrom": ["jane-doe"]
    }
  }
}
```

### Required Panels

1. **Header** - business name, clock, last-updated.
2. **What's New** - meta.notes auto-bulleted.
3. **KPI strip** - total clients, active count, MRR sum, avg completion%, urgent task count, payments due today.
4. **Today panel** - 3 columns:
   - Today's meetings (filtered from `calendar.upcoming`)
   - Urgent tasks (clientTasks + agencyTasks where priority === "Urgent")
   - Payments due today (clients where today's day-of-month matches pay day)
5. **Clients table** - sortable, filterable, status badges, links to CRM and to vault folder. Click name → opens Focus modal.
6. **Per-client Focus modal** (see below).
7. **Sales pipeline panel** - reads `ghl.pipelines`, horizontal funnel with stages and counts. Click stage → see opportunities.
8. **Client tasks panel** - sorted by priority, grouped by client.
9. **Agency tasks panel** - sorted by priority.
10. **Plans section** - cards from `plans[]`.
11. **Add-ons section** - cards from `addOns[]`.
12. **Onboarding section** - per-client stages collapsible.

### Focus Modal

The highest-value component. Clicking a client opens a full-screen overlay.

Layout:
- Left column: profile snapshot (status, plan, MRR, contact, social links).
- Center column: tabs.
- Right column: quick actions (open CRM, open vault, leave note, add task).

Tabs:
- **Profile** - renders `brief.files.profile.content` as markdown.
- **Tasks** - filters `state.clientTasks` to this client, grouped by priority.
- **Conversations** - reads from KV `/client-notes?client=<name>` if Worker is set up, else `brief.files.conversations.content`.
- **Setup** - renders `client.stages[]` with YES/NO/BLOCKED status badges and tooltip notes.
- **Events Log** - reads from KV `/client-notes?client=<name>&kind=event`, sorted by ts.
- **Deliverables** - filters `state.clientTasks` to kind="Deliverable" for this client.

### Pipeline Visualization

Horizontal funnel. Each stage as a colored card. Counts as big numbers. Click stage to filter opportunities below.

If `ghl.pipelines` is empty or null, show "CRM not connected yet."

### Required Behaviors

- 30-second auto-refresh of state.json AND client-briefs.json.
- Cache-bust with `?t=Date.now()`.
- Focus modal opens via click, closes via X / ESC / clicking outside.
- Sort and filter clients table by status, priority, completion%.
- Pay day calculation: `today = new Date().getDate(); client.payDay === today`.

---

## Critical Behaviors Across All Three

### Cache-Busting

Add this to each deploy folder root:

`_headers`:
```
/*.json
  Cache-Control: no-store

/data/*
  Cache-Control: no-store
```

Without this, Cloudflare's CDN caches JSON forever and changes never show up.

### Cache-Busting in Fetch

Always:
```javascript
fetch('./data/state.json?t=' + Date.now())
```

The `?t=` cache-bust complements the `_headers` rule. Both required.

### Deploy Command (CRITICAL FLAG)

```bash
wrangler pages deploy . \
  --project-name=[slug]-[component] \
  --branch=main \
  --commit-dirty=true
```

The `--branch=main` flag is REQUIRED. Without it, you deploy to a preview URL with a random hash and the production URL never updates. This is the single most common failure mode.

### No Hardcoded API Keys

Never. Ever. localStorage only, set via config panel. The HTML must be safe to commit to a public repo.

### Voice Layer Lessons (Non-Negotiable)

1. **Echo cooldown 1800ms minimum** after every TTS finish, ignore wake words.
2. **Require greeting prefix** in wake word matcher. Bare wake fires too often.
3. **Banned phrase filter** silently drops apology and AI-disclosure phrases.
4. **Hard stop on STOP/ESC/SPACE/reactor click** must cancel TTS audio AND clear sentence queue AND abort recognition.
5. **TTS streaming kill switch** at entry of EVERY speak function: check `launchState.ttsCancelled` and `launchState.muted`.
6. **Mic permission gesture**: reactor click is the user gesture Chrome requires before TTS can play. Never try to start TTS before any click.

### Frontmatter Rule for Vault Files

YAML frontmatter MUST start at line 1 of every markdown file that has it. If any preamble exists above the `---`, downstream parsers silently return empty frontmatter, causing the dashboard to show blank fields.

If client-briefs.json shows empty snapshots, check `profile.md` for that client. The first 3 characters of the file must be `---`.

### Single-Folder Per Client

Use the slug of the PERSON'S NAME, not their business name. `Wiki/clients/jane-doe/`, never `Wiki/clients/janes-business/`.

If you ever discover a client at two folders, merge into the name-slug folder. The rebuild script `sync_client_briefs.py` includes a dual-folder merge fallback, but the right answer is never create two in the first place.

---

## Build Order

1. Build `ai-ops.html` first. Simplest schema, fastest to validate.
2. Build `agency-ops.html` second. Bigger schema, more panels. Test Focus modal carefully.
3. Build `launch-bridge.html` last. Most complex. Stub voice initially. Wire voice last.
4. Deploy each to Cloudflare Pages with `--branch=main`.
5. Set up `_headers` for cache-busting on each.
6. Wire `auto-deploy.sh` + launchd watcher so edits auto-deploy on save.
7. Add voice layer to Bridge.
8. Optional: add Cloudflare Access for privacy.

---

## Tech Stack Summary

- **Frontend**: Vanilla HTML/CSS/JS. No framework. No build step.
- **State**: JSON files in `data/` folder.
- **Hosting**: Cloudflare Pages.
- **Optional Worker**: Cloudflare Worker with KV namespace for `/client-notes` endpoint.
- **Optional Functions**: Cloudflare Pages Functions for API proxies.
- **Auto-deploy**: launchd watcher + wrangler CLI.
- **Voice**: Browser SpeechRecognition + ElevenLabs Streaming TTS + Anthropic Streaming Chat.
- **Optional voice capture daemon**: Python + mlx-whisper (local transcription, no API costs).

---

## What You Need From the Client

Before starting:

1. Business name + tagline.
2. Brand colors (primary, secondary, accent).
3. Logo (PNG or SVG).
4. Wake word (2-3 syllables, distinct).
5. ElevenLabs voice ID (they pick from Voice Library).
6. List of their top KPIs.
7. List of their connected tools (CRM, calendar, etc.).
8. List of their top 5-10 clients (to seed state.json).
9. Plan tiers and pricing if applicable.
10. Cloudflare account access (or API token with Pages + Workers + KV permissions).

---

## What This System Does Not Do

- Does not store data on your server. Everything lives on the client's Cloudflare account.
- Does not handle authentication beyond Cloudflare Access (which you set up if they want privacy).
- Does not write to the vault from the browser (Cloudflare Pages is static). The vault is updated by Claude Desktop on the client's Mac, and a sync script pushes vault → JSON → Cloudflare on a 15-minute schedule.
- Does not work without modern browser SpeechRecognition (Chrome and Safari work, Firefox is spotty).
- Does not replace a CRM. It surfaces CRM data through panels but does not store opportunities.

---

## Estimated Build Time

| Component | First build | Replica |
|---|---|---|
| AI Ops | 4-6 hrs | 1-2 hrs |
| Agency Ops | 6-10 hrs | 2-3 hrs |
| Bridge skeleton | 6-10 hrs | 2-3 hrs |
| Voice layer | 8-15 hrs | 3-5 hrs |
| Deploy + auto-deploy | 2-4 hrs | 30 min |
| Auto-flow scripts | 6-10 hrs | 2-3 hrs |
| **Total** | **30-55 hrs** | **10-15 hrs** |

First build is investment in your template. Every replica after gets 70-80% reuse.

---

Done. Build clean, ship fast, test the voice layer obsessively.
