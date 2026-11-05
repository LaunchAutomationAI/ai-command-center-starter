# Plugins, Skills, and Connectors

The complete list of what to install in your Claude Desktop.

---

## Where To Install

Open Claude Desktop. Look for one of:
- A puzzle-piece icon in the left sidebar
- Settings (gear icon) > Plugins
- Settings > Capabilities > Skills

Click. You see the plugin marketplace.

---

## Foundation Plugins (Everyone Installs These)

These four are document handling. Every user needs them.

- **docx** - create, read, edit Word documents
- **xlsx** - create, read, edit Excel spreadsheets
- **pptx** - create, read, edit PowerPoint presentations
- **pdf** - read, merge, split, extract from PDFs

Then a productivity layer:

- **productivity** - task management and the two-tier memory system (TASKS.md and persistent memory across sessions)
- **schedule** - create scheduled tasks that run automatically (daily briefings, recurring reports)
- **skill-creator** - the tool you use to build YOUR OWN custom skills later
- **consolidate-memory** - monthly cleanup of Claude's memory files
- **setup-cowork** - guided helper for adding new mounted folders later
- **mcp-builder** - guide for integrating any niche API into Claude later

And research and content tools:

- **watch** - watch a video, extract transcript and frames, answer questions about it
- **web-asset-generator** - favicons, app icons, Open Graph images for your website
- **viral-video-production** - motion graphics, kinetic typography, social reels
- **deep-research** - multi-source web research with citation verification

Install every one of these in your first Claude session.

---

## Domain Plugins (Install What Matches Your Business)

### Operations Plugin
Install if you run a structured business, have processes, document SOPs, or manage vendors.

Skills included: `status-report`, `process-doc`, `runbook`, `vendor-review`, `capacity-plan`, `risk-assessment`, `compliance-tracking`, `change-request`, `process-optimization`.

What you use it for: weekly status reports, documenting SOPs, runbooks for recurring tasks, vendor evaluations, risk registers.

### Marketing Plugin
Install if you market your business (you probably do).

Skills: `campaign-plan`, `content-creation`, `draft-content`, `email-sequence`, `brand-review`, `competitive-brief`, `performance-report`, `seo-audit`.

What you use it for: drafting blogs and emails, planning campaigns, reviewing content for brand voice consistency, building email drip sequences.

### Brand Voice Plugin
Install if you produce content at any scale (sales emails, blog posts, social, sales decks).

Skills: `discover-brand`, `generate-guidelines`, `enforce-voice`, `brand-voice-enforcement`.

What you use it for: auditing your existing brand materials, generating a style guide from sales calls or documents, enforcing voice on every new piece of content.

### SearchFit SEO Plugin
Install if you have a website you want found in search or AI tools.

Skills: `seo-audit`, `technical-seo`, `on-page-seo`, `content-strategy`, `content-brief`, `ai-visibility` (AEO for ChatGPT, Claude, Perplexity, Gemini), `schema-markup`, `keyword-clustering`, `internal-linking`, `broken-links`, `content-translation`, `create-content`, `create-topic`, `generate-schema`, `seo-check`.

What you use it for: full SEO and AEO audits, content briefs, schema markup, keyword clustering, AI visibility tracking.

### Enterprise Search Plugin
Install AFTER your connectors are set up.

Skills: `search`, `digest`, `knowledge-synthesis`, `search-strategy`, `source-management`.

What you use it for: searching across ALL your connected sources (Gmail, Drive, Slack, etc.) at once, daily digests of activity across sources.

### ZoomInfo Plugin
Install ONLY if you have a ZoomInfo subscription.

Skills: `account-research`, `build-list`, `buying-committee`, `competitor-analysis`, `enrich-company`, `enrich-contact`, `find-similar`, `meeting-prep`, `recommend-contacts`.

What you use it for: account intelligence, prospect lists, meeting prep, competitor research.

### Sanity Plugin
Install ONLY if you use Sanity CMS.

Skills: `sanity-best-practices`, `content-modeling-best-practices`, `portable-text-conversion`, `portable-text-serialization`, `deploy-schema`, `typegen`, `review`, `seo-aeo-best-practices`.

---

## Connectors (MCPs) - Different From Skills

Skills extend what Claude can DO. Connectors extend what Claude can ACCESS.

Skills install through the Plugins menu. Connectors install through Settings > Connectors.

Connectors require OAuth (sign-in with your account) for most services.

### Install in this order

**Phase 1: Foundation (everyone)**
- Gmail
- Google Calendar
- Google Drive

**Phase 2: Meetings (if you record meetings)**
- Fathom OR Granola (whichever you use)

**Phase 3: Your stack (varies)**
- Your CRM (GoHighLevel, HubSpot, Salesforce, Pipedrive, Close, etc.)
- Slack (if you use it)
- Project management (Asana, Linear, Monday, ClickUp, Notion)
- Docs and wiki (Notion, Confluence)
- Design (Canva, Figma)
- Payments (Stripe, QuickBooks)
- Web scraping (Apify, if you scrape)
- Browser (Claude in Chrome, for web automation)

**Phase 4: Premium (if you have them)**
- ZoomInfo (if you have an active subscription)
- Cloudflare (if you build dashboards in later phases)

### Install one at a time

Each connector has its own OAuth flow. Things can go wrong. If you install 10 at once and a morning briefing breaks, you can't tell which connector failed.

Install one. Test with a real query. Log it in TOOLS.md. Move to the next.

---

## Anthropic Foundation Skills

These ship from Anthropic and extend core Claude capability. Install all of them.

Source: https://github.com/anthropics/skills

- `consolidate-memory` - monthly memory cleanup
- `schedule` - create scheduled tasks
- `skill-creator` - build custom skills
- `setup-cowork` - guided setup helper
- `mcp-builder` - guide for building custom MCP servers
- `viral-video-production` - high-impact video content
- `web-asset-generator` - web asset generation
- `watch` - video transcription and analysis
- `deep-research` - cited research reports

---

## Custom Skills (Built Later, Specific to You)

Once you've used the system for 30+ days, your coach will help you build custom skills for the workflows you repeat. Examples:

- Your Monday morning briefing in your house format
- New client intake automation
- Client meeting prep (one-shot brief before any call)
- Weekly status report to a team or partner
- Daily journal / decision log
- Specific compliance check (A2P, GDPR, HIPAA, etc.)
- Recurring industry research (e.g., for an insurance agent, daily T65 carrier updates)

These aren't installed from the marketplace. Your coach helps you build them using the `skill-creator` skill. They live in your vault under `Templates/skills/` and are unique to you.

---

## Final Checklist

After your first few sessions, your TOOLS.md should look something like this:

```
## Plugins

- docx, xlsx, pptx, pdf - document handling
- productivity, schedule, skill-creator, consolidate-memory, setup-cowork
- mcp-builder, watch, web-asset-generator, viral-video-production, deep-research
- operations (if applicable)
- marketing (if applicable)
- brand-voice (if applicable)
- searchfit-seo (if applicable)
- enterprise-search (after connectors)

## Connectors

- Gmail - <your work email> - connected YYYY-MM-DD
- Google Calendar - connected YYYY-MM-DD
- Google Drive - connected YYYY-MM-DD
- Fathom - connected YYYY-MM-DD
- <Your CRM> - connected YYYY-MM-DD
- Slack - connected YYYY-MM-DD
- ...

## Custom Skills

- (added later, after your first month)
```

Keep this list current. Your future Claude reads it to know what's available.
