---
name: egreen-funil
description: >-
  Use quando o usuário mencionar funil de vendas, low ticket, infoproduto, tripwire,
  order bump, upsell, OTO, landing page de vendas, copy de anúncio, sequência de email
  para venda, lead magnet, value stack, conversão de produto digital, ou pedir para
  criar/avaliar/estruturar qualquer funil de produto digital. Também dispara com pricing
  de produto, estruturar oferta, aumentar ticket médio ou escalar vendas de produto digital.
  Baseado em Russell Brunson (Value Ladder + Tripwire), Alex Hormozi (Grand Slam Offer)
  e Iman Gadzhi (Commitment Escalation).
allowed-tools: Read, WebSearch
model: sonnet
---

# Funil Low Ticket — Estratégia Completa

## Passo 0. Carregar contexto do projeto

Antes de qualquer recomendação, leia:

- `memoria/egreen-produto.md` — produto ativo, ticket, posicionamento, público
- `memoria/egreen-nicho.md` — nicho, avatar, dores, concorrentes

Use esses dados para personalizar as recomendações. Se os arquivos estiverem ausentes
ou com `status: vazio`, aplicar o framework genericamente e avisar o usuário.

---

## Princípios Fundamentais dos 3 Modelos

### Russell Brunson — Value Ladder & Tripwire
**Princípio central:** "O objetivo do front-end não é lucrar. É pagar pelo tráfego. O lucro real vem dos upsells e do backend."

- Front-end (tripwire R$0–37): transforma visitante em comprador — não importa o lucro
- Uma compra muda a relação psicológica: probabilidade de recompra sobe 60–80%
- Order bump no checkout: 20–35% de aceitação sem nova página
- OTO 1 na thank-you page: 15–25% de aceitação (pessoa está no pico do "modo comprador")
- OTO 2 / Downsell: recupera indecisos do OTO 1

### Alex Hormozi — Grand Slam Offer
**Princípio central:** "Faça a oferta tão boa que as pessoas se sintam burras recusando."

**Equação de valor:**
```
Valor percebido = (Resultado desejado × Probabilidade de realização)
                  ÷ (Tempo até o resultado × Esforço e sacrifício)
```

- Lead magnet: solução COMPLETA para problema estreito (não fragmento)
- Value stack: produto + 3 bônus que removem objeções específicas + valor declarado em cada item
- Cada bônus deve remover uma objeção real de compra
- Return path: membership R$27–47/mês para LTV recorrente

### Iman Gadzhi — Commitment Escalation
**Princípio central:** "Leads gratuitos se comportam como leads gratuitos."

- Entry offer paga (R$67–147): filtra intenção, qualidade sobre quantidade
- Downsell (R$47–97): para quem recusou a entrada — mantém no ecossistema
- VSL pós-compra: reframe psicológico, não agradecimento
- Comunidade como qualificador: engajamento = proxy de probabilidade de compra futura

---

## Análise Comparativa

| Dimensão | Brunson | Hormozi | Gadzhi |
|---|---|---|---|
| Entrada | Tripwire R$0–37 (zero custo) | Lead magnet grátis | Entry offer paga R$67–147 |
| Filosofia | Front-end paga o tráfego | Oferta irrecusável | Preço filtra qualidade |
| Motor | Upsell sequencial | Stack de bônus | Comprometimento progressivo |
| Velocidade caixa | Alta — volume alto | Média | Média — volume menor |
| Dificuldade iniciante | Baixa | Média (copy forte) | Média-alta (VSL) |

---

## Funil Híbrido Recomendado para Iniciantes

Combina o melhor dos 3 sem exigir escala prévia. Executável na semana 1.

```
[Anúncio] → [Lead Magnet grátis] → [Landing Page] → [Core Offer R$47]
                                                           ↓
                                                    [Order Bump R$27]
                                                           ↓
                                                    [OTO 1 — R$97]
                                                           ↓
                                                    [Downsell R$47]
                                                           ↓
                                              [Sequência email 30 dias]
                                                           ↓
                                                  [Membership R$27/mês]
```

### As 8 Etapas do Funil Híbrido

**1. Lead Magnet (Brunson base)**
- PDF de 1 página resolvendo dúvida urgente e específica do avatar
- Entregue automaticamente via email (Brevo, ActiveCampaign, etc.)
- Objetivo: construir lista + qualificar intenção

**2. Core Offer R$47 (Hormozi stack)**
- Produto principal + 3 bônus com valores declarados
- Value stack visual: mostrar R$300+ de valor por R$47
- Bônus devem remover as 3 objeções principais do avatar

**3. Order Bump R$27 (Brunson tática)**
- Checkbox no checkout antes de confirmar pagamento
- Resolve o "próximo problema" após usar o produto principal
- Meta: 20–30% de aceitação

**4. OTO 1 — R$97 (Brunson OTO)**
- Thank-you page imediata após compra
- Versão "feita com você" ou aprofundamento do core
- Meta: 15–20% de aceitação

