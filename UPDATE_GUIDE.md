# UPDATE GUIDE — Working Offline, Publishing, and Backups

This document is for internal use. It explains how to maintain this project safely.

## Work Offline
1. **Clone** the repository (first time only)
   ```bash
   git clone https://github.com/your-username/monte-carlo-gmp-pharma.git
   ```
2. **Edit locally** using VS Code or RStudio. All content is text-based (`.md`, `.R`).
3. **Preview images** from `/images`. R code lives in `/code`.

## Publish Changes
1. Check what changed
   ```bash
   git status
   git add -A
   git commit -m "Update chapter X / add example"
   git push
   ```
2. GitHub Pages updates automatically within ~1–2 minutes (if enabled).

## Rollback If Needed
- View **Commit history** on GitHub → click a previous commit → **Revert** or manually restore files.

## Add a New Chapter
1. Create `chapters/12_new_topic.md` (copy a previous file as template).
2. Update the **Table of Contents** in `README.md` if you want quick navigation.
3. Commit and push.

## Local Backups
- Zip the whole folder locally.
- Or export a `.zip` of the repository from GitHub: **Code → Download ZIP**.

## Safety Tips
- Keep the repository clean and descriptive commits.
- Prefer **plain Markdown** for maximum portability.
- Keep images both as **PNG** (compatibility) and **SVG** (scalable for slides).
