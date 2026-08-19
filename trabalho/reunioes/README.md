---
date: 2026-04-07
description: "Caixa de entrada para exportações brutas de reunião — jogue as notas aqui e rode /om-intake para classificar e rotear para as notas certas do vault"
tags:
  - index
aliases:
  - Caixa de Entrada de Reuniões
---

# Caixa de Entrada de Reuniões

Jogue aqui as notas de reunião exportadas ou brutas. Rode `/om-intake` para processar todos os arquivos — ele lê cada um, classifica o conteúdo e roteia tudo para os lugares certos do vault:

- Notas de 1:1 → `trabalho/individuais/<Pessoa> AAAA-MM-DD.md`
- Atualizações de projeto → a nota correspondente em `trabalho/ativos/`
- Decisões → Registro de Decisão + registro de decisões em `trabalho/Índice.md`
- Vitórias → `desempenho/Conquistas.md`
- Itens de ação → as notas de trabalho correspondentes

**Esta pasta é área de passagem, não de armazenamento.** Depois que uma nota é processada, o `/om-intake` pergunta se pode apagar a exportação bruta.

## Convenção de Nomes

Jogue os arquivos como saem da sua ferramenta de exportação. Prefixo sugerido, para clareza:

```
AAAA-MM-DD <Tema ou Pessoa>.md
```
