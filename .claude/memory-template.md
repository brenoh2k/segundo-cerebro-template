# Auto Memory

All project memories live in the vault (git-tracked). This file is a lightweight index.

## Rule: Vault-First Memories

**All new memories for this project MUST be written to vault notes in `cerebro/`, NOT to files in this directory.**

- Durable knowledge → `cerebro/` notes (git-tracked, Obsidian-browsable, linked)
- This `MEMORY.md` → index only, pointers to vault locations
- Never create new `.md` files in this `~/.claude/` memory directory — they aren't version-controlled

## Where to Find Things

| Topic | Vault Location |
|-------|---------------|
| Technical gotchas | `cerebro/Armadilhas.md` |
| Patterns and conventions | `cerebro/Padrões.md` |
| Key decisions | `cerebro/Decisões-Chave.md` |
| Goals and focus | `cerebro/Norte.md` |
| Slash commands and skills | `cerebro/Habilidades.md` |
| People and org context | `equipe/Pessoas e Contexto.md` |
| Active work and projects | `trabalho/Index.md` |
| Performance evidence | `desempenho/Conquistas.md` |

## Setup

1. Find your project memory path: `~/.claude/projects/<encoded-path>/memory/`
2. Copy this file there as `MEMORY.md`
3. Claude Code will auto-load it at the start of every conversation
4. When Claude creates memories, they go to vault notes — not this directory
