# START HERE

Welcome to your new AI command center foundation.

This folder is the complete starter kit for your Obsidian vault and Claude setup. Everything here is ready to drop into place. Your coach (the person installing this with you) will walk through it live in your first session.

---

## What This Folder Is

This is a drag-and-drop starter pack for your personal AI second brain. Inside:

- **CLAUDE.md** - The operating instructions Claude will read every time you talk to it. We customize this with your business in your first session.
- **System/** - Files that hold your rules, tools inventory, identity, and email routing.
- **Wiki/** - Where all your structured knowledge will live. Clients, operations, marketing, products, anything you want your second brain to remember.
- **Templates/** - Pre-built note templates for new clients, conversations, tasks, meetings.
- **Raw/** - Your inbox. Drop anything here. Articles, screenshots, transcripts. You ask Claude to compile it into the Wiki later.
- **Output/** - Where Claude saves files it generates for you (reports, drafts, exports).
- **Captures/** - Voice transcripts if you ever add the ambient voice capture feature.
- **Daily Briefings/** - Auto-generated daily summaries (added later).

---

## How To Install (For Your Coach)

After Obsidian is installed and an empty vault exists at `/Users/<your-username>/Documents/Vault/`:

1. Open Finder.
2. Select EVERYTHING inside this "Install for client" folder.
3. Drag the contents into your new Vault folder.
4. Obsidian picks it up automatically.

After that, the vault is structured and Claude has its operating instructions. Your coach customizes the bracketed sections (your business context, your name, your brand, your style preferences) during the live session.

---

## How To Use It (For You, The Owner)

After your coach installs this:

### Day 1
- Open Obsidian. The Vault folder shows the structure.
- Click around. See where things live.
- Open `Getting-Started.md` and read it. 5 minutes.

### Every Day After
- Drop interesting files into `Raw/` as they cross your desk.
- Tell Claude "compile Raw" when you want them filed into Wiki.
- Ask Claude for a morning briefing.
- Let Claude write to your Wiki as you have conversations.

### Recurring Patterns
- New client? Ask Claude to "create a new client folder for [name]". It uses the templates.
- New meeting? Ask Claude to "create a meeting note for my call with [name] today". Same.
- Need a quick summary of where you stand with someone? "What is my history with [client]?"

---

## What Goes In Each Folder

### Raw/
Anything unprocessed. Screenshots, PDFs, transcripts, voice memos, articles you save, emails you forward. Don't organize. Just dump.

### Wiki/
The structured second brain. Topics, organized. Claude maintains this. You read from it, point Claude at it, refer to it.

### Wiki/clients/
One folder per client. The living CRM. Each client has a profile, conversations log, task list, daily log.

### System/
Rules and state-of-the-world. Files Claude reads to orient itself. CLAUDE.md (operating instructions, at the vault root) plus CONTEXT.md (recent decisions), TOOLS.md (what's installed), USER.md (who you are), IDENTITY.md (your brand).

### Templates/
Note templates. Don't edit these unless you want to change the template structure. New notes are CREATED from these.

### Output/
Where Claude saves deliverables: reports, PDFs, exports, drafts.

### Captures/
Voice transcripts (optional, added if you add voice capture later).

### Daily Briefings/
Auto-summarized daily briefings of your voice captures (optional).

---

## Important Rules

### Frontmatter at line 1

Any file with YAML frontmatter (the `---` block at the top) MUST start at line 1. If you put any text above the `---`, Claude will read the file as having no frontmatter and important fields like your plan, status, or business name will silently disappear from any dashboards we build later.

If you ever see Claude getting confused about a client's data, check `profile.md` for that client and make sure the very first character of the file is `-`.

### One client folder per person

Don't create two folders for the same client. If Jane Doe runs Jane's Business, use `Wiki/clients/jane-doe/`, not `Wiki/clients/janes-business/`. The slug comes from the PERSON'S NAME, not their business. This prevents downstream tools from getting confused.

### Don't manually edit `_master-index.md` or `_index.md` files

Claude maintains those automatically. If you edit them by hand, your changes may get overwritten next time Claude updates the indexes.

---

## What's Next

After install:

1. Spend a week using the system every day.
2. Drop files into Raw, ask Claude to compile them.
3. Talk to Claude. Ask for briefings. Use the templates.
4. Note what feels broken or missing. Tell your coach in the next session.
5. Book your next session when you're ready to add more.

There's no rush. Each session adds capability. You only pay for what you book.

Welcome aboard.
