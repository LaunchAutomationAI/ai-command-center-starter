# Clients

One folder per client. The living CRM. Each client folder contains:

- `profile.md` - frontmatter (plan, status, contact) plus body (Snapshot, Profile, Voice, Key Takeaways)
- `conversations.md` - dated log of every interaction (calls, emails, meetings, captures)
- `tasks.md` - open and completed tasks for this client
- `daily-log.md` - one-line entries every time something ships for the client
- `meetings/` - per-meeting notes, one file per meeting

## Active Clients

(empty, will fill in as you add clients)

## Inactive / Past Clients

(empty)

## New Prospects

(empty)

## Rules for Adding a New Client

1. Use the slug of the PERSON'S NAME (kebab-case). NOT the business name.
   - Example: Jane Doe of Jane's Business -> `Wiki/clients/jane-doe/`
2. Copy the templates from `Templates/` into the new folder.
3. Fill in `profile.md` frontmatter and Snapshot section.
4. Add a line to "Active Clients" in this index file.
5. Add their email to `System/CLIENT_EMAIL_MAP.md`.
