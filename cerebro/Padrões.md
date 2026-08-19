---
date:
description: "Padrões e convenções recorrentes descobertos ao longo do trabalho — arquitetura, nomenclatura, ferramental e implementação"
tags:
  - brain
aliases:
  - Padrões
  - Patterns
---

# Padrões

Padrões recorrentes descobertos ao longo do trabalho.

- **Convenção bilíngue: prosa em PT-BR, cabeçalhos referenciados por ferramenta em EN** — ao traduzir o vault para português, a prosa e a maioria dos cabeçalhos viram PT-BR, mas alguns nomes de seção ficam deliberadamente em inglês porque hooks, comandos `/om-*` ou templates os referenciam literalmente (ex.: `## Current Focus` em [[Norte]], lido por `session-start.ts`). Antes de traduzir um cabeçalho de nota de infraestrutura (`cerebro/`, templates, notas geradas por comando), grep em `.claude/scripts/` e `.claude/commands/` pela string literal do cabeçalho — se algo depende dela, mantenha em inglês. Ver [[Armadilhas]] para o caso concreto do `## Current Focus`.
- **Documentar o contexto pessoal explicitamente no CLAUDE.md** — antes de usar o vault a sério, escreva 2-3 frases descrevendo seu papel, de onde vêm suas entradas reais (reuniões, ferramenta de tarefas, etc.) e o que o vault deve e não deve repetir de outras ferramentas. Sem isso, o Claude tende a inferir o contexto errado do template genérico e sugerir estrutura que não bate com seu trabalho real.

-
