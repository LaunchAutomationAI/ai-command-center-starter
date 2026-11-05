# Captures

Voice transcripts land here, one file per day. Format: `YYYY-MM-DD.md`.

This folder stays empty until your coach sets up the optional voice capture daemon (typically in a later phase, after you've used the foundation system for a while).

Once active, the daemon:
- Listens through your microphone
- Detects voice activity
- Transcribes locally using Whisper (no cloud, your voice stays on your computer)
- Appends to the day's file with timestamps

Each entry looks like:

```
## 09:32 AM  ·  18s
Quick reminder to follow up with Jane about the proposal.

## 09:45 AM  ·  62s
On the phone with Mike. He wants to add the upgrade tier. Need to send him the pricing sheet today.
```

Daily Briefings folder summarizes each day's captures into a structured briefing using Claude's Haiku model.

You control the daemon. Turn it off any time. Delete a day's file any time. Your voice, your data.
