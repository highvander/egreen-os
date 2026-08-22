---
name: egreen-metricas
description: "Planeja e audita medicao de marketing/dados usando os frameworks de Avinash Kaushik (ex-Diretor de Analytics da Intuit, Evangelista de Marketing Digital do Google, autor de Web Analytics 2.0): decisao por HiPPO vs por dado, regra 10/90 (ferramenta vs pessoas), macro-conversao vs micro-conversoes, o framework See-Think-Do-Care para segmentar audiencia por intencao, e equilibrio entre dado quantitativo e qualitativo. Use sempre que o usuario pedir para definir metricas/KPIs, montar plano de medicao ou dashboard, auditar se os dados atuais fazem sentido, decidir o que medir em uma campanha ou funil, ou questionar se uma metrica e vaidade ou resultado real - mesmo sem citar Kaushik, See-Think-Do, HiPPO ou 10/90. Funciona como camada de medicao sobre as outras skills de marketing do EGreen OS (egreen-posicionamento, egreen-copywriting, egreen-growth, egreen-seo-estrategia) - reaproveite o contexto delas quando disponivel. E o plano de medicao que antecede a analise de campanha ja rodando feita por egreen-analise."
---

# Métricas e Medição (Kaushik)

Esta skill aplica a abordagem de Avinash Kaushik para transformar dado em decisão de negócio, não em decoração de dashboard. Ao contrário de skills que decidem posicionamento, mensagem, funil ou SEO, esta skill funciona como uma **camada de medição** que pode ser aplicada sobre qualquer uma delas — ela audita e estrutura o que medir e como decidir com base no dado.

**Princípio central de Kaushik, resumido**: dado só vale a pena se muda uma decisão. Se uma métrica não influencia nenhuma ação, é vaidade — reportá-la como sucesso é o mesmo erro que decidir por hierarquia em vez de evidência.

**Como se relaciona com `egreen-analise`:** esta skill define o *plano de medição* (o que medir, por que, e o que ignorar) antes ou durante a estruturação do funil. `egreen-analise` usa esse plano depois, com a campanha já rodando, para calcular ROAS/CPL/CPA e diagnosticar vazamentos reais com os números que entraram. Rode `egreen-metricas` primeiro quando a instrumentação ainda não existir.

---

## Passo 0 — Carregar memória do produto ativo

Antes do intake, leia:

```
memoria/produto-ativo.md                    → pasta ativa
{pasta-ativa}/memoria/produto.md            → produto, oferta
{pasta-ativa}/memoria/funil.md              → funil já desenhado (via egreen-funil/egreen-growth)
```

Se já existir um output de `egreen-growth` salvo em `{pasta-ativa}/egreen-growth/`, reaproveite o mapa de CVJ (Aware/Engage/.../Promote) na Fase 4 em vez de mapear do zero. Se `memoria/produto-ativo.md` não existir, siga com o intake normal — este passo não bloqueia a skill.

---

## Quando usar

Acione esta skill sempre que o usuário pedir para:
- Definir métricas/KPIs de uma campanha, funil, site ou produto
- Montar um plano de medição ou estrutura de dashboard
- Auditar se os dados que já são reportados fazem sentido
- Decidir o que medir em uma ação específica de marketing
- Questionar se um número reportado é resultado real ou métrica de vaidade
- Entender por que uma decisão de marketing está sendo tomada "no feeling" e como trazer dado para ela

Se o usuário já estiver trabalhando com `egreen-growth` ou `egreen-seo-estrategia`, reaproveite o funil/plano já definido e aplique esta skill na Fase de métricas correspondente, em vez de recomeçar do zero.

---

## Como funciona o processo

```
FASE 0 — Intake             → contexto do negócio e do que já é medido hoje
FASE 1 — Diagnóstico HiPPO    → como as decisões são tomadas hoje (dado ou hierarquia?)
FASE 2 — Auditoria 10/90      → onde está o investimento: ferramenta ou análise?
FASE 3 — Mapa de conversões   → macro-conversão e as micro-conversões no caminho
FASE 4 — See-Think-Do-Care    → segmentar audiência por intenção, não só por dado demográfico
FASE 5 — Plano de medição final → o que medir, por camada, e o que ignorar
```

---

## FASE 0 — Intake

Complete o que não veio da memória (pergunte ao usuário o que faltar; não invente números sobre o negócio real):

1. O que o produto está tentando decidir ou melhorar com dado (uma campanha? o funil todo? uma página específica?)
2. O que já é medido hoje, mesmo que informalmente
3. Como as decisões de marketing são tomadas hoje — com base em dado, em opinião de quem decide, ou mistura dos dois?
4. Que ferramentas de medição já existem (analytics, CRM, pesquisa de usuário)?

---

## FASE 1 — Diagnóstico HiPPO

