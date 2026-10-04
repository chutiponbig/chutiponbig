# File hub: local Claude Code ⇄ cloud Claude Code

This repo moves files between a local Claude Code session and a cloud session
that converts documents to Markdown (OCR included).

## Workflow

1. **Local session**: put source files in `inbox/<batch>/` on branch `file-hub`, then commit and push.
   - `<batch>` is a short name, e.g. `2026-10-04-contracts`.
   - Optional: add `inbox/<batch>/NOTES.md` with instructions (language, table handling, pages to skip).
2. **Cloud session**: pulls `file-hub`, converts each file, and pushes the results to
   `outbox/<batch>/<original-name>.md`.
3. **Local session**: runs `git pull origin file-hub` and picks up the `.md` files from `outbox/<batch>/`.

## Conversion defaults (unless NOTES.md says otherwise)

- One `.md` per source file, with the same base name.
- Text-layer PDFs: extract the text layer. Scanned PDFs and images: OCR the page images.
- Tables become Markdown tables. Figures become a short `[Figure: …]` description.
- Text that can't be read is marked `[illegible]`. Nothing is guessed or filled in.
- Page breaks are marked `<!-- page N -->`.

## Limits

- GitHub rejects any file over 100 MB and warns above 50 MB. Split large PDFs first.
- The repo is the transport, so don't push files you aren't allowed to store on GitHub.
  Make sure the repo is **private** before pushing confidential documents.
