---
date:
description: "Fluxos e comandos de barra próprios deste vault — padrões reutilizáveis para preparar avaliações, acompanhar projetos e manter o vault"
tags:
  - brain
  - index
aliases:
  - Habilidades
  - Skills
---

# Habilidades

Comandos de barra, subagentes e fluxos reutilizáveis. Comandos `/om-*` definidos em `.claude/commands/` e `.claude/agents/`. **Esta nota é o catálogo canônico de comandos** para agentes que não recebem a injeção de skills em sessão (Codex, Gemini, Cursor) — mantenha-a atualizada quando os comandos mudarem; o CLAUDE.md deliberadamente não traz tabela de comandos.

**Idioma**: toda saída de comando/skill (relatórios, resumos, cabeçalhos de seção) deve vir em português, mesmo quando o template do comando está escrito em inglês. Regra completa em `CLAUDE.md` → "Response Language".

## Templates

| Template | Para que serve |
|----------|----------------|
| `Nota de Trabalho` | Nota padrão de projeto ativo |
| `Registro de Decisão` | Decisão de arquitetura/fluxo, com contexto e alternativas consideradas |
| `Nota de Reflexão` | Reflexão livre, pensamento em processo |
| `Nota de Competência` | Competência/habilidade demonstrada, com evidência |
| `Modelo de Review` | Estrutura de autoavaliação ou avaliação de par |
| `Briefing de Site` | Exemplo de template de domínio específico — adapte ou remova conforme seu contexto |

## Comandos de Barra

### Rotina Diária

| Comando | Para que serve |
|---------|----------------|
| `/om-standup` | Abertura do dia — carrega contexto, revisa ontem, levanta tarefas, identifica prioridades |
| `/om-dump` | Captura livre — despeje qualquer coisa, o roteamento para as notas certas é automático |
| `/om-wrap-up` | Revisão completa da sessão — verifica notas, índices e links, sugere melhorias. Disparado automaticamente ao dizer "wrap up". |

### Edição e Síntese

| Comando | Para que serve |
|---------|----------------|
| `/om-humanize` | Edição calibrada pela sua voz — faz o texto rascunhado pelo Claude soar como se você tivesse escrito |
| `/om-weekly` | Síntese semanal — padrões entre sessões, alinhamento com o Norte, vitórias não registradas |

### Preparação e Captura de Reuniões

| Comando | Para que serve |
|---------|----------------|
| `/om-prep-1on1` | Prepara um 1:1 que vem aí — carrega contexto da pessoa, pendências, vitórias a compartilhar e pauta sugerida |
| `/om-capture-1on1` | Transforma a transcrição de um 1:1 em nota estruturada, com citações, itens de ação e contexto de DM |
| `/om-capturar-acoes` | Transforma a transcrição de qualquer reunião em diagnóstico + ações escritas em texto corrido, sem linguagem de IA, com gate de aprovação antes de criar tarefa no seu gerenciador ou atualizar o vault |
| `/om-incident-capture` | Captura um incidente a partir de canais/DMs do Slack em notas estruturadas — linha do tempo, pessoas, análise, entrada de conquista |
| `/om-slack-scan` | Varredura profunda de canais/DMs do Slack em busca de evidência — extrai pontos de contato com data e organiza por contexto |
| `/om-meeting` | Prepara qualquer reunião por tema — briefing focado no assunto, com pendências, bloqueios e pontos levantados |
| `/om-intake` | Processa a caixa de entrada de reuniões — classifica as exportações brutas em `trabalho/reunioes/` e roteia para as notas certas |

### Desempenho e Avaliação

| Comando | Para que serve |
|---------|----------------|
| `/om-peer-scan` | Varredura profunda dos PRs de um colega no GitHub para preparar avaliação — gera análise estruturada em `desempenho/evidencias/` |
| `/om-review-brief` | Gera o briefing de avaliação (versão para gestor ou para pares) a partir dos dados do vault |
| `/om-self-review` | Escreve a autoavaliação para a ferramenta de avaliação — projetos, competências, princípios |
| `/om-review-peer` | Escreve a avaliação de um par — projetos, princípios, resumo de desempenho |

### Manutenção do Vault

| Comando | Para que serve |
|---------|----------------|
| `/om-vault-audit` | Auditoria estrutural profunda — índices, frontmatter, links, Bases, posicionamento de pastas, contexto obsoleto |
| `/om-vault-upgrade` | Importa conteúdo de um vault existente — detecta versão, classifica notas, transforma frontmatter, reconstrói índices |
| `/om-project-archive` | Move um projeto concluído de `trabalho/ativos/` para `trabalho/arquivo/AAAA/` e atualiza todos os índices — leva clusters `ativos/<Tema>/` inteiros, sem quebrar |
| `/om-tidy` | Passe de automanutenção — age sobre cada sinal de higiene: arquiva o que terminou, agrupa clusters, divide notas grandes demais, reporta pendências. Nunca apaga, nunca faz commit |

