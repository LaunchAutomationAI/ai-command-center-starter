# Getting Started

Your vault is installed, Claude is connected, and you have skills loaded. Now what?

This is your day-one guide. Read it once. Try the things on it. Watch your coach's recording if you forget.

---

## Your First Conversation With Claude

Open Claude Desktop. Start a new chat. Type:

```
Read CLAUDE.md and tell me what you know about my business.
```

Claude reads your operating instructions (which include your customized Business Context section) and gives you a summary. If anything sounds wrong, tell your coach in the next session and we'll tune it.

---

## The Three Commands You'll Use Most

### 1. Compile Raw

You drop files into the `Raw/` folder. Articles, screenshots, transcripts, voice memos, PDFs. Whenever you want them organized into your Wiki:

```
Compile Raw.
```

Claude reads each file, decides where it belongs in your Wiki structure, writes a wiki article, updates the indexes, and moves the original to `Raw/_archive/`.

### 2. Show me [client/topic]

```
Show me [client name].
```

Claude pulls everything you have on that client (profile, conversations, tasks, recent activity) and gives you a tight summary. Useful before calls.

Same pattern for topics:

```
What do I have on [topic]?
```

### 3. Morning briefing

```
Give me a morning briefing.
```

Once your connectors are set up (Gmail, Calendar, Drive, etc.), Claude pulls from your actual email, calendar, and Drive to give you an executive summary of your day.

---

## Daily Patterns Worth Building

These aren't required. They're patterns that compound. Pick the ones that fit your style.

### Morning (5 minutes)

```
Give me a morning briefing. What is on my plate today?
```

### After every meeting (2 minutes)

```
I just finished a call with [name]. Here's what we covered:
- [bullet]
- [bullet]
- [bullet]

Update their profile.md and append a conversation entry.
```

### End of day (5 minutes)

```
What did I commit to today? Pull from our chats and any meetings.
```

### Friday afternoon (10 minutes)

```
Run through my open client tasks. What is overdue? What is blocked? What needs a check-in?
```

### Monday morning (10 minutes)

```
Run my Monday morning briefing.
```

Once you've done this a few times, your coach can build a custom skill that automates it.

---

## How To Add a New Client

```
I have a new client: [name]. They run [business]. Their email is [email]. They're paying $[X] per month for [what you're doing for them]. Set up their folder.
```

Claude uses the templates in `Templates/` to create:

- `Wiki/clients/[their-slug]/profile.md`
- `Wiki/clients/[their-slug]/conversations.md`
- `Wiki/clients/[their-slug]/tasks.md`
- `Wiki/clients/[their-slug]/daily-log.md`

Then updates `Wiki/clients/_index.md` to list them.

---

## How To Log a Meeting

```
I had a meeting today with [name] about [topic]. Here's what happened: [tell Claude the story]. Save it.
```

Claude creates a meeting note in the right client's `meetings/` folder using the template, and appends a summary to their `conversations.md`.

---

## How To Capture Decisions

```
Decision: [what you decided]. Reason: [why]. Add to System/CONTEXT.md.
```

Claude logs it. Future you (and future Claude) can read it back when relevant.

---

## What Lives Where

Quick mental map:

- **Need to find a person:** `Wiki/clients/<their-name>/`
- **Need to recall a decision:** `System/CONTEXT.md`
- **Need to remember a process:** `Wiki/operations/`
- **Need a sales script or hook:** `Wiki/sales-and-demos/` or `Wiki/marketing/`
- **Need a product detail:** `Wiki/products/`
- **Need to drop a file fast:** `Raw/`
- **Need Claude to make you something:** outputs land in `Output/`

You shouldn't have to navigate manually. Just ask Claude.

---

## When You Get Stuck

**Claude doesn't seem to know about something it should know:**

Ask "what files have you read in this conversation?" and see if it's looking in the wrong place. Tell it to check `Wiki/_master-index.md` first.

**Claude is making up facts:**

Tell it "stop. Read the relevant vault file first and answer from there." This is rare once CLAUDE.md is dialed in but happens occasionally.

**A client folder won't update:**

Open the file in Obsidian. Check that the YAML frontmatter at the top starts on LINE 1. If anything is above the `---`, move the frontmatter to line 1.

**Anything else:**

Text or email your coach. Most fixes are 5 minutes. If it's a real problem, we book a quick session.

---

## What Not To Do

- **Don't move folders around manually.** If you need a different structure, ask Claude to reorganize.
- **Don't edit the `_index.md` files by hand.** Claude maintains them.
- **Don't put two folders for the same client.** Always use the person's name as the slug.
- **Don't dump 500 files into Raw at once.** It still works, but compile in batches of 20-50 for sanity.
- **Don't paste API keys or passwords into Claude chat.** They live in your tool configs, not in chat history.

---

## Next Steps

Once you've used the daily patterns for a week:

- Tell your coach what feels broken or missing. We tune.
- Tell your coach what workflows you repeat. We build custom skills for them.
- Tell your coach what you want next: connectors, dashboards, voice assistant, more skills.

There's no rush. The system gets better the more you use it.

Welcome.
