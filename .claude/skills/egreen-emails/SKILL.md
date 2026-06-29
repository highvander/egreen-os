---
name: egreen-emails
description: >-
  Use quando o usuário pedir sequência de emails, nutrição de lista, emails de lançamento,
  boas-vindas para leads, follow-up pós lead magnet, aquecimento de lista, copy de email,
  ou qualquer sequência de email marketing para infoproduto. Dispara com "emails de
  lançamento", "sequência de nutrição", "boas-vindas para lista", "email de venda",
  "sequência de aquecimento", "copy de email", "/egreen-emails".
allowed-tools: Read, Write, Edit, Glob, AskUserQuestion
model: sonnet
---

# Egreen Emails — Sequências de Email para Infoprodutos

Gera sequências de email completas e prontas para envio: copy real, subject lines, preview text, CTA e cadência. Toda sequência parte do contexto já salvo em `memoria/` — nenhuma pergunta repetida sobre nicho ou produto.

---

## Passo 0 — Carregar contexto do produto ativo

Antes de qualquer ação, leia **todos** os arquivos existentes:

```
memoria/produto-ativo.md          → pasta ativa (ex: produto-01)
{pasta-ativa}/memoria/nicho.md    → avatar, dores, linguagem, objeções
{pasta-ativa}/memoria/produto.md  → produto, preço, promessa, benefícios
{pasta-ativa}/memoria/funil.md    → lead magnet, funil, oferta, upsells
{pasta-ativa}/memoria/design.md      → identidade visual (se existir)
{pasta-ativa}/memoria/brand-voice.md → voz de marca: vocabulário, tom, do/don't, amostras (se existir)
```

Se `brand-voice.md` existir: use vocabulário autorizado, evite palavras proibidas, siga as dimensões de tom e o guia do/don't. As amostras de copy servem como âncora de estilo para subject lines e corpo dos emails.

Se `produto-ativo.md` não existir ou qualquer arquivo de memória tiver `status: vazio`:

> **PARE.** Execute `/egreen-setup` primeiro.

---

## Passo 1 — Coletar tipo de sequência

Pergunte **em uma única mensagem**:

```
Qual sequência você quer gerar?

1. Boas-vindas (5 emails, 8 dias) — pós download de lead magnet
2. Nutrição (6 emails, 18 dias) — leads que ainda não compraram
3. Lançamento (9 emails, 7 dias) — abertura de carrinho
4. Todas as três

→ Digite o número ou nome.
```

Se escolher **Lançamento** ou **Todas**, pergunte logo em seguida:

```
Qual é a data de abertura do carrinho? (ex: 15/07/2026)
```

---

## Passo 2 — Gerar sequências

Use os dados de `memoria/` para personalizar **cada email com copy real** — sem colchetes de placeholder. O leitor deve reconhecer o próprio nicho e dor específica em cada linha.

### Regra de ouro: uma mensagem, um trabalho

Cada email tem exatamente:
- **Um assunto central** (ideia ou história)
- **Uma ação desejada** (CTA)
- **Uma emoção principal** (curiosidade / confiança / urgência / esperança)

---

## Frameworks de Copy

### Framework 1 — Valor Antes do Pedido (3:1)

```
Email 1-2-3: Valor puro — ensina, surpreende, resolve (sem pedir nada)
Email 4:     Valor + caso de sucesso que menciona o produto naturalmente
Email 5+:    Pedido direto com reversão de risco
```

Proporção obrigatória: mínimo 3 emails de valor para cada 1 email de venda.

### Framework 2 — Narrativa Argumentativa

```
Gancho:  Abre com história, dado ou observação inesperada (2-3 frases)
Ponte:   Conecta ao problema real do leitor (1-2 frases)
Lição:   Entrega insight acionável completo — não fragmento (2-3 frases)
CTA:     Liga a lição ao próximo passo (1 frase + link)
```

Usar em emails de nutrição e para audiências sofisticadas.

### Framework 3 — PAS (Problema-Agitação-Solução)

```
Problema:  "Você ainda está [dor específica]?"
Agitação:  "Cada semana que passa, [consequência concreta]. Enquanto isso, [concorrente/mercado]..."
Solução:   "[Produto] resolve isso através de [mecanismo único]. Veja como..."
CTA:       "Entra agora e vê a diferença em [prazo real]."
```

Usar em emails de lançamento, D0 e fechamento de carrinho.

---

## Fórmulas de Subject Line

Gere **1 subject principal + 1 variação A/B** para cada email.