**5. Downsell R$47 (Gadzhi tática)**
- Para quem recusou OTO: versão menor, mesmo valor percebido
- Recupera ~30% das recusas

**6. Sequência pré-compra (emails E-01 a E-07)**
- Para leads que não compraram na landing page
- 7 emails em 10 dias: história → prova → oferta → urgência
- Meta: 4–12% de conversão dos leads
- Detalhes completos → leia `.claude/skills/egreen-funil-low/references/email-sequences.md`

**7. Pós-compra 30 dias (Hormozi return path)**
- P-01 a P-06: onboarding → vitória rápida → upsell membership
- Membership R$27/mês como LTV recorrente
- Detalhes completos → leia `.claude/skills/egreen-funil-low/references/email-sequences.md`

**8. Retargeting (Brunson backend)**
- Pixel rastreia visitantes que não compraram
- Anúncio específico com social proof + urgência
- Setup completo → leia `.claude/skills/egreen-funil-low/references/traffic-setup.md`

---

## Framework de Copy — Hook · Story · Offer

Todo anúncio, email e página segue esta estrutura:

**HOOK (3 segundos)**
- Para o scroll com dor específica ou curiosidade irresistível
- Fórmula: [Quem] + [Resultado] + [Tempo] + [Sem objeção principal]
- Exemplo: "Para mulheres 42–55 anos: durma 7 horas seguidas em 21 dias — sem hormônios ou remédios"

**STORY (15–30 segundos)**
- Jornada identificável — começa no pior momento emocional
- Cria ponte de empatia antes de apresentar solução

**OFFER (CTA direto)**
- Empilha valor declarado, revela preço como surpresa positiva
- Copy do botão: descreve resultado, não ação ("Sim, quero dormir melhor" > "Comprar")
- Nunca pede desculpas pelo preço

---

## Estrutura da Landing Page (6 Seções)

Para estrutura detalhada de cada seção, leia `.claude/skills/egreen-funil-low/references/egreen-landing-page.md`.

Ordem obrigatória:
1. **S1 — Above the fold**: headline curiosidade + CTA + sem menu
2. **S2 — Prova social**: números reais + depoimentos com disclaimer
3. **S3 — Problema**: emoção primeiro (Brunson), primeira pessoa do avatar
4. **S4 — Mecanismo**: lógica, nova categoria, por que outros falham
5. **S5 — Value stack**: tabela visual com valores declarados (Hormozi)
6. **S6 — CTA + garantia 30 dias + checkout embed**

**VSL:** opcional fase 1 (sem depoimentos). Entra na fase 2 com primeiro depoimento real.

---

## Roadmap de Escala — 3 Meses

Para roadmap completo semana a semana, leia `.claude/skills/egreen-funil-low/references/roadmap.md`.

**Mês 1 — Validação**
- Meta Ads exclusivo, estrutura 1-1-1, R$150–250/dia
- 1 criativo UGC amador, Advantage+ audience
- Aguardar 7–10 dias antes de qualquer julgamento
- Gate para avançar: ROAS ≥ 1.0, mínimo 1 venda

**Mês 2 — Otimização**
- Expandir para 1-1-5 (5 ângulos diferentes)
- Ativar retargeting separado (20% do budget)
- Escalar +20–30%/semana nos vencedores (ROAS ≥ 1.5)
- Fortalecer sequência email E-03/E-05

**Mês 3 — Escala**
- Escalar vencedores, testar TikTok com budget fixo separado
- Ativar membership e estruturar high ticket R$997–1497
- Gate de ciclo: ROI ≥ 200%, compradores ≥ 300, iniciar produto 2

---

## Regras de Ouro (Não Violar)

1. **Front-end não precisa lucrar** — precisa pagar o tráfego
2. **Order bump vale mais que OTO** — mais fácil, converte 2x mais
3. **Não escalar com ROAS < 1.5** — perde dinheiro em escala
4. **Não mexer antes de 7 dias** — pixel precisa aprender
5. **Mês 1 é para coletar dados** — pixel precisa de 50 conversões para otimizar
6. **E-03 é o email mais importante** — revisar primeiro se open rate cair
7. **Vitória rápida no produto** — reduz chargeback, aumenta LTV
8. **Bônus remove objeção** — não é complemento genérico
9. **Cada bônus tem valor declarado** — torna preço irrecusável
10. **Depoimento específico converte** — "passei a dormir 7h" > "adorei o produto"

---

## Quando Carregar Referências

- Estrutura detalhada da landing page → `.claude/skills/egreen-funil-low/references/egreen-landing-page.md`
- Roadmap semana a semana → `.claude/skills/egreen-funil-low/references/roadmap.md`
- Sequências de email completas → `.claude/skills/egreen-funil-low/references/email-sequences.md`
- Setup de tráfego Meta Ads → `.claude/skills/egreen-funil-low/references/traffic-setup.md`

Para configurar campanhas Meta Ads, use a skill `/egreen-meta-ads`.
