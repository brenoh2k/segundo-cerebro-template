---
date:
description: "Coisas que já deram problema antes e vão dar de novo — armadilhas, casos de borda e ciladas de teste"
tags:
  - brain
aliases:
  - Armadilhas
  - Gotchas
---

# Armadilhas

Coisas que já deram problema antes e vão dar de novo.

- **Não traduza o cabeçalho `## Current Focus` em [[Norte]]** — `.claude/scripts/session-start.ts` ancora a extração do resumo injetado no início de sessão nesse literal exato (`l.trim().startsWith("## Current Focus")`). Traduzir para "Foco Atual" não quebra o hook, mas o âncora falha silenciosamente: ele cai para as primeiras linhas do arquivo (frontmatter + preâmbulo) em vez do conteúdo de metas vivo, e a injeção de contexto perde a atualidade sem erro visível. Ver [[Padrões]] para a convenção bilíngue completa.
