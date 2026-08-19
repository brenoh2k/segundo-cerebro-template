---
description: "Transforma uma transcrição de reunião (cliente, projeto ou 1:1) em diagnóstico + ações claras, escritas em texto corrido, sem linguagem de IA — pronto pra virar tarefa no seu gerenciador ou entrada no vault."
---

# Capturar Ações de Reunião

Pega uma transcrição crua (Gemini, nota manual, ata) e produz uma proposta de **diagnóstico + ações**: parágrafo único por ação, direto, sem rótulos, sem cara de texto gerado por IA.

Esta skill NÃO decide nem cadastra nada sozinha — ela escreve a proposta e espera aprovação. Depois de aprovada, os textos aprovados são usados para criar a tarefa no seu gerenciador de projetos (se houver conector e lista de destino) e/ou para atualizar a nota certa no vault (`trabalho/ativos/<Projeto>.md`, ou o equivalente de domínio específico que você tiver criado).

## Usage

```
/om-capturar-acoes <cliente/projeto ou contexto>
```

Cole a transcrição/notas em seguida. Exemplo: `/om-capturar-acoes Projeto Alfa`

## Workflow

### 1. Consolidar o insumo

Ler a transcrição e extrair — não copiar a transcrição inteira — os pontos que geram ação: problemas relatados, decisões tomadas na própria reunião, números que sustentam o diagnóstico (métricas, prazos, quem ficou responsável por quê).

Se já existir uma nota do projeto/pessoa no vault (`equipe/pessoas/<Pessoa>.md`, `trabalho/ativos/<Projeto>.md`), ler antes para não repetir contexto que já está registrado e para saber se alguma ação já apareceu numa reunião anterior.

### 2. Escrever a proposta

Para cada ação, escrever um único parágrafo que explica o que fazer, por que (a partir de qual achado da reunião) e qual é o critério de pronto — tudo junto, em prosa, não em lista de rótulos como "O quê / Passos / Pronto quando". Ver o Guia de Estilo abaixo antes de escrever a primeira linha.

Apresentar a proposta assim:

```
## Diagnóstico
{2-4 frases descrevendo o que a reunião revelou, com os números que sustentam}

## Ações propostas
1. **{Verbo + objeto} — {Cargo/responsável}**
   {parágrafo único, direto, sem rótulos}
2. ...

## Destino
- Gerenciador de tarefas: {lista/tarefa-mãe, se aplicável}
- Vault: {qual nota vai ser atualizada}
```

### 3. Aguardar aprovação

Nunca criar task ou editar nota antes do usuário responder. Resposta possível: aprovar (segue exatamente o proposto), ajustar (reescrever o trecho apontado), ou cancelar.

### 4. Efetivar

Só depois da aprovação: criar as tarefas no seu gerenciador (seguindo as regras de campo da lista de destino, se houver) e/ou atualizar a nota do vault com as mesmas ações, no mesmo texto aprovado — não reescrever de novo nesse passo.

## Guia de Estilo (obrigatório em toda ação escrita por esta skill)

**Faça:**
- Um parágrafo corrido por ação — sem cabeçalhos, sem "Passos:", sem "Pronto quando:" como rótulo. O critério de pronto entra na própria frase.
- Frases diretas: "implementar X para resolver Y" em vez de "seria interessante considerar a implementação de X".
- Travessão para encadear uma ideia complementar dentro da frase — é o conector natural do português, use-o quando ajudar a leitura (ex.: "a segmentação já mudou para manual em SP — mas as campanhas seguem paradas por falta de verba").
- Números e evidência da própria reunião, não generalização vaga ("205 contatos geraram 9 agendamentos em julho", não "os resultados ficaram abaixo do esperado").

**Não faça (linguagem de IA a evitar):**
- Vocabulário inflado: "notavelmente", "significativamente", "demonstra", "viabiliza", "evidencia".
- Frases de enchimento: "é importante notar que...", "vale ressaltar que...", "cabe destacar...".
- Empilhamento de ressalva: "potencialmente", "possivelmente poderia", "de certa forma".
- Transições vazias: "dessa forma", "nesse sentido", "em suma".
- Voz passiva onde a ativa é mais natural: "foi identificado que" → "identificamos" / "a reunião identificou".
- Parecer lista de checklist de curso: cada ação não deve começar com o mesmo padrão de frase.

**Exemplo de antes/depois:**

> ❌ Antes: "O quê: implementar o CRM. Passos: (1) confirmar dados; (2) preencher formulário; (3) confirmar cronograma. Pronto quando: formulário enviado."
>
> ✅ Depois: "O diagnóstico da reunião aponta leads se perdendo por falta de CRM. Confirmar que o cliente enviou os dados cadastrais necessários, preencher o formulário de acionamento do time comercial para a implantação, e confirmar com o responsável o cronograma e o treinamento da equipe."

## Important

- Não confundir com `/om-humanize` — aquele calibra a voz de uma nota inteira já escrita; esta skill nasce já escrevendo no estilo certo, a partir de uma transcrição crua, focada em ação (não em nota de reunião completa — para isso use `/om-capture-1on1`, `/om-intake` ou `/om-dump`).
- Se seu processo tiver um sistema formal de plano de ação com regras próprias de campo/lista, esta skill prepara o texto mas o cadastro segue as regras daquele sistema — não duplicar o trabalho de diagnóstico, só herdar o padrão de escrita.
- Sensível/pessoal (saúde, conflito, avaliação de desempenho) segue as mesmas regras de qualquer nota do vault — sinalizar, não expor em local errado.
