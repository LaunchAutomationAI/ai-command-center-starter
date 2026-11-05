---
type: system
purpose: email-recognition
last_updated: YYYY-MM-DD
---

# Client Email Recognition Map

When an inbound email arrives (forwarded, pulled via Gmail connector, or referenced in chat), identify the sender before filing any notes.

## How to use this file

1. Match the sender address (case-insensitive) against the Email Address column below.
2. If matched, file communication notes in the listed vault folder.
3. If NOT matched, ask the user before assuming who it is. Never guess.

## Lookup Table

| Email Address (lowercase) | Client Name | Vault Folder | Label |
|---|---|---|---|
| (none yet, will fill in as you add clients) | | | |

## Adding a new entry

When a new client is added or a new email address is associated with an existing client:

1. Add a row to this table (lowercase email).
2. Add the email to the client's `profile.md` frontmatter (under `email` or `email_secondary`).
3. Update `last_updated` at the top of this file.