| Fórmula | Exemplo (adaptar ao nicho) | Melhor para |
|---------|---------------------------|-------------|
| Número + Benefício | "3 erros que travam sua copy" | Educacional |
| Lacuna de Curiosidade | "O que ninguém te contou sobre [nicho]" | Nutrição |
| Benefício Direto | "Seu [lead magnet] está aqui" | Boas-vindas |
| Pergunta Incômoda | "Você ainda comete esse erro?" | Conscientização |
| Como Fazer | "Como [resultado] sem [sacrifício]" | Educacional |
| Prova Social | "Por que [N] pessoas já fizeram isso" | Lançamento |
| Urgência Real | "Encerra hoje à meia-noite" | Fechamento |
| Padrão Quebrado | "Eu estava completamente errado" | Reengajamento |
| Negativo | "Pare de fazer isso no seu [nicho]" | Dor aguda |
| Confissão | "Me arrependo de não ter feito antes" | Emocional |

**Regras:**
- Máximo 45 caracteres (mobile-first)
- Palavra mais importante nos primeiros 30 caracteres
- Números ímpares > pares (3, 5, 7 convertem mais)
- Evitar: "grátis", "garantido", "clique aqui" em excesso (filtro de spam)
- Preview text (preheader) é obrigatório — complementa, não repete o subject

---

## Sequência 1 — Boas-vindas (5 emails, 8 dias)

Ativada após download do lead magnet. Objetivo: transformar lead frio em seguidor engajado e preparar para compra.

```
Email 1 — Imediato    ENTREGA + EXPECTATIVA
Email 2 — Dia 1       HISTÓRIA DE ORIGEM
Email 3 — Dia 3       CONTEÚDO EDUCATIVO GRATUITO
Email 4 — Dia 5       PROVA SOCIAL COM NÚMEROS
Email 5 — Dia 8       PITCH DIRETO + REVERSÃO DE RISCO
```

### Email 1 — Entrega + Expectativa
**Objetivo:** Entregar o prometido. Criar antecipação para próximos emails.
**Tom:** Próximo, direto, sem floreios.
**Corpo:**
- Linha 1: entrega o link/material (imediata)
- Parágrafo 1: explica o que vem nos próximos dias (brevemente)
- Parágrafo 2: faz uma pergunta de engajamento (aumenta deliverability)
- Sem pitch de produto

### Email 2 — História de Origem
**Objetivo:** Construir conexão emocional. Mostrar que o criador viveu a mesma dor do leitor.
**Tom:** Vulnerável, honesto, específico.
**Corpo:**
- Antes: situação difícil com detalhe concreto (não genérico)
- Virada: o que mudou / o que descobriu
- Depois: resultado real com número se possível
- Transição suave: "foi isso que me levou a criar [produto]" — apenas menciona, não vende

### Email 3 — Conteúdo Educativo Gratuito
**Objetivo:** Demonstrar expertise. Entregar valor sem pedir nada.
**Tom:** Professor generoso.
**Corpo (Framework Narrativa Argumentativa):**
- Insight surpreendente sobre o nicho (dado real ou observação contraintuitiva)
- Por que isso importa para o leitor agora
- 1 tática concreta que podem aplicar hoje — completa, não fragmento
- CTA: ler post / assistir vídeo / responder com dúvida (não comprar)

### Email 4 — Prova Social com Números
**Objetivo:** Mostrar que o método funciona para pessoas reais. Reduzir ceticismo.
**Tom:** Factual, específico, sem exagero.
**Corpo:**
- Mini-caso de sucesso: nome + situação antes + o que fez + resultado com número
- Insight extraído do caso (lição transferível)
- CTA suave: "se quiser o mesmo caminho, [produto] é o próximo passo"

### Email 5 — Pitch Direto + Reversão de Risco
**Objetivo:** Converter leads prontos. Eliminar última objeção.
**Tom:** Direto, confiante, sem desculpas pelo preço.
**Corpo (Framework PAS):**
- Recapitula a dor principal em 1 frase
- Apresenta o produto com clareza: o que é, o que entrega, para quem é
- Responde à objeção #1 do nicho (extraída de `nicho.md`)
- Reversão de risco: garantia, período de teste, política de reembolso
- CTA: link direto com urgência contextual (não artificial)

---

## Sequência 2 — Nutrição (6 emails, 18 dias)

Para leads que entraram na lista mas não compraram. Objetivo: manter autoridade, aprofundar dor, preparar para próxima oferta.

```
Email 1 — Dia 0    INSIGHT SURPREENDENTE
Email 2 — Dia 3    ERRO COMUM DO NICHO
Email 3 — Dia 6    A GRANDE MENTIRA DO MERCADO
Email 4 — Dia 10   CASO DE SUCESSO DETALHADO
Email 5 — Dia 14   RESPOSTA À OBJEÇÃO PRINCIPAL
Email 6 — Dia 18   OFERTA COM URGÊNCIA SUAVE
```

