---
name: email-triage
description: >-
  Triage the user's email inbox. Reads unread/recent messages, sorts each one
  into a priority + category, applies Gmail labels, produces a short "what needs
  your attention" briefing, and drafts replies for the user to approve before
  anything is sent. Use this whenever the user asks to triage, sort, sift,
  clean up, process, "go through", or "get to inbox zero" on their email, or
  asks "what's important in my inbox?" or "anything I need to reply to?".
license: MIT
---

# Email Triage

## Purpose

This skill turns a noisy inbox into a short, ranked briefing and gets routine
replies ready to send. It is **read-first and draft-only**: it will read mail
and organize it with labels, but it will **never send an email, delete an
email, or archive anything permanently on its own**. Sending is always the
user's decision.

## What "triage" means here

For a batch of emails, the agent does four things, in order:

1. **Categorize** every message (priority + type).
2. **Label** each message in Gmail so the inbox stays organized.
3. **Brief** the user with a ranked summary of what actually needs them.
4. **Draft** replies for the messages that need a response, and leave them in
   Gmail's Drafts folder for the user to review and send.

## When to run

Trigger this skill when the user says things like:
- "Triage my inbox" / "sort my email" / "go through my unread mail"
- "What's important today?" / "Anything I need to reply to?"
- "Clean up my inbox" / "help me get to inbox zero"
- "Catch me up on email"

If the user does not say how far back to look, **default to unread messages
from the last 7 days**, and tell them that is what you did so they can widen
it if they want.

## Tools this skill relies on (Gmail connector)

This skill uses the **Gmail connector**. The exact tool names may look like
`Gmail.search_threads`, `Gmail.get_message`, `Gmail.create_label`,
`Gmail.label_message`, `Gmail.create_draft`, etc. Use whatever Gmail tools the
connector exposes. The capabilities you need are:

- **Search / list** messages or threads (to pull the batch to triage)
- **Read** a message or thread (subject, sender, body, date)
- **List labels** and **create labels** (to set up the triage labels once)
- **Apply a label** to a message or thread
- **Create a draft** reply (never send)

If the Gmail connector is not connected, **stop and tell the user** they need
to connect Gmail first, and point them to the "Connect the Gmail connector"
section of the project README. Do not guess or fabricate email content.

## Step-by-step procedure

### Step 1 — Make sure the triage labels exist

The first time you run (or any time a label is missing), list the existing
Gmail labels and create any of these that are not already there. Creating a
label that already exists is fine to skip.

Create these labels (they are safe, non-destructive, and easy for the user to
recognize):

- `Triage/Urgent`
- `Triage/Action-Needed`
- `Triage/Waiting-On`
- `Triage/FYI`
- `Triage/Newsletter`
- `Triage/Receipts`
- `Triage/Spam-Suspicious`

See `references/triage-rules.md` for exactly what belongs in each bucket.

### Step 2 — Pull the batch

Search for the messages to triage. Default query: unread mail from the last 7
days (for Gmail search this is typically `is:unread newer_than:7d`). If the
user asked for a different scope (e.g. "everything from this week", "just today",
"emails from my boss"), use that instead.

If there are more than ~30 messages, process the **most recent 30 first**, tell
the user how many are left, and offer to continue. Do not silently stop after a
subset — always report what you did and did not get to.

### Step 3 — Read and categorize each message

For each message, read the sender, subject, and body, then assign:

- **One priority:** `Urgent`, `Action-Needed`, `Waiting-On`, `FYI`,
  `Newsletter`, `Receipts`, or `Spam-Suspicious`.
- **A one-line reason** (why it got that priority).
- **Whether it needs a reply** (yes/no), and if yes, a one-line note on what the
  reply should say.

Use the rules in `references/triage-rules.md`. When you are genuinely unsure
between two buckets, pick the **higher-attention** one (e.g. prefer
`Action-Needed` over `FYI`) — it is safer to over-surface than to bury
something important.

**Never mark a message as spam and act on it destructively.** The
`Triage/Spam-Suspicious` label only *flags* it for the user to look at. You do
not delete or report anything.

### Step 4 — Apply labels

Apply the matching `Triage/...` label to each message. This is the only change
this skill makes to the mailbox, and it is fully reversible (the user can remove
a label at any time). Do **not** mark messages as read, do **not** archive, and
do **not** move anything to trash.

### Step 5 — Draft replies (only where a reply is genuinely needed)

For messages that need a response, create a **draft** reply in Gmail using the
tone and structure in `references/reply-templates.md`. Rules for drafts:

- Match the sender's formality. Keep it concise and professional.
- If you are missing a fact you would need to answer (a date, a number, a
  decision only the user can make), **do not invent it** — leave a clearly
  marked placeholder like `[[NAresh: confirm the delivery date]]` so the user
  sees exactly what to fill in.
- Never send. Only ever create a draft. Tell the user how many drafts you left
  and that they are in the Drafts folder awaiting their review.

### Step 6 — Deliver the briefing

Present a single, scannable summary to the user. Lead with what matters. Use
this shape:

```
📥 Inbox triage — <N> messages, <date range>

🔴 URGENT (needs you now)
  • <Sender> — <subject>  → <why> [draft ready]

🟠 ACTION NEEDED
  • <Sender> — <subject>  → <what to do> [draft ready]

🟡 WAITING ON OTHERS / FYI
  • <Sender> — <subject>  → <one line>

🟢 HANDLED / LOW PRIORITY
  • Newsletters: <N> labeled
  • Receipts: <N> labeled
  • Suspicious: <N> flagged for your review

✍️  I left <N> draft replies in your Drafts folder for you to review and send.
     I did NOT send anything.
```

Keep the urgent/action items specific; collapse the low-priority noise into
counts. End by asking if they want you to widen the search, draft more replies,
or send any of the drafts (which they can also do themselves in Gmail).

## Hard safety rules (do not break these)

1. **Never send email.** Drafts only.
2. **Never delete, trash, or permanently archive** any message.
3. **Never mark messages as read** unless the user explicitly asks.
4. **Never fabricate** email content, senders, dates, or facts in a draft. Use
   a clearly marked placeholder instead.
5. **Never act on the "spam/suspicious" flag** beyond labeling — no reporting,
   no blocking, no deleting.
6. If Gmail is not connected or a tool fails, **say so plainly** and stop;
   do not pretend the work was done.

## Reference files

- `references/triage-rules.md` — the exact definition of each priority bucket
  and how to decide.
- `references/reply-templates.md` — tone and ready-to-adapt reply patterns for
  common situations.
