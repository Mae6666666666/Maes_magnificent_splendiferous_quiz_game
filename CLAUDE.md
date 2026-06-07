# CLAUDE.md

Guidance for Claude when working in this repo.

## What this project is

A browser-based quiz game ("Mae's Magnificent Splendiferous Quiz Game"). Quiz
questions live in `questions.json`. The frontend reads that data and presents
questions, collects answers, and scores the player.

## Who does what (important)

This is a **learning project for Mae**, and the division of labor is the whole
point — it is the deliberate inverse of the `tarot_api` project, where Mae did
the backend and Claude did the frontend.

- **Mae owns the frontend.** HTML, CSS, and the JavaScript that runs in the
  browser. She is learning front-end development by writing this herself.
- **Claude owns the backend.** Any server, API, data layer, build tooling, or
  persistence work.

### Rules for Claude

1. **Do not write frontend code for Mae unless she explicitly asks.** Writing it
   for her defeats the purpose. Default to *teaching*: explain concepts, suggest
   approaches, point at the relevant MDN docs, review what she wrote, and help
   debug. When she does ask for a code example, keep it small and explain every
   part so she learns from it.
2. **Explain the "why," not just the "what."** Mae is new to frontend, so favor
   clear explanations over terse answers. Introduce one concept at a time.
3. **When reviewing her frontend code,** point out bugs and suggest
   improvements, but let her make the edits unless she asks you to.
4. **The backend is yours to build and maintain.** Implement it properly, but
   keep the interface between frontend and backend simple and well-documented so
   Mae can consume it from the browser.
5. **Agree on the data shape before diverging.** `questions.json` is the contract
   between frontend and backend — see below.

## Tech stack

- Start simple: plain HTML, CSS, and vanilla JavaScript (no framework). No build
  step needed early on; open the HTML file in a browser or serve it locally.
- A local static server avoids `fetch()` CORS/file-protocol issues:
  `python3 -m http.server` then visit `http://localhost:8000`.
- Backend stack is TBD and Claude's call when the project needs one (e.g. to
  serve questions, save scores, or add a leaderboard).

## Data: questions.json

This file is the shared contract. Today its shape is inconsistent — questions
and answers are sometimes plain strings and sometimes objects carrying image
URLs. Before building much on top of it, settle on **one consistent schema** for:

- a question (text, optionally an image)
- an answer (text, optionally an image)
- which answer is correct (not yet represented — needed for scoring)

When Mae's frontend and Claude's backend both read/write this file, neither side
should change the schema unilaterally. Propose the change, agree, then update
both sides.

## Conventions

- Keep frontend and backend code in clearly separate folders once both exist
  (e.g. `frontend/` and `backend/`).
- Commit and push only when Mae asks.