### Email 1 — Insight Surpreendente
**Objetivo:** Reativar atenção. Mostrar perspectiva nova.
**Tom:** Jornalista investigativo.
**Corpo:** Dado contraintuitivo do nicho + por que isso muda tudo + 1 ação imediata.

### Email 2 — Erro Comum
**Objetivo:** Criar conscientização de problema que o produto resolve.
**Tom:** Conselheiro honesto.
**Corpo:** Erro específico que 80% do nicho comete + consequência concreta + como corrigir (parcialmente — produto resolve o resto).

### Email 3 — A Grande Mentira
**Objetivo:** Quebrar crença limitante que impede a compra.
**Tom:** Provocador, baseado em evidência.
**Corpo:** "O mercado diz X. A realidade é Y. Prova: [evidência]." + O que fazer em vez disso.

### Email 4 — Caso de Sucesso Detalhado
**Objetivo:** Prova social + aspiração. Tornar o resultado concreto e alcançável.
**Tom:** Narrador.
**Corpo:** História de aluno/cliente com: situação antes → decisão → ações → resultado com número → o que aprendeu.

### Email 5 — Objeção Principal Respondida
**Objetivo:** Eliminar a barreira de compra #1 identificada em `nicho.md`.
**Tom:** Direto, sem rodeios.
**Corpo:** "Sei que muitos pensam [objeção exata]. Entendo. Mas aqui está o que a evidência mostra: [argumento]. É por isso que [produto] foi construído para [solução específica]."

### Email 6 — Oferta com Urgência Suave
**Objetivo:** Converter sem pressão excessiva. Dar motivo real para agir agora.
**Tom:** Parceiro que conhece a situação.
**Corpo:** Recapitula a jornada dos emails anteriores → apresenta o produto como próximo passo lógico → urgência contextual (bônus, preço, vagas) → CTA direto.

---

## Sequência 3 — Lançamento (9 emails, 7 dias)

Cronograma com data de abertura como D0. Todos os emails baseados na data informada no Passo 1.

```
D-2 manhã   Email 1 — TEASER
D-1 manhã   Email 2 — REVELAÇÃO
D-1 tarde   Email 3 — PROVA SOCIAL PRÉ-LANÇAMENTO
D0  manhã   Email 4 — CARRINHO ABERTO (email principal)
D0  tarde   Email 5 — FAQ + OBJEÇÕES
D+1 manhã   Email 6 — MOMENTUM SOCIAL
D+2 manhã   Email 7 — OBJEÇÃO PRINCIPAL RESPONDIDA
D+3 manhã   Email 8 — URGÊNCIA — ÚLTIMO DIA AMANHÃ
D+3 tarde   Email 9 — ÚLTIMO DIA — ENCERRA HOJE
```

### Email 1 — Teaser (D-2, manhã)
**Objetivo:** Criar curiosidade. Fazer o leitor aguardar.
**Tom:** Misterioso, sem revelar o produto.
**Corpo:** "Algo grande chega em 48 horas. Não posso contar tudo ainda, mas posso dizer que [resultado que o produto entrega] vai ser muito mais acessível a partir de [data]." CTA: "Fique de olho neste email."

### Email 2 — Revelação (D-1, manhã)
**Objetivo:** Apresentar o produto com clareza. Ancorar o valor antes do preço.
**Tom:** Entusiasmado, específico.
**Corpo:** Apresenta o produto completo — o que é, o que entrega, para quem é, o que inclui. Anuncia a data e hora de abertura. CTA: "Salva este email — o link abre amanhã às [hora]."

### Email 3 — Prova Social Pré-lançamento (D-1, tarde)
**Objetivo:** Reduzir ceticismo antes da abertura. Social proof antecipado.
**Tom:** Factual, inspirador.
**Corpo:** 2-3 resultados de beta testers ou alunos anteriores. Cada um com nome + situação + número. CTA: "Amanhã às [hora] você tem a mesma oportunidade."

### Email 4 — Carrinho Aberto (D0, manhã)
**Objetivo:** Converter. Este é o email mais importante da sequência.
**Tom:** Direto, confiante, urgente sem ser desesperado.
**Corpo (Framework PAS expandido):**
- Abertura: "Está aberto."
- Problema em 2 frases
- O produto como solução: o que é + o que inclui (lista de entregáveis + bônus + valor declarado de cada item)
- Prova: 1 resultado real com número
- Reversão de risco: garantia completa
- Urgência real: data/hora de encerramento
- CTA principal em destaque + CTA secundário ("tenho dúvidas" → FAQ link)

