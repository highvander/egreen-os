---
name: egreen-vsl
description: >
  Escreve o roteiro completo de vídeo de venda longo — Webinar/live de lançamento ou VSL (Vídeo de Venda) gravada — não a copy de página de vendas nem anúncio curto. Usa dois frameworks amplamente reconhecidos no mercado de infoprodutos: o Perfect Webinar Script de Russell Brunson (história de origem, introdução do Vehicle, quebra de 3 crenças falsas, stack e fechamento) para webinar/live, e o framework PASTOR de Ray Edwards (Problem, Amplify, Story, Transformation, Offer, Response) para VSL gravada mais curta. Use esta skill sempre que o usuário pedir "roteiro de webinar", "script de VSL", "roteiro de vídeo de vendas", "live de lançamento", "roteiro pra gravar o vídeo de venda", ou pedir ajuda pra estruturar uma apresentação de venda longa em vídeo — mesmo sem citar Brunson, PASTOR ou Perfect Webinar. Para copy de página de vendas em texto use `egreen-copy`; para anúncio curto use `egreen-copywriting` ou `egreen-mandala`.
---

# Roteiro de VSL e Webinar (Brunson + PASTOR)

Esta skill escreve o **roteiro falado** de um vídeo de venda longo — não texto de página, não anúncio de 30 segundos. Dois formatos possíveis, com estruturas diferentes: **Webinar/live** (com ou sem interação real) e **VSL gravada** (sem interação, mais curta).

**Antes de escrever, leia `references/frameworks-roteiro.md`** — os dois frameworks detalhados abaixo vêm de lá.

---

## Passo 0 — Carregar memória do produto ativo

```
memoria/produto-ativo.md                    → pasta ativa
{pasta-ativa}/memoria/egreen-nicho.md              → avatar, dores, objeções
{pasta-ativa}/memoria/egreen-produto.md            → produto, preço, promessa
{pasta-ativa}/memoria/egreen-funil.md              → oferta, bônus, garantia
{pasta-ativa}/memoria/brand-voice.md        → voz de marca (se existir)
```

Se existir output de `egreen-concepcao` (Promessa, 5 Baldes) ou `egreen-copy` (Blocos aprovados, especialmente Depoimentos e Stack de Valor), reaproveite em vez de repetir intake — o roteiro reusa a mesma oferta, não cria uma nova.

---

## FASE 0 — Escolha de formato

Pergunte:
```
Qual formato de vídeo de venda?

1. Webinar/live de lançamento (60-90 min, pode ter Q&A) — Perfect Webinar Script
2. VSL gravada (10-25 min, sem interação) — framework PASTOR
```

Se o usuário já tiver produto de ticket alto e evento de lançamento planejado, sugira Webinar. Se for produto de ticket baixo/médio vendido de forma evergreen (sem data de lançamento), sugira VSL.

---

## ROTA A — Webinar/Live (Perfect Webinar Script)

Estruture nesta ordem, sem pular:

1. **História de origem** — como o apresentador descobriu o Vehicle, geralmente depois de tentar o "jeito velho" e falhar. Peça ao usuário uma história real; não invente biografia.
2. **Introduzir o Vehicle** — o método com nome próprio, em oposição ao "jeito velho" que o público já tentou (reaproveitar objeções mapeadas em `egreen-nicho.md`).
3. **Quebrar as 3 crenças falsas** — para cada uma, uma mini-história + prova:
   - Crença no Vehicle ("não funciona pra mim")
   - Crença interna ("não sou capaz")
   - Crença externa ("não tenho tempo/dinheiro/recurso")
4. **Stack e fechamento** — revelar oferta, empilhar valor item por item sem revelar preço antes do stack completo, revelar preço, bônus com urgência real (reaproveitar `egreen-funil.md`), fechar com objeções antecipadas.

Ao final de cada bloco, mostre ao usuário e pergunte se aprova antes de seguir pro próximo — roteiro de 60-90 minutos é longo demais pra revisar tudo de uma vez.

---

## ROTA B — VSL gravada (PASTOR)

Para cada letra, escreva o bloco correspondente:

- **P — Problem**: nomear o problema real (reaproveitar `egreen-nicho.md`), específico o suficiente pra reconhecimento imediato
- **A — Amplify**: custo de não resolver — o que a pessoa já perde continuando assim
- **S — Story/Solution**: história de descoberta do método (própria ou de terceiro)
- **T — Transformation/Testimony**: prova real com número e prazo — nunca inventar, sinalizar como placeholder se não houver depoimento real disponível
- **O — Offer**: a oferta específica, sem ambiguidade (reaproveitar `egreen-funil.md`)
- **R — Response**: chamada à ação com urgência real e instrução de próximo passo claro

Se o produto for de ticket alto (mentoria, curso completo 700+), considere incorporar a quebra de 1-2 crenças (lógica Brunson) dentro do bloco Story/Solution antes de seguir pra Transformation.

---

## Passo Final — Salvar output

```
{pasta-ativa}/egreen-vsl/{YYYY-MM-DD-descricao-curta}.md
```

Confirmação:
```
✅ Salvo em: {pasta-ativa}/egreen-vsl/{YYYY-MM-DD-descricao-curta}.md

Próximo passo: gravar/ensaiar o roteiro, ou revisar com /egreen-cro antes de subir tráfego pra ele
```

---

## Notas de estilo

- Roteiro é pra ser falado, não lido — frases mais curtas que copy de página, marcações de pausa/ênfase quando relevante.
- Nunca inventar depoimento, número de resultado ou prova que o usuário não forneceu — sinalizar como placeholder.
- Reaproveitar objeções reais já mapeadas em `egreen-nicho.md`/`egreen-pesquisa` na etapa de quebra de crença (Rota A) ou Amplify (Rota B), em vez de genéricas.
- Entregar em blocos claramente identificados (Bloco 1, 2, 3... ou P-A-S-T-O-R), prontos pra teleprompter. Se o usuário pedir arquivo específico, gerar no formato apropriado; caso contrário, entregue na conversa e salve o Markdown conforme o Passo Final.
