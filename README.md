# Downloads Exorcist

An AI agent cleans up a chaotic, "haunted" Downloads folder: it sorts files into folders, renames junk, traps duplicates, and issues an official certificate saying the folder has been cleansed. The agent never deletes a single file.

Built with [Mel](https://www.openmel.dev/), the agentic terminal, as a demo for **Trick or Build**, a Halloween build night in Miami.

---

## Contents

- [What this project does](#what-this-project-does)
- [What is Mel?](#what-is-mel)
- [Why I chose Mel](#why-i-chose-mel)
- [How it works](#how-it-works)
- [Try it yourself](#try-it-yourself)
- [Repository layout](#repository-layout)
- [Safety notes](#safety-notes)

---

## What this project does

Most people's Downloads folder is a graveyard: duplicate installers, screenshots with timestamp names, `invoice_FINAL_v3 (2).pdf`, and files nobody remembers downloading. Downloads Exorcist shows how an AI agent can clean that up safely, with a person approving each step.

Starting from a messy folder of 40 files, the agent:

| Step | What happens |
| --- | --- |
| Sort | Groups files into `Screenshots`, `Documents`, `Installers`, `Audio`, `Video`, `Notes`, and `Spooky` |
| Rename | Turns names like `Screenshot 2026-10-12 at 3.14.07 PM.png` into clean `2026-10-12.png` |
| Contain duplicates | Moves every `(1)` and `(2)` copy into a `Duplicates` folder instead of deleting it |
| Report | Produces [`exorcism-report.pdf`](exorcism-report.pdf), a one-page certificate listing what was sorted |

**The result in this repo:** 29 files sorted into 7 folders, 11 duplicates contained, and all 40 files accounted for.

> This repository holds the folder **after** the exorcism. To watch the full before-and-after, follow [Try it yourself](#try-it-yourself).

## What is Mel?

[Mel](https://www.openmel.dev/) is a desktop terminal (macOS, Windows, Linux, and a VS Code extension) with an AI agent built in. It runs your normal shell, so you can type commands as usual. When you press **cmd+enter** (**ctrl+enter** on Windows and Linux) instead of enter, your request goes to the agent instead.

The agent can read files, run commands, and edit code in the folder you're working in. Key features:

- **Plain-English requests.** You describe the outcome; the agent works out the commands.
- **Plans before it acts.** It can propose a plan, and you can edit the plan before approving it.
- **Approvals.** Reading is free, but every file change or command pauses on an **Allow / Always allow / Deny** card.
- **Any model.** Works with Claude, GPT, Gemini, Grok, DeepSeek, and more, or `auto` to let Mel pick.
- **Everything in one window.** Terminal, agent, and code review live in the same place.

Mel is in early development (v0.1.x as of October 2026). See the [docs](https://www.openmel.dev/docs/getting-started) to get started.

## Why I chose Mel

I'm a Mel ambassador, and I picked this project for my first build because it shows what makes Mel different without needing any coding knowledge.

- **It's approachable.** I described the cleanup in a sentence. I didn't need to know `mv`, `find`, or shell scripting.
- **It's safe by design.** Mel showed me its plan and asked before every change. Combined with the instruction "never delete anything," I always knew what was happening to my files.
- **It shows its work.** Every command and its output appears in the terminal, so the cleanup is transparent rather than a black box.
- **It does more than code.** The same agent that moved the files also designed and generated the PDF certificate.
- **It's easy to undo.** Because Mel runs inside a normal terminal, a git save point let me reset the folder and rerun the demo as many times as I wanted.

## How it works

```
 1. Generate        2. Snapshot         3. Plan            4. Approve & run      5. Report
 ┌────────────┐    ┌────────────┐    ┌─────────────┐    ┌───────────────┐    ┌──────────────┐
 │ Mel creates │ →  │ git commit │ →  │ Mel proposes│ →  │ You approve;  │ →  │ Mel writes   │
 │ 40 fake     │    │ "haunted   │    │ folders,    │    │ Mel moves and │    │ the PDF      │
 │ messy files │    │  state"    │    │ renames,    │    │ renames files │    │ certificate  │
 └────────────┘    └────────────┘    │ duplicates  │    └───────────────┘    └──────────────┘
                                     └─────────────┘
```

1. **Generate.** Mel creates a realistic mess of placeholder files, so no real data is ever at risk.
2. **Snapshot.** A git commit saves the messy state, so the demo can be reset in seconds.
3. **Plan.** Mel proposes a plan and waits for approval before touching anything.
4. **Approve and run.** Each move or rename is approved through Mel's approval cards. **Always allow** speeds up the rest.
5. **Report.** Mel writes the exorcism certificate as a PDF using only tools already on the Mac.

## Try it yourself

### Prerequisites

- [Mel](https://www.openmel.dev/download) installed and signed in
- A model to use: a paid Mel plan, or a free key from [Groq](https://console.groq.com/keys) or [Google AI Studio](https://aistudio.google.com/apikey) added under **Settings → AI → Provider API keys**
- Git
- About 30 minutes

### 1. Create a workspace

In Mel, press **enter** after each line:

```bash
mkdir ~/exorcist
cd ~/exorcist
```

### 2. Summon the haunted folder

Press **cmd+enter** to send this to the agent:

> Create a folder called haunted-downloads in this directory and fill it with about 40 small fake files that look like a messy Downloads folder: screenshots named like "Screenshot 2026-10-12 at 3.14.07 PM.png", PDFs like "invoice_FINAL_v3.pdf", duplicate files ending in "(1)" and "(2)", random .dmg and .zip installers, some .mp3 and .mov files, notes like "untitled.txt", and a few spooky ones like "DO_NOT_OPEN.txt" and "ghost_photo.jpg". The files can be tiny placeholder text, they don't need to be real images.

### 3. Save a snapshot

```bash
git init
git add -A
git commit -m "haunted state"
```

### 4. Perform the exorcism

> Exorcise the haunted-downloads folder. First show me a plan and wait for my OK. The plan should: sort files into subfolders (Screenshots, Documents, Installers, Audio, Video, Notes, Spooky), rename screenshots to a clean YYYY-MM-DD format, find duplicates like "(1)" and "(2)" and move them into a Duplicates folder instead of deleting them, and never delete anything.

Review the plan, approve it, then approve the commands as they come.

### 5. Issue the certificate

> Write a one-page "Exorcism Report" as a PDF called exorcism-report.pdf in this folder. Make it look like an official paranormal certificate: a title, today's date, how many files were sorted into each folder, how many duplicates were trapped, the spookiest file names you found, and a closing line declaring the folder cleansed. Use only tools already installed on this Mac.

### Reset and run again

From `~/exorcist` **only**, return to the haunted state:

```bash
git reset --hard
git clean -fd
```

> **Warning:** these commands permanently discard every change since your last commit in the current folder. Check that you're in `~/exorcist` before running them.

## Repository layout

```
.
├── exorcism-report.pdf        # The generated certificate
└── haunted-downloads/
    ├── Audio/                 # .mp3 files
    ├── Documents/             # PDFs, spreadsheets, archives, slides
    ├── Duplicates/            # Every "(1)" / "(2)" copy, preserved
    ├── Installers/            # .dmg files
    ├── Notes/                 # .txt and .rtf notes
    ├── Screenshots/           # Renamed to YYYY-MM-DD.png
    ├── Spooky/                # ghost_photo.jpg, haunted-house.jpg
    └── Video/                 # .mov files
```

## Safety notes

- Every file in `haunted-downloads/` is a **placeholder** containing one line of text. Names like `passwords_old.txt` and `tax_documents_2025.zip` are props, not real data.
- Try this on generated files first, not your real Downloads folder. When you're ready to use it on real files, keep the "never delete anything" instruction and make a backup first.

---

Built by [Katie](https://github.com/b-urge) with Mel for Trick or Build: Mel × Prompt Anything × AI Builders, Miami, October 2026.
