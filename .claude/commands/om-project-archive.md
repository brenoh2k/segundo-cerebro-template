# Project Archive

Move a completed project from `trabalho/ativos/` to `trabalho/arquivo/YYYY/` and update all indexes.

## Usage

```
/om-project-archive <project name>
```

## Workflow

### 1. Find the Note

Search `trabalho/ativos/` for the project name. Confirm with the user before proceeding.

### 2. Update Frontmatter

- Set `status: completed`
- Verify `quarter` property is set correctly
- Verify `description` reflects the final state

### 3. Move the File

```bash
git mv "trabalho/ativos/<Note>.md" "trabalho/arquivo/YYYY/"
```

Use the year from the note's `date` field.

**Clustered workstreams**: when the project lives in a topic folder (`trabalho/ativos/<Topic>/` — the grouping convention for >1-note workstreams), move the WHOLE folder and keep the grouping:

```bash
git mv "trabalho/ativos/<Topic>" "trabalho/arquivo/YYYY/<Topic>"
```

Every note inside keeps its cluster context, and wikilinks resolve by basename so nothing breaks.

### 4. Update Indexes

- **`trabalho/Index.md`**: Move from Active Projects to the appropriate Completed quarter section
- **`cerebro/Norte.md`**: Mark as completed in Current Focus if listed there
- **`desempenho/Conquistas.md`**: Verify the project is captured in the relevant quarter's highlights
- **`cerebro/Memórias.md`**: Update Recent Context if the project is mentioned as "in progress"

### 5. Verify

- Run a quick check that no wikilinks are broken (Obsidian resolves by name, so moves shouldn't break links)
- Confirm the Painel de Trabalho Base shows the note in "Completed" view, not "Active Work"

## Important

- Always use `git mv` — never copy+delete
- Don't archive without user confirmation
- If the project has sub-notes (like incidents have RCA + deep dive), ask if those should move too
