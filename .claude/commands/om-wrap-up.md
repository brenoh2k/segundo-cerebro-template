# Wrap Up

Full session review before ending. Review context, ways of working, files modified, consistency, and suggest improvements.

## Usage

```
/om-wrap-up
```

Triggered when the user says "wrap up", "let's wrap", "wrapping up", or similar. Claude should invoke this automatically.

## Subagent

- **`brag-spotter`** — run at the end to find uncaptured wins and competency gaps from the session

## Workflow

### 1. Review What Was Done

Scan the conversation for:
- Notes created or modified (list them all with paths)
- People notes created or updated
- Indexes updated
- Brag doc entries added
- Brain notes updated (Patterns, Gotchas, Decisões-Chave, Memories)

### 2. Verify Note Quality

For each note created or modified this session:
- Frontmatter complete? (`date`, `quarter`, `description`, `tags`, type-specific fields)
- At least one wikilink to another note?
- In the correct folder? (`trabalho/ativos/` vs `trabalho/arquivo/` vs `trabalho/incidentes/` etc.)
- Description accurate and ~150 chars?
- Status field correct?

### 3. Check Index Consistency

- `trabalho/Index.md` — are new notes linked? Are completed projects in the right section?
- `cerebro/Memórias.md` — does Recent Context reflect what happened this session?
- Auto-memory index — if cerebro/ notes were added or their descriptions changed, REGENERATE the index instead of hand-editing it: `node --experimental-strip-types .claude/scripts/generate-memory-index.ts > <your ~/.claude/projects/<slug>/memory/MEMORY.md path>`. MEMORY.md is a derived view (pointers only); hand edits get overwritten by design.
- `equipe/Pessoas e Contexto.md` — any new people or relationship changes to capture?
- `desempenho/Conquistas.md` — any wins or achievements from this session?
- `Home.md` — are embedded Bases still valid?

### 4. Check for Orphans

- Any new notes not linked from at least one other note?
- Any new people not added to Pessoas e Contexto?
- Any thinking notes that should be promoted or deleted?

### 5. Archive Check

- Are there notes in `trabalho/ativos/` that should be moved to `trabalho/arquivo/YYYY/`?
- Any status fields still `active` that should be `completed`?

### 6. Ways of Working Review

**Index-first**: read each brain note's headline/one-liner structure, then open ONLY the topics this session actually touched — same knowledge transfer, a fraction of the tokens. Check if this session revealed:
- A new pattern that should be in `cerebro/Padrões.md`?
- A new gotcha that should be in `cerebro/Armadilhas.md`?
- A workflow improvement for `cerebro/Habilidades.md`?
- A CLAUDE.md update needed (new convention, stale reference)?
- A new or improved slash command?
- A hook that should be added or modified?

### 7. Suggest Improvements

Based on how the session went:
- Were there friction points in the workflow?
- Did we do something manually that could be automated?
- Did we repeat a pattern that should be a skill?
- Are there Bases that should be created or updated?
- Any frontmatter properties that would help future queries?

### 8. Report

Present a concise summary:
- **Done**: what was captured this session
- **Fixed**: issues found and resolved
- **Flagged**: things that need user input
- **Suggested**: improvements for next time

## Important

- This is a READ + VERIFY pass, not a creation pass. Fix small issues (broken links, missing frontmatter), but flag larger changes for user approval.
- Be honest about what's missing — the goal is leaving the vault in a better state than you found it.
- If Norte goals shifted during the session, suggest updating it.
