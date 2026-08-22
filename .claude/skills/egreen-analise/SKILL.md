---
name: egreen-analise
description: >-
  Use quando o usuário quiser analisar performance do infoproduto em campanha: ROAS,
  CPL, CPA, taxa de conversão do funil, métricas de email, diagnóstico de onde o funil
  está vazando, ou decidir se escala, otimiza ou pausa campanha. Dispara com "analisar
  resultados", "como está minha campanha", "meu ROAS", "taxa de conversão", "relatório
  de performance", "onde está vazando", "/egreen-analise".
allowed-tools: Read, Write, Edit, Glob, AskUserQuestion
model: sonnet
---

# Egreen Analise — Performance do Funil de Infoproduto

Analisa os números reais do funil em campanha: tráfego, captação, conversão, email e financeiro. Detecta onde está vazando, calcula score de saúde do negócio e entrega plano de ação priorizado. Output: relatório HTML com gráficos SVG + arquivo MD de ações.

---

## Passo 0 — Carregar contexto

Leia antes de qualquer ação:

```
memoria/produto-ativo.md           → pasta ativa
{pasta-ativa}/memoria/nicho.md     → nicho, avatar
{pasta-ativa}/memoria/produto.md   → produto, preço, ticket, formato
{pasta-ativa}/memoria/funil.md     → estrutura do funil, metas de CPL/CPA, lead magnet
```

Se `produto-ativo.md` ausente ou memória vazia → **PARE**, execute `/egreen-setup`.

---

## Passo 1 — Coletar período e plataformas

Pergunte em uma mensagem:

```
Qual período vamos analisar? (ex: últimos 7 dias / 30 dias / mês de junho)

Quais plataformas têm dados?
1. Meta Ads (Facebook/Instagram)
2. Google Ads
3. Ambas
4. Nenhuma — análise só de email e funil orgânico
```

---

## Passo 2 — Coletar métricas

Pergunte em uma mensagem, agrupadas por bloco:

### Bloco Tráfego Pago (Meta e/ou Google)
```
Para cada plataforma ativa, informe:
• Investimento total (R$)
• Impressões
• Cliques no link
• CTR (se souber) — ou calcularemos
• CPC médio (se souber) — ou calcularemos
```

### Bloco Captação (Leads)
```
• Leads gerados no período
• CPL médio (ou calcularemos com investimento ÷ leads)
• Origem dos leads: % Meta / % Google / % orgânico
• Taxa de confirmação de duplo opt-in (se usar)
```

### Bloco Vendas
```
• Vendas realizadas
• Receita total (R$)
• Ticket médio (se houver variação)
• Reembolsos/cancelamentos no período
• Plataforma de venda (Hotmart / Kiwify / Eduzz / outra)
```

### Bloco Email (se tiver sequência ativa)
```
• Taxa média de abertura (%)
• Taxa média de clique (%)
• Taxa de descadastro (%)
• Qual sequência está ativa (boas-vindas / nutrição / lançamento)
```

### Bloco Produto (se quiser análise completa)
```
• Order bumps vendidos / % de aceitação
• Upsells vendidos / % de aceitação
• Suporte / reclamações no período (estimativa)
```

Se o usuário não tiver algum bloco, pular e notar como "dados indisponíveis".

---

## Passo 3 — Calcular métricas derivadas

Com os dados coletados, calcule e mostre antes do relatório final:

### Métricas de Tráfego
```
CTR          = Cliques / Impressões × 100
CPC médio    = Investimento / Cliques
CPM          = Investimento / Impressões × 1000
```

### Métricas de Funil
```
CPL          = Investimento / Leads
Taxa opt-in  = Leads / Cliques × 100
CPA          = Investimento / Vendas
Taxa conv.   = Vendas / Leads × 100
```

### Métricas Financeiras
```
ROAS         = Receita / Investimento
Margem bruta = (Receita - Investimento) / Receita × 100
ROI          = (Receita - Investimento) / Investimento × 100
LTV estimado = Ticket médio × (1 + % upsell aceitação)
CAC          = Investimento total / Vendas
```

---

## Passo 4 — Scorecard de Saúde (6 categorias, 0-100)

### Benchmarks Infoproduto Brasil (referência)

