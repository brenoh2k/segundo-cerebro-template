---
description: "Morning kickoff. Load today's context, review yesterday, surface open tasks, and identify priorities."
---

Run the morning standup.

**Start from the SessionStart injection — do NOT re-read what it already carries.** The hook has already injected: the Norte excerpt, active work, recent git changes, open tasks, hygiene flags (incl. open loops), and the file listing. Re-reading `Home.md`, `cerebro/Norte.md`, or re-running `git log` doubles the token cost for zero new information.

Gather only what the injection does NOT have:

1. Read yesterday's and today's daily notes if they exist: `obsidian daily:read`
2. List Obsidian-tracked tasks: `obsidian tasks daily todo` (the injected Open Tasks section covers checkbox tasks in active notes and the vault root — this adds daily-note tasks)
3. Read `trabalho/Index.md` ONLY if the injected active-work list needs status detail the summary will actually use
4. Check for unprocessed inbox items (`trabalho/reunioes/` raw exports — the hygiene flags name them when they age)
5. **Reconcile yesterday's calendar with the vault** — check whether any of yesterday's meetings have a Gemini transcript that hasn't been captured yet:
   - List yesterday's events on the primary calendar (`mcp__claude_ai_Google_Calendar__list_events`, `startTime`/`endTime` = yesterday, your own calendar address).
   - For each event with an "Anotações do Gemini" attachment, check if it's already reflected in the vault (yesterday's daily-note entry, the matching project note in `trabalho/ativos/`, or `trabalho/individuais/` for a 1:1).
   - If not captured: read the note (`mcp__claude_ai_Google_Drive__read_file_content` on the file ID from the attachment's `fileUrl`) and route it the same way `/om-dump` would — project meeting → the relevant work note; internal/daily meeting → the relevant work note; 1:1 → `trabalho/individuais/`.
   - Skip events with no Gemini attachment (nothing to pull) and events already reflected in the vault (don't duplicate entries).
   - Known limits: only sees events on Breno's own calendar (meetings he's not on won't show), and not every meeting has Gemini notes enabled.
   - Report in the standup summary exactly what got pulled in and filed, and what was skipped and why — a meeting should never silently go uncaptured.

Present a structured standup summary:
- **Yesterday**: What got done (from the injected Recent Changes + daily note + any meeting notes just reconciled in step 5)
- **Active Work**: Current projects in trabalho/ativos/ with their status
- **Open Tasks**: Pending items
- **Open Loops**: stale follow-ups from the injected hygiene flags — anything to chase today?
- **Norte Alignment**: How active work maps to current goals
- **Suggested Focus**: What to prioritize today based on goals + open items — act on injected hygiene flags here

Keep it concise. This is a quick orientation, not a deep dive.

## Daily TODO Note

After the summary, maintain the visual daily checklist in `trabalho/diario/YYYY-MM-DD.md` (Obsidian Daily Notes core plugin, configured to that folder with the `modelos/TO DO Diário` template):

1. **Reconcile yesterday's daily note first, if one exists** (`trabalho/diario/<yesterday>.md`): for every checked box (`- [x]`) that links back to a source task in `trabalho/ativos/*` or elsewhere, mark that same task done at its source too — check the box there, don't just leave it checked only in the daily note. Unchecked items don't need action; they'll be re-surfaced below if still open.
2. **Generate today's note** at `trabalho/diario/YYYY-MM-DD.md` from the template. Populate `## To Do` with fresh unchecked boxes aggregating:
   - Open checkbox items from `trabalho/ativos/*.md` (the ones already surfaced in the injected Open Tasks section)
   - Open loops from the hygiene flags worth chasing today
   - Anything from today's Suggested Focus that isn't already a checkbox elsewhere
   Each item should link back to its source note (e.g. `- [ ] Cobrar retorno do fornecedor ([[Projeto Alfa]])`) so reconciliation tomorrow knows where to write the checkmark back to. Leave `## Notas do Dia` empty for freeform additions during the day.
3. If today's note already exists (e.g. standup re-run), don't duplicate — just refresh the To Do section with any newly surfaced items, preserving existing checks.

This note is the visual, checkable surface in Obsidian — open it via the Daily Notes ribbon icon or `obsidian daily:read`/`obsidian create`. Checking a box here is the day-to-day habit; the reconciliation step (1) is what keeps it honest with the source notes.