1. Pergunte: as últimas 2-3 decisões de marketing importantes foram tomadas com base em dado, ou na opinião da pessoa mais experiente/mais bem paga na sala?
2. Se a resposta apontar para decisão por hierarquia/intuição, isso não é necessariamente errado sempre (intuição tem valor, especialmente com pouco dado disponível) — mas sinalize isso ao usuário como um padrão a observar, e sugira que a próxima decisão relevante seja testada com dado antes de escalar.
3. Nunca trate "HiPPO" como insulto pessoal — é um padrão organizacional, não uma crítica individual. Framing correto: "como podemos trazer mais evidência para essa decisão", não "vocês decidem errado".

---

## FASE 2 — Auditoria 10/90

1. Estime (com o usuário) a proporção atual de investimento entre ferramenta/software de analytics e pessoas/tempo dedicado a interpretar esses dados.
2. Se o investimento estiver concentrado quase todo em ferramenta e pouco ou nada em análise humana dedicada, sinalize isso como o gargalo mais provável — ferramenta sem interpretação não gera decisão, só relatório.
3. Não é necessário literalmente atingir a proporção 10/90 — é uma heurística para chamar atenção ao desequilíbrio, não uma meta rígida a ser seguida ao pé da letra.

---

## FASE 3 — Mapa de conversões (macro e micro)

1. **Identifique a macro-conversão**: o resultado final de negócio (venda, assinatura, lead qualificado).
2. **Mapeie as micro-conversões no caminho**: os sinais intermediários de intenção que acontecem antes da macro-conversão (ex: uso de calculadora/simulador, assistir vídeo até o fim, adicionar ao carrinho, iniciar cadastro, abrir e-mail, agendar demonstração).
3. Para cada micro-conversão mapeada, pergunte: isso está sendo medido hoje? Se não, sinalize como lacuna de instrumentação antes de avançar.
4. Regra prática: medir só a macro-conversão dificulta diagnosticar onde o funil está travando — as micro-conversões são o que permite identificar o ponto exato de perda antes da venda.

Consulte `references/macro-micro-conversoes.md` para exemplos por tipo de negócio.

---

## FASE 4 — See-Think-Do-Care

Classifique a audiência/conteúdo/campanha em uma das quatro camadas de intenção:

| Camada | Quem é essa audiência | Erro comum a evitar |
|---|---|---|
| **See** | Audiência endereçável total, ainda sem intenção clara de compra | Medir essa camada pela taxa de conversão em venda — ela ainda não está pronta para isso |
| **Think** | Já considera a categoria, está pesquisando opções | Empurrar oferta de venda direta antes de educar/comparar |
| **Do** | Tem intenção de compra ativa | Não remover atrito suficiente no momento de decisão |
| **Care** | Já é cliente | Ignorar métricas de retenção/satisfação, tratando a venda como linha de chegada |

Para cada camada, defina uma métrica de sucesso própria — nunca usar a métrica de "Do" (conversão em venda) para julgar o desempenho de conteúdo/campanha de "See".

Se o usuário já tem a Customer Value Journey de Deiss mapeada (via `egreen-growth`), cruze as camadas: See/Think ≈ Aware/Engage, Do ≈ Subscribe/Convert, Care ≈ Excite/Ascend/Advocate/Promote — não repita o mapeamento do zero, só aplique a métrica certa a cada estágio já definido.

Consulte `references/see-think-do-care.md` para o template completo e exemplo preenchido.

---

## FASE 5 — Plano de medição final

Entregue:

1. Uma métrica principal por camada/estágio (não uma lista longa de KPIs vagos)
2. As micro-conversões mapeadas na Fase 3, com indicação de quais já são medidas e quais precisam de instrumentação
3. Equilíbrio explícito entre dado quantitativo (o que aconteceu) e qualitativo (por que aconteceu) — para cada métrica quantitativa relevante, sugerir uma forma de coletar o "porquê" (pesquisa curta, teste de usabilidade, entrevista)
4. Uma nota clara sobre o que NÃO vale a pena medir/reportar como sucesso isolado (ex: tráfego bruto sem contexto de conversão, curtidas sem engajamento real)

---

## Passo Final — Salvar output

Depois de aprovado pelo usuário, salve o plano de medição em:

```
{pasta-ativa}/egreen-metricas/{YYYY-MM-DD-descricao-curta}.md
```

Exiba a confirmação:

```
✅ Salvo em: {pasta-ativa}/egreen-metricas/{YYYY-MM-DD-descricao-curta}.md

Próximo passo: instrumentar o que faltar e, com a campanha rodando, usar /egreen-analise para diagnosticar performance real
```

---

## Notas de estilo

- Nunca inventar números, benchmarks de mercado ou dados de ferramentas que o usuário não forneceu.
- Framing sempre construtivo em relação a decisões passadas por intuição — o objetivo é trazer mais evidência, não criticar quem decidiu antes.
- Se o usuário pedir um dashboard ou arquivo de acompanhamento, gerar no formato apropriado (xlsx) usando a skill de documento correspondente; caso contrário, entregar o plano direto na conversa (e salvar o Markdown conforme o Passo Final).