## Notas de Uso

**Diário:**
- `/om-standup` substitui a abertura manual de sessão — lê o Norte, o trabalho ativo, as tarefas, o log do git
- `/om-dump` processa texto livre e roteia cada pedaço para o tipo de nota e a pasta corretos
- `/om-wrap-up` dispara sozinho quando você diz "wrap up" — roda a revisão completa da sessão

**Edição e Síntese:**
- `/om-humanize` se calibra pelas suas amostras reais de escrita, não por uma lista negra de palavras. Detecta o contexto pelo frontmatter (avaliação → corporativo e assertivo, incidente → preciso, 1:1 → conversacional). Rode depois de rascunhar qualquer nota, para soar humano.
- `/om-weekly` liga o standup ao briefing de avaliação — rode no fim da semana para ver padrões entre sessões, desvio em relação ao Norte e vitórias não registradas. A saída é transitória por padrão; ele oferece promover os achados ao registro de conquistas ou ao Norte.

**Captura:**
- `/om-capture-1on1` aceita transcrições, notas cruas ou resumos
- `/om-capturar-acoes` foca só na escrita das ações (parágrafo único, sem rótulos, travessão como conector), não na nota de reunião inteira; complementa `/om-humanize` (que calibra a voz de uma nota já escrita) em vez de substituí-lo
- `/om-incident-capture` recebe URLs do Slack e produz documentação estruturada do incidente
- `/om-slack-scan` deve rodar DEPOIS do `/om-peer-scan`, para acrescentar contexto além do código (liderança, comunicação, evidência de colaboração)

**Desempenho:**
- `/om-peer-scan` rende mais quando disparado como agentes paralelos (um por pessoa)
- `/om-review-brief` exige que o briefing privado já exista — é dele que saem as versões filtradas

**Manutenção:**
- `/om-vault-audit` vale ao fim de sessões longas — pega índices desatualizados e contexto misturado
- `/om-vault-upgrade` importa conteúdo de um vault existente (obsidian-mind antigo ou qualquer vault Obsidian). Detecta versão, classifica notas, transforma frontmatter, conserta wikilinks, reconstrói índices. Use `--dry-run` para pré-visualizar.
- `/om-project-archive` cuida da mudança de `ativos/` para `arquivo/` junto com a atualização dos índices

## Subagents

| Agente | Para que serve | Invocado por |
|--------|----------------|--------------|
| `brag-spotter` | Encontra proativamente vitórias não registradas e lacunas de competência | `/om-wrap-up`, `/om-weekly` |
| `context-loader` | Carrega todo o contexto do vault sobre uma pessoa, projeto, incidente ou conceito | Direto — "carregue o contexto sobre X" |
| `cross-linker` | Acha wikilinks faltando, notas órfãs e backlinks quebrados no vault inteiro | `/om-vault-audit` |
| `people-profiler` | Cria/atualiza notas de pessoas em lote, a partir dos perfis do Slack | `/om-incident-capture` |
| `review-prep` | Agrega toda a evidência de desempenho de um dado período de avaliação | `/om-review-brief` |
| `slack-archaeologist` | Reconstrução completa do Slack — lê cada mensagem, thread e perfil, e produz uma linha do tempo unificada | `/om-incident-capture` |
| `vault-librarian` | Manutenção profunda do vault — detecção de órfãs, links quebrados, validação de frontmatter, notas obsoletas | `/om-vault-audit` |
| `review-fact-checker` | Confere cada afirmação de um rascunho de avaliação contra as fontes no vault | `/om-self-review`, `/om-review-peer` |
| `vault-migrator` | Classifica, transforma e migra conteúdo vindo de um vault de origem | `/om-vault-upgrade` |

Os subagentes rodam em janelas de contexto isoladas, via `.claude/agents/`. Eles não poluem a conversa principal.

## Hooks

| Hook | Quando | O que faz |
|------|--------|-----------|
| SessionStart | Na abertura/retomada | Reindexa o QMD, injeta o Norte, trabalho ativo, mudanças recentes, tarefas e listagem de arquivos |
| UserPromptSubmit | A cada mensagem | Classifica o conteúdo (decisão, incidente, 1:1, vitória, arquitetura, pessoa, atualização de projeto) e injeta dicas de roteamento |
| PostToolUse | Depois de escrever `.md` | Valida o frontmatter e confere os wikilinks |
| PreCompact | Antes da compactação de contexto | Faz backup da transcrição da sessão em `rascunhos/session-logs/` |
| Stop | Fim da sessão | Checklist: arquivar, atualizar índices, conferir órfãs |

