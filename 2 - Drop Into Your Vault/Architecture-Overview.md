# Architecture Overview

What this system actually is, in plain language.

---

## The Three-Layer Mental Model

Your AI command center is three layers stacked together. Understanding which layer does what makes everything else click.

### Layer 1: The Vault

Your Obsidian vault. A folder on your Mac at `/Users/<your-username>/Documents/Vault/`.

Inside it, every meeting, client, decision, SOP, idea, and asset lives as a plain markdown file. No database. No SaaS. Just folders and `.md` files.

Why a folder of markdown files?

- It runs on your computer. No login. No subscription to lose.
- You own it. If anything happens to your AI tools, the vault is still there.
- It works without any AI. You can open Obsidian and read your notes manually.
- It's searchable, linkable, and portable.

The vault is the SOURCE OF TRUTH. Everything else is just a view of the vault.

### Layer 2: The Brain (Claude)

Claude Desktop running in Cowork mode with your vault mounted.

Cowork is the feature that lets Claude read and write files in folders you explicitly mount. When you mount your Vault folder, Claude can:

- Read CLAUDE.md and follow its instructions.
- Read any file in your Wiki and reference it.
- Create new files when you ask.
- Update existing files when something changes.
- Search across the vault for context.

Claude is THE INTERFACE. You talk to Claude. Claude reads the vault. Claude writes to the vault. Claude answers questions using vault content.

Skills extend Claude's capabilities (create Word docs, generate spreadsheets, run marketing analyses, etc.).

Connectors extend Claude's reach (read your Gmail, your calendar, your Drive, your CRM).

### Layer 3: The Cockpit (Optional)

This layer is optional. Many users stop after Layer 2 and get plenty of value.

If you want the full Iron Man feel, Layer 3 is dashboards (HTML files that read your vault data and display it visually) plus a voice assistant ("Hey [wake word], give me the morning briefing").

Dashboards are pages you open in a browser. They show your KPIs, your clients, your tasks, your pipeline, your AI inventory. They auto-refresh from the vault.

The voice assistant uses a wake word, responds in a voice you choose, and drives the dashboards by command.

You only build this layer if it helps you. Some people prefer the vault + Claude alone. That's fine.

---

## How Data Flows

```
EXTERNAL TOOLS              VAULT                       BRAIN (CLAUDE)         COCKPIT (OPTIONAL)
---------------             -----                       --------------         ------------------

Gmail messages              Wiki/clients/<slug>/        Reads CLAUDE.md +      Dashboard panels
Calendar events             conversations.md            vault topics           read JSON files
Drive documents      ---->  Wiki/operations/SOPs   <--- Writes new articles    that summarize
Fathom transcripts          System/CONTEXT.md           when info comes in     vault content
CRM contacts                Templates/                  Answers queries
Voice captures              Captures/<date>.md          using vault as truth
```

The vault is the hub. Everything reads from it. Everything writes to it.

---

## What Makes This Different From a SaaS

- **It runs on your computer.** Not in someone else's cloud. Your data, your files, your control.
- **You own the code.** If you ever stop working with your coach, the system keeps running.
- **No login to lose.** Vault is a folder. Claude is desktop software. Dashboards are HTML files you can open in any browser.
- **No vendor lock-in.** Everything is plain markdown, plain JSON, plain HTML. Portable forever.
- **Your data trains your brain, not someone else's.** What you put into the vault makes YOUR Claude smarter, not OpenAI's training set.

---

## What You're Building, Phase By Phase

You will not build all of this in one session. Some clients stop after Phase 4. Some build all the way through Phase 10. Your custom session plan tells you what's right for you.

### Phase 1: Vault Foundation
Obsidian, folder structure, CLAUDE.md, system files, templates. The foundation everything else sits on.

### Phase 2: Brain Connected
Claude Desktop installed, Cowork enabled, vault mounted, document skills installed (Word, Excel, PowerPoint, PDF), domain skills installed (matching your business).

### Phase 3: Senses Connected
Gmail, Calendar, Drive, Fathom (or meeting tool), your CRM, Slack, project management, payments. Whatever you use daily.

### Phase 4: Custom Workflows
1-3 custom skills built for your recurring tasks. Monday briefings, new client intake, weekly status reports, whatever you repeat.

After Phase 4, many users have everything they need. The vault, Claude, connectors, and custom workflows. Months of value.

### Phase 5-7: Visual Dashboards (Optional)
AI Ops dashboard, Agency Ops dashboard, the Bridge (master HTML console with voice control). Iron Man feel.

### Phase 8-9: Auto-Flow Pipelines (Optional)
Background scripts that pull Gmail threads into client conversations automatically. Auto-deploy when files change. 15-minute sync cycles.

### Phase 10: Voice Assistant (Optional)
Wake word, voice response in a voice you pick, all-day ambient capture that transcribes you for tomorrow's briefing.

---

## What This System Replaces

- **Multiple SaaS subscriptions.** Notion + Reflect + Coda + a CRM + a project management tool. One vault.
- **Generic AI tools.** ChatGPT in a tab knows nothing about your business. This Claude knows your clients by name.
- **Hunting for information.** Where did I save that doc? When did we agree to that price? Just ask Claude.
- **Manual data entry.** Drop files in Raw. Compile. Claude organizes.
- **Forgetting decisions.** CONTEXT.md remembers what you decided and why.
- **Inconsistent client management.** Every client gets the same structure, the same updates, the same care.

---

## What This System Does NOT Replace

- **Your judgment.** Claude surfaces information. You still decide.
- **Your relationships.** Claude makes follow-up easier. It doesn't replace the actual call.
- **Your taste.** Templates give consistency. Your voice and decisions stay yours.
- **Your work ethic.** AI gives leverage. Leverage works on what you put in.

---

## The Honest Truth

This works because you use it daily. Skip a week and it becomes a folder of empty templates. Use it daily and it becomes the most valuable thing on your computer.

The first 30 days are tuning. By week 4 you'll feel the difference. By month 3 you'll forget how you worked without it.

Welcome aboard.
