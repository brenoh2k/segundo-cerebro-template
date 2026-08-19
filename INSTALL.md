# Instalação — Segundo Cérebro

Este repositório é um vault Obsidian pronto para uso com Claude Code (e também Codex CLI / Gemini CLI), já com toda a estrutura, hooks, comandos e templates configurados. Ele **não tem nenhum dado pessoal** — só a arquitetura. Personalize conforme os passos abaixo.

## 1. Clonar o repositório

```bash
git clone https://github.com/brenoh2k/segundo-cerebro-template.git "Segundo Cerebro"
cd "Segundo Cerebro"
```

> Depois de clonar, você pode (e deve) renomear a pasta e ajustar o remote (`git remote set-url origin <seu-fork>`) se for manter seu próprio histórico separado deste.

## 2. Abrir como vault do Obsidian

1. Baixe o [Obsidian](https://obsidian.md) (1.12 ou mais recente).
2. **Open folder as vault** → selecione a pasta clonada.
3. Em **Settings → Community plugins**, habilite os plugins já listados em `.obsidian/community-plugins.json` (inclui `obsidian-local-rest-api`, usado pela CLI).
4. Em **Settings → General**, habilite o **Obsidian CLI** (requer Obsidian 1.12+).
5. O core plugin **Bases** já vem habilitado — as visões em `bases/*.base` (Painel de Trabalho, Tocados Recentemente, etc.) aparecem prontas.

## 3. Instalar o Node (necessário para os hooks)

Os hooks (`.claude/scripts/*.ts`) rodam TypeScript nativamente via Node, sem build step.

- [Node 22+ LTS](https://nodejs.org) (o flag `--experimental-strip-types` é estável a partir do 22.6)

Teste com:

```bash
node --experimental-strip-types --version
```

## 4. Instalar seu agente de IA

Escolha um (ou mais — os hooks funcionam nos três):

| Agente | Instalação |
|--------|-----------|
| **Claude Code** (suporte completo) | `npm install -g @anthropic-ai/claude-code` — veja [docs](https://docs.anthropic.com/en/docs/claude-code) |
| **Codex CLI** | Veja [github.com/openai/codex](https://github.com/openai/codex) |
| **Gemini CLI** | Veja [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) |

Rode o agente **dentro da pasta do vault**:

```bash
claude
```

Na primeira sessão, o hook `SessionStart` já injeta o contexto do vault automaticamente (arquivos, `Norte.md`, tarefas abertas).

## 5. (Recomendado) Instalar QMD para busca semântica

Sem isso o vault ainda funciona (cai para grep + Obsidian CLI), mas a busca fica bem melhor com ele:

```bash
npm install -g @tobilu/qmd
node --experimental-strip-types .scripts/qmd-bootstrap.ts
```

O bootstrap é idempotente — pode rodar de novo sem problema. Ele lê `vault-manifest.json` (`qmd_index`, `qmd_context`) e monta o índice/embeddings. Os três modelos que ele baixa (embedding, query-expansion, reranker) rodam localmente — sem chave de API, sem custo por consulta.

## 6. Personalizar o vault

Isso é o que transforma a estrutura genérica no *seu* segundo cérebro:

1. Abra `CLAUDE.md` e leia a seção **"Personalize Isto Primeiro"** no topo — ela te guia pelos ajustes.
2. Preencha `cerebro/Norte.md` com seus objetivos reais (curto/médio/longo prazo).
3. Se seu trabalho tem um conceito de "conta"/"cliente" que merece pasta própria (nem todo mundo tem), crie a pasta, o template em `modelos/`, e registre em `vault-manifest.json` → `user_content_roots`.
4. `desempenho/` (brag doc, competências, ciclo de avaliação) já vem ativo — é o fluxo original do template. Se não fizer sentido pro seu contexto, marque como dormente no `CLAUDE.md` (comentário, nunca apague os arquivos).
5. Rode `/om-standup` ou converse normalmente — o Claude vai começar a preencher `equipe/`, `trabalho/`, `cerebro/` conforme você usa.

## 7. (Opcional) Conectar o vault a outros repositórios via MCP

Se você também usa Claude Code em projetos de código e quer que eles consultem este vault (decisões, convenções, memórias), registre o servidor `om`:

```json
// .mcp.json do OUTRO projeto (nunca no próprio vault)
{
  "mcpServers": {
    "om": {
      "command": "node",
      "args": ["<caminho absoluto para este vault>/.claude/scripts/om-mcp.mjs"]
    }
  }
}
```

E adicione uma seção curta no `CLAUDE.md`/`AGENTS.md` daquele projeto avisando que o vault existe e deve ser consultado — os dois passos são necessários (detalhes em `CLAUDE.md` → "Reaching the Vault From Another Repo").

## Checklist rápido

- [ ] Clonei e abri como vault no Obsidian
- [ ] Community plugins habilitados
- [ ] Obsidian CLI habilitado
- [ ] Node 22+ instalado
- [ ] Agente de IA instalado e rodando dentro da pasta do vault
- [ ] QMD instalado e bootstrap rodado (opcional, mas recomendado)
- [ ] `cerebro/Norte.md` preenchido com meus objetivos
- [ ] Seção "Personalize Isto Primeiro" do `CLAUDE.md` revisada/ajustada

## Mais detalhes

- **`README.md`** — visão geral do template, exemplos, como funciona por baixo dos panos
- **`CLAUDE.md`** — manual operacional completo (estrutura, convenções de nota, linking, hooks) — é o que o agente lê a cada sessão
- **`ARCHITECTURE.md`** — como as peças se encaixam, para quem quiser customizar sem quebrar a mecânica
- **`cerebro/Habilidades.md`** — catálogo de comandos `/om-*` e subagentes