| Métrica | Crítico | Abaixo | OK | Bom | Excelente |
|---------|---------|--------|-----|-----|-----------|
| CTR Meta | <0,5% | 0,5-1% | 1-2% | 2-4% | >4% |
| CTR Google | <1% | 1-3% | 3-5% | 5-8% | >8% |
| Taxa opt-in LP | <10% | 10-20% | 20-35% | 35-50% | >50% |
| CPL (depende do nicho) | — | — | benchmark do nicho | — | — |
| Taxa conv. lead→venda | <0,5% | 0,5-1% | 1-3% | 3-5% | >5% |
| ROAS perpétuo | <1 | 1-2 | 2-3 | 3-5 | >5 |
| ROAS lançamento | <2 | 2-3 | 3-5 | 5-8 | >8 |
| Abertura email | <10% | 10-20% | 20-30% | 30-40% | >40% |
| Clique email | <1% | 1-2% | 2-4% | 4-7% | >7% |
| Descadastro email | >2% | 1-2% | 0,5-1% | 0,2-0,5% | <0,2% |

### Categorias do Score

**1. Tráfego (0-100)** — Eficiência do criativo e segmentação
- CTR: 40 pts
- CPC relativo ao CPL viável: 40 pts
- Consistência (variância entre campanhas): 20 pts

**2. Captação (0-100)** — Eficiência da página de captura
- Taxa opt-in da LP: 50 pts
- CPL vs meta definida em funil.md: 30 pts
- Qualidade da fonte (baixo descadastro): 20 pts

**3. Conversão (0-100)** — Eficiência da oferta e copy de venda
- Taxa conv. lead→venda: 50 pts
- CPA vs ticket: 30 pts
- Reembolso <5%: 20 pts

**4. Financeiro (0-100)** — Rentabilidade
- ROAS vs mínimo viável (3:1 perpétuo): 50 pts
- Margem bruta: 30 pts
- ROI positivo com headroom: 20 pts

**5. Email (0-100)** — Engajamento da lista
- Taxa abertura: 40 pts
- Taxa clique: 40 pts
- Descadastro: 20 pts

**6. Escalabilidade (0-100)** — Potencial de crescimento
- ROAS > 4:1 (há margem para escalar): 40 pts
- CTR estável ou crescente: 30 pts
- Sem gargalo na página de captura: 30 pts

**Score geral:**
```
Score = (Tráfego × 0.20) + (Captação × 0.20) + (Conversão × 0.25) +
        (Financeiro × 0.20) + (Email × 0.10) + (Escalabilidade × 0.05)
```

| Score | Grade | Diagnóstico |
|-------|-------|-------------|
| 85-100 | A | Máquina rodando. Hora de escalar. |
| 70-84 | B | Sólido. 1-2 ajustes podem subir 20-30%. |
| 55-69 | C | Funciona mas tem vazamento claro. Identificar e tapar antes de escalar. |
| 40-54 | D | Deficitário ou no limite. Não escalar. Otimizar primeiro. |
| 0-39 | F | Pausar e reestruturar. Está queimando dinheiro. |

---

## Passo 5 — Detectar vazamentos do funil

Analise cada etapa e aponte onde a queda é desproporcional:

```
[Cliques] → [Leads] → [Lista ativa] → [Vendas]
   ↓ taxa opt-in    ↓ engajamento email  ↓ taxa conversão
```

**Regras de detecção:**

| Sintoma | Diagnóstico | Ação |
|---------|-------------|------|
| CTR <1% Meta | Criativo fraco ou público errado | Testar novo ângulo de anúncio (`/egreen-mandala`) |
| Taxa opt-in <20% | LP fraca ou tráfego frio demais | Otimizar LP (`/egreen-landing`) ou aquecer mais |
| CPL alto + opt-in ok | CPC alto = leilão competitivo | Testar público diferente ou horário |
| Lista engajada, conversão <1% | Copy de venda fraca ou oferta errada | Revisar oferta (`/egreen-concepcao`) + copy (`/egreen-copy`) |
| ROAS <2 | Custo de aquisição alto demais | Reduzir CPL OU aumentar LTV (upsell, bump) |
| Abertura email <15% | Deliverability ruim ou subjects ruins | Higienizar lista + testar subjects |
| Clique email <1% | CTAs fracos ou conteúdo sem relevância | Revisar copy dos emails (`/egreen-emails`) |
| Descadastro >1,5% | Público errado na lista ou frequência alta | Rever segmentação e cadência |
| Reembolso >5% | Expectativa desalinhada ou produto fraco | Revisar promessa (`/egreen-concepcao`) |