## Busca Semântica (QMD)

Se o QMD estiver instalado (`npm install -g @tobilu/qmd`), o vault ganha busca semântica. Todo comando aceita `--index <nome>`, onde `<nome>` é o campo `qmd_index` do `vault-manifest.json` quando preenchido e, caso contrário, o nome da pasta do vault em formato slug:

- `qmd --index <nome> query "..."` — híbrido BM25 + vetor + reranking por LLM (melhor qualidade)
- `qmd --index <nome> search "..."` — busca rápida por palavra-chave (BM25)
- `qmd --index <nome> vsearch "..."` — busca vetorial semântica (exploratória)
- `qmd --index <nome> update && qmd --index <nome> embed` — atualiza o índice depois de mudanças em massa

O hook SessionStart roda `qmd --index <nome> update` sozinho, lendo o nome do índice a partir do manifest. Configuração inicial em um clone novo: `node --experimental-strip-types .scripts/qmd-bootstrap.ts`. Referência completa em `.claude/skills/qmd/SKILL.md`, e veja [[Memórias]] para os temas que o QMD mais costuma procurar no vault.

## O servidor MCP `om` (alcançar este vault de outro repositório)

O `.claude/scripts/om-mcp.mjs` expõe este vault por MCP, para que uma sessão em **outro repositório** consiga usá-lo. Ele é registrado no `.mcp.json` do projeto *consumidor*, nunca no do próprio vault — o servidor recusa gravar memória vinda de uma sessão que roda dentro do vault, porque essa memória ficaria no escopo do vault-como-projeto e só alcançaria sessões que já leem cada nota diretamente.

| ferramenta | para que serve |
|------------|----------------|
| `search` | busca semântica + por palavra-chave nas notas que este vault serve |
| `expand` | os links de saída e os backlinks de uma nota |
| `recall` | lições duradouras no escopo do repositório que chamou, da mais específica para a mais geral; `explain: true` informa o que foi omitido e por quê |
| `remember` | registra uma lição que generaliza para além deste repositório |
| `record_work` | registra o que aconteceu aqui, arquivado onde é o lugar |
| `reason` | julgamento cruzando várias notas, lendo o vault com uma segunda sessão do Claude |
| `health` | onde as memórias vivem, quais raízes estão expostas, se o índice está acessível |

Dois prompts que você mesmo invoca pelo menu `/`: `recall_topic` e `prior_art`. Eles precisam ser **selecionados** no menu — digitar o rótulo exibido dá erro.

**O `reason` é o lento.** Os outros respondem sem inferência; esse abre uma sessão, então leva de segundos a minutos. Recorra a ele quando `search` ou `recall` trouxeram as notas mas não a resposta. Roda no modelo padrão do seu CLI, a menos que `reason.model` fixe outro. As respostas ficam em `.claude/om-reasoning/`, marcadas como `confidence: inferred`, e nunca viram memória automaticamente.

**Como depurar:** chame `health` primeiro. Toda falha nessa camada aparece igual, como "nenhum resultado" — e é o `health` que distingue uma causa da outra.

Configuração completa, quais notas o servidor serve e o trecho necessário do lado do repositório: `CLAUDE.md` § *Reaching the Vault From Another Repo*. Como a camada inteira funciona: `ARCHITECTURE.md` § *Reaching the Vault From Another Repo*.

## Fluxo: Revisão Semanal

1. **`/om-weekly`** — sintetiza a atividade da semana, confere alinhamento, acha padrões
2. Promova ao registro de conquistas qualquer vitória não capturada
3. Atualize o Norte se o foco mudou
4. **`/om-wrap-up`** — encerra a sessão limpa

## Fluxo: Preparação do Ciclo de Avaliação

1. **`/om-review-brief manager`** — gera o documento de transferência de contexto para o gestor
2. **`/om-review-brief peers`** — gera o documento de transferência de contexto para os pares
3. **`/om-peer-scan`** (em paralelo, um por par) — varre a fundo os PRs de cada par
4. **`/om-slack-scan`** — varre os canais relevantes atrás da sua própria evidência e do contexto dos pares
5. **`/om-capture-1on1`** — captura o 1:1 de avaliação com seu gestor
6. **`/om-vault-audit`** — organiza tudo depois da enxurrada de dados novos

## Fluxo: Entrada em Projeto

1. **`/om-slack-scan`** — varre os canais do projeto atrás de histórico e decisões
2. **`/om-peer-scan`** (se necessário) — entende o que os colegas já construíram
3. Cria a nota de trabalho a partir do contexto reunido
4. **`/om-vault-audit`** — garante que tudo esteja linkado corretamente
