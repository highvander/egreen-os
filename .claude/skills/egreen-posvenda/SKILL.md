---
name: egreen-posvenda
description: >
  Escreve a copy do momento da compra em diante — order bump, OTO/upsell no checkout, sequência de onboarding pós-compra, upsell/cross-sell posterior e pedido de depoimento — as etapas Convert-final, Excite, Ascend e Advocate da Customer Value Journey que `egreen-growth` planeja mas não escreve. Usa a Value Equation de Alex Hormozi (checkout/upsell), o princípio de "tempo até o primeiro valor" de Lincoln Murphy/Customer Success (onboarding) e o gatilho de reciprocidade de Robert Cialdini (pedido de depoimento no momento certo). Use esta skill sempre que o usuário pedir "copy de order bump", "texto da página de obrigado", "sequência de boas-vindas pós-compra", "como pedir depoimento", "copy de upsell", "onboarding do cliente que acabou de comprar" — mesmo sem citar os frameworks. Para e-mails de pré-venda (boas-vindas de lead, nutrição, lançamento) use `egreen-emails`; para a página de vendas principal use `egreen-copy`/`egreen-landing`.
---

# Pós-Venda: Checkout, Onboarding, Upsell, Depoimento

Esta skill escreve o conteúdo das etapas da jornada que vêm **depois da decisão de compra** — `egreen-emails` cobre a fase de pré-venda (lead → comprador); esta skill cobre comprador → cliente ativado → cliente que compra de novo → cliente que recomenda.

**Antes de escrever, leia `references/frameworks-posvenda.md`.**

---

## Passo 0 — Carregar memória do produto ativo

```
memoria/produto-ativo.md                    → pasta ativa
{pasta-ativa}/memoria/produto.md            → produto, preço
{pasta-ativa}/memoria/funil.md              → order bump/OTO/upsell já definidos, garantia
```

Se existir output de `egreen-growth` (`{pasta-ativa}/egreen-growth/`), reaproveite o mapa de Excite/Ascend/Advocate de lá em vez de perguntar do zero — esta skill escreve o conteúdo daquilo que `egreen-growth` já diagnosticou como lacuna nessas etapas.

---

## FASE 0 — Escolha do módulo

Pergunte qual módulo o usuário precisa (pode ser mais de um):
```
1. Order bump / OTO (copy do checkout)
2. Onboarding pós-compra (primeiros dias)
3. Upsell/cross-sell posterior
4. Pedido de depoimento
```

---

## MÓDULO 1 — Order bump / OTO

1. Confirme se já existe order bump/OTO definido em `funil.md`; se não, isso precisa ser resolvido em `egreen-funil` primeiro — esta skill escreve a copy, não desenha a oferta.
2. Aplique a Value Equation de Hormozi: identifique qual dos 4 fatores (resultado, probabilidade, tempo, esforço) essa oferta complementar melhora especificamente.
3. **Order bump**: uma frase de benefício + preço ancorado, sem reabrir objeção da oferta principal.
4. **OTO (thank-you page)**: mais espaço que o order bump, mas ainda curto — sem quebrar o "modo comprador" com página longa.

---

## MÓDULO 2 — Onboarding pós-compra (Excite)

1. Escreva a **confirmação imediata** (momento da compra, antes de qualquer e-mail formal).
2. Defina a **primeira ação única** que o cliente deve fazer nas primeiras 24-48h — uma ação, não uma lista de boas-vindas com tudo de uma vez.
3. Escreva a comunicação que entrega essa primeira ação de forma que gere sensação real de progresso rápido.
4. Escreva o **checkpoint de reforço** (dia 3-7) verificando se a primeira ação foi feita, com oferta de ajuda se não foi.

---

## MÓDULO 3 — Upsell/cross-sell (Ascend)

1. Confirme que o cliente já teve o primeiro resultado (Módulo 2) antes de recomendar enviar isso — nunca ofereça upgrade antes da primeira vitória confirmada.
2. Aplique a Value Equation: o upsell deve acelerar/ampliar o resultado que o cliente já sentiu, não vender algo não relacionado.
3. Escreva a copy no mesmo tom de `brand-voice.md` se existir.

---

## MÓDULO 4 — Pedido de depoimento (Advocate)

1. Pergunte ao usuário qual resultado específico e reconhecido o cliente teve (nunca gerar pedido genérico "conta o que achou").
2. Escreva o pedido seguindo a estrutura: reconhecer o resultado específico → pedir algo fácil e guiado (2-3 perguntas, não "escreva um depoimento") → oferecer forma fácil de responder (vídeo curto, print, áudio) → deixar claramente opcional.

---

## Passo Final — Salvar output

```
{pasta-ativa}/egreen-posvenda/{YYYY-MM-DD-descricao-curta}.md
```

Confirmação:
```
✅ Salvo em: {pasta-ativa}/egreen-posvenda/{YYYY-MM-DD-descricao-curta}.md

Próximo passo: {sugestão, ex: configurar automação de envio no canal escolhido, ou seguir pro próximo módulo}
```

---

## Notas de estilo

- Order bump/OTO deve ser sempre mais curto que o instinto do usuário pede — fricção no checkout é o erro mais comum aqui.
- Nunca condicionar suporte, acesso ou reembolso ao pedido de depoimento.
- Reaproveitar `brand-voice.md` em toda a copy gerada, se existir.
- Entregar em blocos claramente identificados por módulo. Se o usuário pedir arquivo específico, gerar no formato apropriado; caso contrário, entregue na conversa e salve o Markdown conforme o Passo Final.