---

## Passo 6 — Plano de ação priorizado

Gere ações organizadas em 3 horizontes baseadas nos vazamentos detectados:

**Ações Imediatas (essa semana)** — alto impacto, baixo esforço
**Médio Prazo (próximas 2-4 semanas)** — impacto alto, esforço médio
**Estratégico (próximo mês+)** — fundacional, requer planejamento

Para cada ação incluir:
- O que fazer (específico, não genérico)
- Impacto esperado (% estimada de melhoria na métrica)
- Skill relacionada (ex: `/egreen-mandala`, `/egreen-landing`, `/egreen-emails`)

---

## Passo 7 — Gerar output HTML

Gere arquivo HTML autocontido (sem dependências externas) com:

### Estrutura do HTML

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Análise de Performance — [Produto] — [Data]</title>
  <style>
    /* Reset e base */
    /* Paleta: #1B2A4A navy, #2D5BFF azul, #FF6B35 laranja, #00C853 verde,
               #FFB300 âmbar, #FF1744 vermelho, #F5F7FA fundo, #2C3E50 texto */
    /* Tipografia sans-serif nativa */
    /* Cards com sombra suave */
    /* Tabelas zebradas */
    /* Barra de progresso CSS pura para scores */
  </style>
</head>
<body>

  <!-- CABEÇALHO -->
  <!-- Produto, período, data de geração -->

  <!-- SCORE GERAL -->
  <!-- SVG: gauge circular com score numérico e grade (A-F) -->
  <!-- Cor do gauge baseada no score (verde/azul/âmbar/vermelho) -->

  <!-- SCORECARD POR CATEGORIA -->
  <!-- SVG: barras horizontais coloridas por score -->
  <!-- Tabela: categoria | score | grade | finding principal -->

  <!-- MÉTRICAS DO FUNIL -->
  <!-- Tabela completa: métrica | valor | benchmark | status (✅❌⚠️) -->

  <!-- VISUALIZAÇÃO DO FUNIL -->
  <!-- SVG: funil vertical com Cliques → Leads → Vendas + taxas de conversão -->

  <!-- DIAGNÓSTICO DE VAZAMENTOS -->
  <!-- Lista de vazamentos detectados com severidade -->

  <!-- PLANO DE AÇÃO -->
  <!-- 3 seções: Imediato | Médio Prazo | Estratégico -->
  <!-- Cada ação com checkbox, impacto esperado, skill relacionada -->

  <!-- RODAPÉ -->
  <!-- Gerado por EGreen OS | Data | Produto -->

</body>
</html>
```

### Regras do HTML

- **Auto-contido:** zero imports externos (sem CDN, sem fonts externas)
- **Gráficos em SVG inline** — gauge de score e barras por categoria
- **Tabelas responsivas** com status visual (✅ bom, ⚠️ atenção, ❌ crítico)
- **Cores mapeadas por score:** verde ≥80, azul 60-79, âmbar 40-59, vermelho <40
- **Funil SVG** mostrando as taxas de conversão de cada etapa
- **Print-friendly** — funciona impresso em PDF pelo browser

---

## Encerramento da Skill

Salvar dois arquivos:

```
{pasta-ativa}/egreen-analise/YYYY-MM-DD-performance-[periodo].html   ← relatório visual
{pasta-ativa}/egreen-analise/YYYY-MM-DD-acoes-[periodo].md           ← só o plano de ação
```

Exibir confirmação:

```
✅ Salvo em: {pasta-ativa}/egreen-analise/

Score geral: [X]/100 (Grade [X])
Principal vazamento: [diagnóstico em 1 linha]
Ação #1: [ação mais prioritária]

Próximo passo: [skill recomendada baseada no diagnóstico]
```

---

## Notas de uso sem dados completos

Se o usuário tiver apenas parte dos dados:

- **Só tráfego:** gerar análise de tráfego + scorecard parcial (marcar demais como N/D)
- **Só email:** gerar diagnóstico de lista + recomendações
- **Só financeiro:** calcular ROAS, margem, ROI e dar diagnóstico de rentabilidade
- **Sem dados nenhum:** oferecer template de coleta de métricas em MD para o usuário preencher

Nunca inventar números. Se dado ausente → marcar `N/D` e notar que a categoria não pontua.
