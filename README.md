# Email Triage Skill for OpenClaw — Naresh's Setup Guide

Welcome, Naresh! 👋

This guide walks you through installing an **Email Triage** skill for your
OpenClaw agent. Once it's installed, you'll be able to say something like
*"triage my inbox"* and your agent will read your unread email, sort it by
importance, organize it with labels, tell you what actually needs you, and
even write draft replies for you to review.

**This guide is written for a non-technical person.** You do **not** need to
know how to code. Follow it step by step, in order, and you'll be done. If a
step uses a word you don't recognize, there's a plain-English explanation right
next to it.

> ⏱️ **Time needed:** about 15–20 minutes.
> 🧰 **You'll need:** your computer, your Gmail login, and your OpenClaw app
> already installed.

---

## 📖 Table of Contents

1. [What this skill does (and what it will NOT do)](#1-what-this-skill-does)
2. [Before you start (checklist)](#2-before-you-start)
3. [A quick vocabulary cheat-sheet](#3-vocabulary-cheat-sheet)
4. [Step 1 — Download the skill onto your computer](#step-1--download-the-skill)
5. [Step 2 — Find the hidden OpenClaw folder](#step-2--find-the-hidden-openclaw-folder)
   - [Mac](#-on-a-mac)
   - [Windows](#-on-windows)
   - [Linux](#-on-linux)
6. [Step 3 — Put the skill in the right place](#step-3--put-the-skill-in-the-right-place)
7. [Step 4 — Turn the skill on in your Agent file](#step-4--turn-the-skill-on-in-your-agent-file)
8. [Step 5 — Connect your Gmail (the connector)](#step-5--connect-your-gmail-the-connector)
9. [Step 6 — Test it](#step-6--test-it)
10. [Everything YOU have to do manually — quick list](#-everything-you-have-to-do-manually)
11. [Troubleshooting](#-troubleshooting)
12. [Frequently asked questions](#-frequently-asked-questions)

---

## 1. What this skill does

When you ask your OpenClaw agent to triage your email, it will:

- 📬 **Read** your unread email (by default, the last 7 days).
- 🗂️ **Sort** each message into a category: *Urgent, Action Needed, Waiting On,
  FYI, Newsletter, Receipts,* or *Suspicious/Spam.*
- 🏷️ **Label** each email in Gmail so your inbox stays organized (it creates
  neat labels like `Triage/Urgent`).
- 📋 **Brief you** with a short, ranked summary — the important stuff first, the
  noise collapsed into simple counts.
- ✍️ **Write draft replies** for the emails that need a response, and leave them
  in your **Drafts** folder for you to check and send.

### 🔒 What it will **NOT** do (your safety guarantees)

This skill is deliberately careful. It will **never**:

- ❌ **Send** an email on its own — *you* always press send.
- ❌ **Delete** or trash any email.
- ❌ **Archive** or hide your mail.
- ❌ **Mark things as read** without you asking.
- ❌ **Make up** facts in a draft — if it needs a detail only you know, it leaves
  an obvious blank like `[[Naresh: confirm the date]]` for you to fill in.

In short: it *organizes and prepares*, but every real action (sending, deleting)
stays in your hands.

---

## 2. Before you start

Please make sure you have all of these ready. ✅

- [ ] **OpenClaw is already installed** on your computer. (This guide does not
      install OpenClaw itself — it assumes it's there. If it isn't, install
      OpenClaw first, then come back.)
- [ ] You **know your Gmail address and password**, and can log into Gmail in a
      web browser.
- [ ] You have **about 20 minutes** and won't be interrupted.
- [ ] You can find your computer's **Home folder** (that's the folder with your
      name on it — we'll show you how).

You do **not** need: a GitHub account, coding tools, or the command line
(unless you *want* to use it — an optional shortcut is included).

---

## 3. Vocabulary cheat-sheet

A few words appear throughout this guide. Here's what they mean in plain English:

| Word | What it really means |
|------|----------------------|
| **OpenClaw** | The AI assistant app you've already installed. |
| **Skill** | A little bundle of instructions that teaches your agent a new ability — in this case, email triage. It's just a folder of text files. |
| **Agent file** | A settings/config file that tells your OpenClaw agent which skills and tools it's allowed to use. Think of it as the agent's "job description." |
| **Connector** | A secure link between OpenClaw and another app (here, Gmail) so the agent can read your email. You approve it by logging in. |
| **Hidden folder** | A folder your computer keeps out of sight to avoid clutter. OpenClaw stores its settings in one. We'll show you how to reveal it. |
| **Home folder** | The top folder for your user account. On Mac it's your name under "Users"; on Windows it's `C:\Users\YourName`; on Linux it's `/home/yourname`. |

---

## Step 1 — Download the skill

You need to get the skill files from GitHub onto your computer. Pick **one** of
the two options below. **Option A is the easiest and needs no special software.**

### Option A — Download as a ZIP (recommended, no tools needed)

1. Open your web browser and go to the project page on GitHub:
   **https://github.com/jvaughan007/Naresh-emailTriage**
2. Click the green **`< > Code`** button near the top right.
3. In the little menu that appears, click **Download ZIP**.
4. The file `Naresh-emailTriage-main.zip` will land in your **Downloads** folder.
5. **Unzip it** (this "opens" the compressed file into a normal folder):
   - **Mac:** double-click the ZIP file. A new folder appears next to it.
   - **Windows:** right-click the ZIP → **Extract All…** → **Extract**.
   - **Linux:** right-click the ZIP → **Extract Here**.
6. You now have a folder called **`Naresh-emailTriage-main`** (or similar) in
   your Downloads. Inside it, you'll find a folder called **`skills`** — and
   inside *that*, a folder called **`email-triage`**. That `email-triage` folder
   is the piece we'll be moving. 👍

### Option B — Use Git (only if you're comfortable with the command line)

If you already have Git installed and don't mind a terminal, run:

```bash
git clone https://github.com/jvaughan007/Naresh-emailTriage.git
```

This creates a `Naresh-emailTriage` folder with the same `skills/email-triage`
folder inside.

> **Either way, the important thing is:** you now have a folder named
> **`email-triage`** somewhere on your computer (inside `skills`). Keep that
> window open — we'll need it in Step 3.

---

## Step 2 — Find the hidden OpenClaw folder

OpenClaw keeps its settings and skills in a **hidden folder** inside your Home
folder. It's called **`.openclaw`** (the dot at the front is what makes it
hidden). Your computer hides it by default, so first we need to **reveal hidden
folders**, then navigate into it.

> 💡 **Where is it?** In almost all cases it's directly inside your Home folder:
> - **Mac:** `/Users/YourName/.openclaw`
> - **Windows:** `C:\Users\YourName\.openclaw`
> - **Linux:** `/home/yourname/.openclaw`
>
> If you can't find it in your Home folder, don't worry — the "If you still
> can't find it" box at the end of this step shows you how to search for it.

Pick your computer type below. 👇

---

### 🍎 On a Mac

**Reveal hidden folders:**

1. Open **Finder** (the smiley-face icon in your Dock).
2. Press these three keys **at the same time**:
   **`Command (⌘)` + `Shift` + `.` (the period key)**
3. Hidden files and folders will suddenly appear (they look slightly faded).
   Pressing the same keys again hides them — leave them shown for now.

**Navigate to the folder:**

1. In Finder's top menu, click **Go → Home** (or press
   `Command (⌘)` + `Shift` + `H`). This opens your Home folder.
2. Look for a faded folder named **`.openclaw`** and double-click it.

**A guaranteed shortcut if you don't see it:**

1. In Finder's top menu click **Go → Go to Folder…**
   (or press `Command (⌘)` + `Shift` + `G`).
2. Type exactly: `~/.openclaw` and press **Return**.
   *(The `~` symbol is shorthand for your Home folder.)*
3. Finder jumps straight into the `.openclaw` folder. ✅

---

### 🪟 On Windows

**Reveal hidden folders:**

1. Open **File Explorer** (the folder icon on your taskbar).
2. At the top, click the **View** menu.
   - **Windows 11:** click **View → Show → Hidden items** (put a check next to it).
   - **Windows 10:** click the **View** tab, then tick the **Hidden items**
     checkbox on the right.
3. Hidden folders now appear (slightly faded).

**Navigate to the folder:**

1. In File Explorer, click in the **address bar** at the very top (the long bar
   that shows your current location).
2. Type exactly: `%USERPROFILE%\.openclaw` and press **Enter**.
   *(`%USERPROFILE%` is a shortcut Windows understands for your Home folder,
   e.g. `C:\Users\Naresh`.)*
3. File Explorer opens the `.openclaw` folder. ✅

*(If you prefer clicking: go to `This PC → C: → Users → YourName`, and the faded
`.openclaw` folder will be there once hidden items are shown.)*

---

### 🐧 On Linux

**Reveal hidden folders:**

1. Open your file manager (**Files / Nautilus** on Ubuntu, **Dolphin** on KDE,
   etc.).
2. Press **`Ctrl` + `H`** to show hidden files. (Press it again to hide them.)
   *(In most Linux file managers, `Ctrl + H` is the universal "show hidden"
   shortcut.)*

**Navigate to the folder:**

1. Click **Home** in the sidebar to open your Home folder
   (`/home/yourname`).
2. Find the folder named **`.openclaw`** and open it.

**Shortcut using the address bar:**

1. In Files/Nautilus, press **`Ctrl` + `L`** to turn the location bar into a
   typing box.
2. Type: `~/.openclaw` and press **Enter**. ✅

---

> ### 🔍 If you STILL can't find the `.openclaw` folder
>
> It may live somewhere other than your Home folder. Here's how to hunt it down:
>
> **Mac / Linux (Terminal):**
> ```bash
> find / -type d -name ".openclaw" 2>/dev/null
> ```
> This searches your whole computer and prints the full path of any `.openclaw`
> folder it finds. Use that path instead of `~/.openclaw`.
>
> **Windows (Command Prompt):**
> ```cmd
> dir C:\.openclaw /a /s /b 2>nul & where /r C:\Users .openclaw 2>nul
> ```
> Or simply type `.openclaw` into the Windows **search box** in the Start menu.
>
> **Still nothing?** Then OpenClaw may not have created its folder yet. **Open
> the OpenClaw app once and close it** — many apps create their settings folder
> on first launch. Then look again. If it's genuinely not there, OpenClaw may
> not be installed correctly; reinstall it, or check its own documentation for
> where it stores skills.

---

## Step 3 — Put the skill in the right place

Now we move the `email-triage` folder into OpenClaw's **skills** folder.

1. Inside the `.openclaw` folder you opened in Step 2, look for a sub-folder
   named **`skills`**.
   - **If `skills` already exists,** open it.
   - **If there is NO `skills` folder,** create one:
     right-click in an empty area → **New Folder** → name it exactly
     **`skills`** (all lowercase).
2. Go back to the folder you downloaded in **Step 1**. Open it and find:
   `skills` → **`email-triage`**.
3. **Copy** the entire **`email-triage`** folder
   (right-click it → **Copy**), then go into `.openclaw/skills/` and
   **Paste** it (right-click empty area → **Paste**).

When you're done, the folder layout should look **exactly** like this:

```
.openclaw/
└── skills/
    └── email-triage/
        ├── SKILL.md
        └── references/
            ├── triage-rules.md
            └── reply-templates.md
```

> ✅ **The one thing that must be right:** the file **`SKILL.md`** has to sit
> directly inside a folder called **`email-triage`**, which sits inside
> **`skills`**, which sits inside **`.openclaw`**. If `SKILL.md` ends up one
> level too deep (e.g. `skills/email-triage/email-triage/SKILL.md`) or too
> shallow, OpenClaw won't find the skill. Double-check the layout above.

> ⚠️ **Copy the folder, not just the files.** Keep the `email-triage` folder and
> its `references` sub-folder together. Don't split them up.

---

## Step 4 — Turn the skill on in your Agent file

OpenClaw usually finds skills in the `skills` folder automatically. But to be
safe — and because your agent needs *permission* to touch your email — you
should make sure the skill and the Gmail tools are enabled in your **Agent
file**.

The Agent file is the settings file that tells your agent what it's allowed to
do. It lives inside `.openclaw` and is usually one of these:

- `.openclaw/agent.md`  *(a plain-text instructions file)*, **or**
- `.openclaw/config/agent.yaml` / `.openclaw/agents/<name>.yaml`
  *(a settings file)*, **or**
- a settings screen inside the OpenClaw app itself.

Open whichever one your installation has. (If you're not sure, open the
`.openclaw` folder and look for a file with `agent` in its name. You can open it
with any plain text editor — TextEdit on Mac, Notepad on Windows, gedit on
Linux.)

### If your Agent file is a text/Markdown file (`agent.md`)

Add a short section like this (anywhere in the file is fine). This tells the
agent it may use the skill and the Gmail connector:

```markdown
## Skills
- email-triage: Use this skill whenever I ask you to triage, sort, clean up,
  or catch me up on my inbox/email.

## Connectors this agent may use
- Gmail (read messages, manage labels, create drafts). Do NOT send or delete
  email without my explicit confirmation.
```

### If your Agent file is a YAML settings file

Make sure the skill and the Gmail connector/tool are listed as enabled. It will
look something like this (your exact field names may differ slightly — match the
style already in your file):

```yaml
skills:
  - email-triage        # enables the email triage skill

connectors:
  - gmail               # allows the agent to use the Gmail connector

permissions:
  gmail:
    read: true          # read messages
    labels: true        # create and apply labels
    drafts: true        # create draft replies
    send: false         # IMPORTANT: keep sending OFF — you send manually
    delete: false       # keep deletion OFF
```

### If OpenClaw has a settings screen (no file to edit)

Open the app's **Settings → Skills** and make sure **email-triage** is toggled
**on**. Then open **Settings → Connectors/Integrations** and confirm **Gmail**
is enabled (you'll actually connect it in the next step).

> 💾 **Save the file** after editing (Mac: `Command + S`; Windows/Linux:
> `Ctrl + S`). Then **fully quit and reopen the OpenClaw app** so it re-reads
> its settings and notices the new skill.

---

## Step 5 — Connect your Gmail (the connector)

The skill can't read your email until OpenClaw is connected to your Gmail
account. This is a **one-time** login you do yourself — for your security,
nobody can do this part for you.

1. Open the **OpenClaw app**.
2. Go to **Settings → Connectors** (it might be called **Integrations** or
   **Tools** — look for the section that lists outside apps).
3. Find **Gmail** in the list and click **Connect** (or **Add** / **Sign in**).
4. A Google login window opens. **Log in with the Gmail account you want triaged.**
5. Google will show a **permissions screen** asking to allow OpenClaw to access
   your mail. Read it, and click **Allow / Continue**.
   - It will ask for permission to **read your email**, **manage labels**, and
     **create drafts**. That's exactly what this skill needs.
6. When it returns you to OpenClaw and shows Gmail as **Connected** ✅, you're set.

> 🔐 **Is this safe?** You are logging in directly with Google, and you're only
> granting the specific permissions Google shows you. You can revoke this access
> at any time from your Google Account under **Security → Third-party access**.
> This skill is also built to never send or delete anything on its own.

> ℹ️ **If you don't see Gmail in the connector list:** your OpenClaw install may
> need the Gmail connector added first. Check OpenClaw's own documentation for
> "add a connector" or "add an integration," add **Gmail**, then come back to
> step 3 above.

---

## Step 6 — Test it

Let's make sure everything works. 🎉

1. Open the **OpenClaw app**.
2. Type this to your agent:

   > **"Triage my inbox."**

3. The agent should:
   - Tell you it's reading your recent unread mail.
   - Create the `Triage/...` labels (the first time only).
   - Give you a ranked summary — urgent stuff first.
   - Tell you it left some **draft** replies in your Drafts folder.

4. **Check the results:**
   - Open Gmail in your browser. In the left sidebar you should see new labels
     starting with **`Triage/`**.
   - Open your **Drafts** folder — you should see the draft replies waiting for
     you. Read them, fill in any `[[Naresh: …]]` blanks, and send the ones you
     like. **The agent did not send them — that's your job, on purpose.**

5. Try a few more phrasings to get comfortable:
   - *"What's important in my inbox today?"*
   - *"Anything I need to reply to?"*
   - *"Catch me up on email from the last 3 days."*

If it worked — you're done! 🥳 From now on, just ask your agent to triage
whenever your inbox gets busy.

---

## ✅ Everything YOU have to do manually

Here's the short checklist of the things **only you can do** — collected in one
place so nothing slips through:

1. **Have OpenClaw installed** before starting (this guide doesn't install it).
2. **Download the skill** and place the `email-triage` folder into
   `.openclaw/skills/` (Steps 1–3).
3. **Enable the skill in your Agent file** (or the Settings → Skills screen),
   and make sure **Gmail** is allowed with **send OFF** and **delete OFF**
   (Step 4).
4. **Connect your Gmail account** by logging in and approving permissions —
   for security, this can only be done by you (Step 5).
5. **Restart the OpenClaw app** after changing settings so it reloads the skill.
6. **Review and send the drafts yourself.** The agent prepares them; you decide
   what actually goes out. Same for deleting — the agent never deletes; if you
   want mail gone, you remove it.
7. **(Optional) Personalize.** If you'd like different labels, a different
   default time window (e.g. 3 days instead of 7), or a different reply tone,
   tell your agent — or ask your setup person (Josh) to tweak the files in
   `skills/email-triage/`.

---

## 🛠 Troubleshooting

**"The agent says it doesn't have an email triage skill."**
- The folder is probably in the wrong place. Re-check Step 3 — `SKILL.md` must be
  at `.openclaw/skills/email-triage/SKILL.md` exactly.
- Restart the OpenClaw app so it re-scans for skills.
- Make sure you copied the **folder**, not just the loose files.

**"The agent can't read my email / says Gmail isn't connected."**
- Go back to Step 5 and connect Gmail. Confirm it shows **Connected**.
- In your Google Account (**Security → Third-party access**), make sure you
  didn't accidentally remove OpenClaw's access.

**"I can't find the `.openclaw` folder at all."**
- Re-read Step 2 and make sure hidden files are being shown.
- Use the "If you STILL can't find it" search box in Step 2.
- Open and close the OpenClaw app once to make it create the folder, then look
  again.

**"There's no `skills` folder inside `.openclaw`."**
- That's fine — just create one named exactly `skills` (all lowercase), then
  continue with Step 3.

**"The agent tried to send/delete an email."**
- It shouldn't — the skill forbids this. If it happened, your Agent file may have
  `send: true` or `delete: true` set. Open the Agent file (Step 4) and set both
  to `false`, then restart the app. If you're unsure, ask Josh to check it.

**"The labels didn't appear in Gmail."**
- Gmail sometimes hides labels. In Gmail's left sidebar, scroll down and click
  **More**, then look for the `Triage/...` labels. You can also go to Gmail
  **Settings → Labels** to make them always show.

**"It only triaged some of my emails."**
- By design, it handles the most recent ~30 at a time and tells you how many are
  left. Just say *"keep going"* or *"do the rest."*

**Still stuck?** Take a screenshot of what you see and send it to Josh — he can
look at the exact spot you're stuck on.

---

## ❓ Frequently asked questions

**Will this delete or send any of my emails?**
No. It only reads, labels, and writes drafts. Sending and deleting are always
done by you, by hand.

**Can it read emails I don't want it to see?**
It reads the batch you ask it to triage (by default, recent unread mail). It
doesn't share your email anywhere — it just summarizes it back to you inside
OpenClaw.

**Can I change the categories or the reply tone?**
Yes. Those live in plain-text files inside the skill
(`skills/email-triage/references/`). Ask Josh to adjust them, or tell your agent
what you'd prefer.

**Do I have to do all this every time?**
No — this whole guide is a **one-time setup**. After it's done, you just say
"triage my inbox" whenever you want.

**What if I use Outlook instead of Gmail?**
This version is built for Gmail. If you need Outlook, ask Josh — the same skill
can be pointed at an Outlook/Microsoft connector instead.

---

*Built as an OpenClaw skill. Licensed under MIT (see `LICENSE`). Questions about
setup? Contact Josh.*