### Email 5 — FAQ + Objeções (D0, tarde)
**Objetivo:** Converter indecisos. Eliminar as 5 objeções mais comuns do nicho.
**Tom:** Paciente, honesto.
**Corpo:** "Recebi perguntas. Aqui estão as respostas:" → Q&A real com 5 objeções extraídas de `nicho.md`. CTA no final de cada resposta.

### Email 6 — Momentum Social (D+1, manhã)
**Objetivo:** Criar FOMO através de prova social real.
**Tom:** Animado, factual.
**Corpo:** "Ontem [X pessoas] entraram. Aqui está o que alguns estão dizendo:" → 3 reações reais (prints, mensagens, comentários). CTA: "Ainda dá tempo. Link abaixo."

### Email 7 — Objeção Principal (D+2, manhã)
**Objetivo:** Converter o segmento que está travado na objeção #1.
**Tom:** Empático, direto.
**Corpo:** Nomeia a objeção principal do nicho. Responde com evidência + história de quem tinha a mesma objeção e entrou mesmo assim + resultado. CTA: link direto.

### Email 8 — Urgência (D+3, manhã)
**Objetivo:** Ativar procrastinadores. Urgência real, não fabricada.
**Tom:** Sério, amigável.
**Corpo:** "Encerra amanhã à meia-noite." Recapitula o que está em jogo: o produto + bônus + garantia + preço. "Depois disso, [preço sobe / vagas fecham / bônus somem]." CTA urgente.

### Email 9 — Último Dia (D+3, tarde)
**Objetivo:** Última conversão. Curto e direto.
**Tom:** Urgente, sem enrolação.
**Corpo:** 5-7 linhas máximo. "Encerra em [X horas]. [Produto] + [bônus principal] + garantia de [X dias]. Link abaixo. Depois disso, acabou." CTA em destaque. Sem mais argumentação.

---

## Cadência Visual

| Sequência | D0 | D1 | D3 | D5 | D8 | D10 | D14 | D18 |
|-----------|----|----|----|----|-----|-----|-----|-----|
| Boas-vindas | E1 | E2 | E3 | E4 | E5 | — | — | — |
| Nutrição | E1 | — | E2 | — | E3 | E4 | E5 | E6 |

Para Lançamento: usar cronograma D-2 a D+3 acima com data real fornecida.

**Melhores horários de envio (Brasil):**
- Infoprodutos B2C: terça a quinta, 8h-10h ou 19h-21h (horário de Brasília)
- Evitar: segunda de manhã, sexta à tarde, finais de semana
- Emails de urgência (D+3): enviar entre 10h e 14h para maximizar abertura antes de dormir

---

## Compliance LGPD

Incluir em **todo** output gerado:

- **Link de descadastro** obrigatório em cada email (texto: "Cancelar inscrição" ou "Sair da lista")
- **Identificação clara do remetente**: nome + email do responsável
- **Nunca usar listas compradas** — apenas opt-in confirmado
- **Duplo opt-in recomendado** (email de confirmação antes de entrar na sequência)
- **Armazenar registro de consentimento**: data, origem, IP quando possível
- **Prazo de atendimento a pedidos de remoção**: até 15 dias (Art. 18 LGPD)

> Nota: Verificar conformidade específica com advogado ou DPO. Estas diretrizes são orientação geral.

---

## Formato de Output

Para cada email da sequência, entregar:

```
### Email [N] — [Nome]
**Envio:** [Timing / Data calculada]
**Assunto:** [Subject principal]
**Assunto B (A/B):** [Variação]
**Preview text:** [Preheader — max 90 chars]

---

[Corpo completo do email — copy real, pronto para enviar]

---

**CTA:** [Texto exato do botão/link]
**Objetivo:** [O que este email deve fazer]
```

---

## Encerramento da Skill

Após gerar e aprovar as sequências:

1. Salvar cada sequência em arquivo separado:
   - `{pasta-ativa}/egreen-emails/YYYY-MM-DD-boas-vindas.md`
   - `{pasta-ativa}/egreen-emails/YYYY-MM-DD-nutricao.md`
   - `{pasta-ativa}/egreen-emails/YYYY-MM-DD-lancamento.md`

2. Exibir confirmação:

```
✅ Salvo em: {pasta-ativa}/egreen-emails/

Próximo passo: /egreen-meta-ads para subir campanha de tráfego
               /egreen-mandala para criar anúncios que alimentam esta lista
```
