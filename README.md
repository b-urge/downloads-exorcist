# Downloads Exorcist

Downloads Exorcist organizes an unruly `haunted-downloads` folder into clear, purpose-built subfolders.

🔗 Hackathon: https://luma.com/wp7gehbn

## What it does

Downloads Exorcist classifies files and then:

- **Screenshots**: renames screenshots to a clean `YYYY-MM-DD` format.
- **Documents**: collects common document formats (spreadsheets, presentations, ebooks, archives, and PDFs).
- **Installers**: collects installer packages (e.g., `.dmg`).
- **Audio**: collects audio recordings and voice memos.
- **Video**: collects video and screen recordings.
- **Notes**: collects text-like notes (`.txt`, `.rtf`, etc.).
- **Spooky**: collects unusual/suspicious-looking files that don’t fit cleanly elsewhere.
- **Duplicates**: preserves files identified as duplicates (e.g., filenames containing `(1)`, `(2)`) by moving them into a `Duplicates` folder.

This project also includes an **`exorcism-report.pdf`**: an official-style certificate documenting the cleanup.

No files are deleted.

## What is Mel?

Mel is an AI coding assistant that works directly inside a terminal environment. It can inspect your project files, generate and modify code/documents, and run commands—while keeping you in control.

## Why I built this with Mel

I built this with Mel to demonstrate a practical, safety-first workflow for file operations:

1. Inspect the real contents of a folder.
2. Plan the moves and renames before executing them.
3. Preserve duplicates instead of deleting them.
4. Generate a human-readable report as proof of what happened.
5. Commit the results to GitHub so the changes are reviewable.

The “haunted” framing keeps the task engaging, while the preservation requirement makes the process reversible and safe.

## Project structure

```text
.
├── README.md
├── exorcism-report.pdf
└── haunted-downloads/
    ├── Audio/
    ├── Documents/
    ├── Duplicates/
    ├── Installers/
    ├── Notes/
    ├── Screenshots/
    ├── Spooky/
    └── Video/
```

## How to reproduce

### 1) Clone the repository

```bash
git clone https://github.com/b-urge/downloads-exorcist.git
cd downloads-exorcist
```

### 2) Inspect the folder state

```bash
find haunted-downloads -type f -print
```

### 3) Re-run the workflow with Mel

Ask Mel to:

- sort files into the eight destination folders above,
- rename screenshots to `YYYY-MM-DD`,
- move duplicate-marked files (e.g. `(1)`/`(2)`) into `Duplicates`,
- and **never delete anything**.

### 4) Generate the PDF certificate

Ask Mel to create `exorcism-report.pdf` in the project root, containing:

- today’s date,
- counts per folder,
- duplicate count,
- spookiest filenames,
- and a closing declaration that the folder was cleansed.

### 5) Commit and publish

```bash
git add -A
git commit -m "Organize haunted-downloads"
git push -u origin main
```

## Safety principles

- Never delete files.
- Preserve duplicates in `Duplicates`.
- Inspect before modifying.
- Plan before executing.
- Verify the resulting file count and folder structure.

## Hackathon

Made for the **Trick or Build hackathon**:

https://luma.com/wp7gehbn
