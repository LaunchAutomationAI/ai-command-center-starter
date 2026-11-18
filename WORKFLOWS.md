# Small-business follow-up workflows

Customer work can get scattered across meeting notes, task lists and messages. These three workflows turn a small set of notes into a reviewable next-step list. They work with this kit's Markdown files and a file-capable assistant you have connected to your own vault.

Start with the [fictional practice notes](examples/fictional-follow-up-notes.md). They contain no real customer details. Copy that file into your vault's `Raw/` folder when you want to try the prompts. The example reference date is November 18, 2026; change it explicitly when using real notes.

## 1. Extract the action items after a meeting

Use this when you want to record commitments without inventing a deadline or a customer decision.

```text
Read only Raw/fictional-follow-up-notes.md. This is fictional practice data.
Extract the action items from the meeting notes. For each item, show:
client, action, owner, agreed due date, status, and source section.
Leave a missing owner or due date as Not agreed. A suggested date is not
an agreed deadline. Preserve completed items separately from open work.
Save a draft to Output/practice-meeting-actions.md. Do not update client
records, send messages, book appointments or connect external services.
Show me the output file path and any uncertainty I need to resolve.
```

Review the result. Alex's logo is still needed, the page outline is the owner's task, and no deadline was agreed for either. Do not turn the suggested Friday check-in into a commitment.

## 2. Review the follow-ups that need attention

Use an explicit reference date so that words such as overdue have a clear meaning.

```text
Use November 18, 2026 as the reference date. Read only
Raw/fictional-follow-up-notes.md and Templates/follow-up-review.md.
Create Output/practice-follow-up-review.md using the template.
Classify open items as Overdue, Due today, Due later, or No agreed date.
Only call an item overdue when its agreed due date is before the reference
date and it is still open. Keep waiting-on-customer items distinct from
work our team owns. Include a source section for each item.
Do not infer a sale, payment, consent or completed delivery from a note.
Propose next steps for my review. Do not send, schedule, charge, change
source files or connect external services.
```

The practice result should have one overdue open item: River Example Studio's quote promised for November 17. Morgan's completed checklist stays out of the open list. Alex's logo and outline belong under No agreed date. A reminder proposal is a draft, not a message that has been sent.

## 3. Prepare a client handoff

Use this before another person takes over work. Keep what was promised separate from what is still a suggestion.

```text
Read only the Alex Example section of Raw/fictional-follow-up-notes.md.
Prepare Output/practice-alex-handoff.md with these sections:
Known facts, Agreed commitments, Waiting on the customer, Open decisions,
and Suggested next steps. Cite the source section for each factual claim.
Leave contact details, pricing, payment and deadlines unknown where the
notes do not establish them. Do not use another client's facts to fill gaps.
Do not send the handoff or update any source records. Save a draft only.
```

## A quick check before using your own notes

- Use only notes you are authorized to process in the assistant and storage you chose.
- Start with one client or a small named set of files. Do not give the prompt a whole drive by default.
- Keep passwords, keys and payment credentials out of notes and prompts.
- Check the source behind each action, owner and date. Correct the underlying record when you find a mistake.
- Treat missing information as unknown. A quote request is not a sale, and a draft reminder is not a sent message.
- Keep source files unchanged until you have reviewed the draft and explicitly requested an update.

You can keep using these files without buying anything. If your team later needs shared customer records and assigned follow-ups in one browser workspace, [Launch OS](https://launchautomation.ai/launch-os) is a separate paid product from Launch Automation. This starter kit does not install it, connect to it or include its service.
