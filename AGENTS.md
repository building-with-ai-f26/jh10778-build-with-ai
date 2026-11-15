# AGENTS.md — Coding Agent Operating Manual

> Give this file to your coding agent and check that it is using these instructions. Keep the stack, commands, and ground rules current.

## 1. Project Overview
- **What this repo builds:** Hidden Shelf. A reader picks a book they loved, writes a short structured reflection (three words, the moment they still remember, what it changed in them), and gets five lesser-known books from Open Library with a reason for each.
- **Primary user & core workflow:** NYU Stern MBA classmates who read for pleasure. Core workflow: pick a book → write the reflection → get five hidden gems. See the living PRD in `docs/index.html`.
- **Tech stack:** Plain HTML + CSS + JavaScript in one file, no framework and no build step. Data from the Open Library Search API (free, no key). Analytics with PostHog (US cloud). No backend yet; an AI model (via OpenRouter, key in `.env`) is planned for Build 3 and will need a small backend so the key never reaches the browser.

## 1b. Project Structure
| Path | What it is |
| --- | --- |
| `prototype/index.html` | The app. All UI, matching logic and PostHog events live in this one file. |
| `docs/index.html` | Public Product Page, living PRD and build log, published with GitHub Pages from `/docs`. |
| `docs/*.png` | Screenshots used on the Product Page. |
| `AGENTS.md` | This file: context and rules for coding agents. |
| `.env.example` | Placeholder for future private keys. The real `.env` is ignored by Git. |
| `Intent.md`, `Plan.md`, `journal/`, `tests/`, `SPONSOR_MEMO.md` | Course templates (optional drafts, evals in Build 4, memo in Week 6). |

**PostHog events** (sent by `track()` in `prototype/index.html`): `book_searched`, `book_selected`, `reflection_submitted`, `recommendations_shown`, `open_library_error`, plus automatic pageviews, clicks and session replay. The PostHog project token in the HTML is public by design; never put private keys in the HTML.

## 2. Commands
- **Install dependencies:** none. Requires Python 3 (preinstalled on macOS) to serve the files.
- **Run locally:** from the repo root, `python3 -m http.server 8000`, then open http://localhost:8000/prototype/ (Product Page preview: http://localhost:8000/docs/). Stop the server with `Ctrl + C`.
- **Run deterministic tests:** none yet (planned for Build 4).
- **Run model evals:** none yet (no AI model until Build 3).

## 3. Non-Negotiable Engineering Rules
1. **Plan before coding:** Before touching multiple files, propose a brief plan and wait for approval.
2. **Small batches:** Make small, focused changes that can be reviewed and explained by a human in a single Pull Request.
3. **Explainability:** Avoid unnecessary abstractions or dependencies. Help the human builder understand the main components, what changed, why it matters, what could break, and how it was checked.
4. **Verify changes:** Run relevant checks. For a reproducible logic bug, use a failing test to demonstrate the fix when practical. Record manual checks and known limitations; follow the selected Build 4 evaluation track.
5. **Zero secrets in code:** Never hardcode API keys, tokens, or credentials. Always read from environment variables (`.env`) and update `.env.example` when new variables are needed.
6. **Stop when looping:** If a fix fails twice in a row, stop, summarize what failed, and ask the human before trying a third approach.
