---
name: egreen-cro
description: "Diagnostica por que uma pagina/funil nao converte e prioriza o que testar, usando a metodologia de Peep Laja (fundador da ConversionXL/CXL): o processo de Conversion Research em 7 passos (analise tecnica, heuristica, web analytics, mouse tracking/heatmaps, pesquisa qualitativa, teste de usuario, consolidacao), o principio de tratar toda opiniao - inclusive a propria - como hipotese a testar, e a regra de nunca pular direto para um teste A/B sem pesquisa antes. Use esta skill sempre que o usuario pedir para melhorar taxa de conversao, diagnosticar por que uma pagina/landing page/checkout nao converte, priorizar o que testar em A/B, ou revisar a landing page do infoproduto - mesmo que ele nao mencione Peep Laja, CXL, CRO ou 'conversion research' explicitamente. Esta skill entra depois de egreen-growth (que ja identificou o gargalo de etapa) e antes de egreen-copywriting/egreen-copy (que escrevem a solucao) - reaproveite o contexto dessas skills quando disponivel em vez de repetir o intake."
---

# CRO — Conversion Research (Peep Laja / CXL)

Esta skill aplica o processo de pesquisa de conversão de Peep Laja: nunca propor um teste A/B ou uma mudança de página sem antes diagnosticar, com dado real, por que a conversão não está acontecendo.

**Princípio central**: toda opinião sobre "o que vai converter mais" — inclusive a do próprio usuário, inclusive a desta skill — deve ser tratada como hipótese a testar, não como verdade. Copiar tática de concorrente sem pesquisa própria não funciona, porque o concorrente provavelmente também não fez a pesquisa.

---

## Passo 0 — Carregar memória do produto ativo

Antes do intake, leia:

```
memoria/produto-ativo.md                    → pasta ativa
{pasta-ativa}/memoria/nicho.md              → avatar, dores
{pasta-ativa}/memoria/produto.md            → produto, oferta
{pasta-ativa}/memoria/funil.md              → funil, etapas
```

Se existir HTML de página de vendas salvo em `{pasta-ativa}/egreen-landing/`, ou performance de campanha em `{pasta-ativa}/egreen-analise/`, use como insumo da Fase 0/1 em vez de perguntar do zero. Se `memoria/produto-ativo.md` não existir, siga com o intake normal — este passo não bloqueia a skill.

---

## Quando usar

Acione esta skill sempre que o usuário pedir para:
- Melhorar taxa de conversão de uma página, landing page, checkout ou formulário
- Diagnosticar por que uma página/funil não está convertendo
- Priorizar o que testar em A/B
- Revisar uma página existente antes de investir em redesign ou nova campanha

**Como se encaixa com as outras skills do Evergreen:**
- Entra depois de `egreen-growth`, que já identifica em qual etapa da Customer Value Journey está o gargalo — esta skill aprofunda o diagnóstico *dentro* dessa etapa
- Entra antes de `egreen-copywriting`/`egreen-copy` — o diagnóstico desta skill vira o briefing para a copy nova, em vez de escrever copy nova sem saber o que realmente trava o usuário
- Se cruza com `egreen-metricas` (Kaushik) — os passos quantitativos (analytics, mouse tracking) e qualitativos (survey, teste de usuário) desta skill são uma aplicação prática do equilíbrio que Kaushik defende
- Se cruza com `egreen-analise` (auditoria de campanha rodando: ROAS, CPL) — `egreen-analise` diagnostica performance de mídia paga, esta skill diagnostica a página/experiência em si

Reaproveite contexto dessas skills quando já existir, em vez de repetir o intake.

---

## Como funciona o processo

```
FASE 0 — Intake                    → contexto da página/funil e dado já disponível
FASE 1 — Conversion Research (7 passos) → diagnóstico completo antes de qualquer teste
FASE 2 — Síntese das perguntas-chave     → de quem é o problema, o que precisa, por quê
FASE 3 — Lista de hipóteses priorizadas  → transformar achados em hipóteses testáveis
FASE 4 — Desenho do teste                → como validar a hipótese com rigor mínimo
FASE 5 — Volta à análise                 → o ciclo não termina no teste, volta para o dado
```

---

## FASE 0 — Intake

Complete o que não veio da memória (pergunte ao usuário o que faltar; não invente dados sobre o negócio real):

1. Qual página/funil/fluxo está em foco, e qual é a conversão-alvo (compra, cadastro, lead)
2. Taxa de conversão atual, se souber (mesmo aproximada)
3. Que dados já existem: analytics configurado? heatmap/mouse tracking? gravação de sessão? pesquisa com usuário já feita?
4. Se já existe alguma hipótese do que está travando (mesmo que seja "não sabemos")

Se o usuário não tiver a maioria dos dados, isso não impede a skill — mas deve ser sinalizado como lacuna, e o processo prioriza primeiro coletar o dado mínimo antes de recomendar qualquer mudança.

---

## FASE 1 — Conversion Research (os 7 passos)

Execute os passos possíveis com a informação disponível; sinalize claramente quais passos não puderam ser feitos por falta de dado/ferramenta, em vez de pular silenciosamente.

1. **Análise técnica** — existem problemas óbvios de velocidade, erro, quebra de layout, incompatibilidade mobile que já matam conversão antes de qualquer outra coisa? Perguntar ao usuário ou, se possível, inspecionar a página.
2. **Análise heurística** — revisar a página contra princípios conhecidos de usabilidade/persuasão (clareza da oferta, hierarquia visual, atrito no formulário, prova social visível, CTA único e claro).
3. **Análise de web analytics** — onde exatamente no funil a maior parte das pessoas abandona? (reaproveitar mapa de macro/micro-conversões da skill `egreen-metricas`, se existir)
4. **Análise de mouse tracking/heatmaps** — se houver essa ferramenta disponível, onde o usuário realmente olha/clica versus onde o produto assume que ele olha
5. **Pesquisa qualitativa/surveys** — existe alguma forma de perguntar diretamente a quem não converteu o que travou a decisão? Se não existir, sugerir 2-3 perguntas curtas que poderiam ser adicionadas (ex: pop-up de saída, pesquisa pós-abandono)
6. **Teste de usuário** — existe algum registro de pessoa real tentando usar a página/fluxo? Se não, sugerir um teste informal simples (pedir para 3-5 pessoas do público-alvo tentarem completar a tarefa e narrar em voz alta)
7. **Consolidação** — cruzar tudo o que foi levantado nos passos 1-6 em uma lista organizada de achados, antes de pular para a Fase 3

Consulte `references/conversion-research-checklist.md` para o checklist detalhado de cada passo.

---

## FASE 2 — Síntese das perguntas-chave

Depois da pesquisa, responda explicitamente (com o que foi levantado, sem inventar):

- De quem é o problema que estamos resolvendo nessa página?
- O que essa pessoa realmente precisa nesse momento da jornada?
- O que ela *acha* que quer (que pode ser diferente do que precisa)?
- Por quê? (aprofundar pelo menos uma vez além da resposta óbvia)
- Como ela está comparando/decidindo entre opções?
- Por quê? (aprofundar de novo)

Essa repetição do "por quê" é proposital — o objetivo é não parar na primeira resposta superficial (ex: "o preço é alto" pode esconder "não ficou claro o valor entregue").

---

## FASE 3 — Lista de hipóteses priorizadas

Para cada achado relevante da Fase 1/2, formule como hipótese testável no formato:

> Se [mudança], então [resultado esperado], porque [evidência da pesquisa que sustenta isso].

Priorize as hipóteses por:
1. Força da evidência que sustenta (múltiplas fontes de pesquisa apontando o mesmo problema > uma opinião isolada)
2. Facilidade de implementação
3. Potencial de impacto (proximidade com a conversão-alvo — mudanças perto do CTA final tendem a ter ciclo de teste mais rápido que mudanças de topo de funil)

Nunca recomendar uma hipótese "porque parece melhor" sem ancorá-la em algum achado da Fase 1 — se não houver evidência nenhuma sustentando uma ideia, sinalizar isso explicitamente como suposição a validar, não como recomendação pronta.

---

## FASE 4 — Desenho do teste

Para a hipótese priorizada:
1. Definir a métrica de sucesso única e clara (a mesma conversão-alvo do intake)
2. Definir o que muda entre a versão atual e a versão testada — o mínimo necessário para isolar a variável, evitando testar muitas mudanças ao mesmo tempo sem conseguir atribuir o resultado a uma causa
3. Sinalizar ao usuário, quando relevante, que resultado de teste A/B só é confiável com volume mínimo de tráfego/conversões — se o volume for baixo, sugerir alternativas (teste qualitativo, mudança direta com monitoramento, em vez de A/B formal)

---

## FASE 5 — Volta à análise

Depois de um teste rodar (mesmo que fora desta conversa, no futuro):
- O resultado do teste vira novo dado de entrada para a próxima rodada de Conversion Research — o processo é cíclico, não termina em um teste único
- Reforce ao usuário: um teste que "não deu certo" ainda gera aprendizado sobre a hipótese, não é fracasso — é insumo para a próxima hipótese

---

## Passo Final — Salvar output

Depois de aprovado pelo usuário, salve o diagnóstico + hipóteses priorizadas em:

```
{pasta-ativa}/egreen-cro/{YYYY-MM-DD-descricao-curta}.md
```

Exiba a confirmação:

```
✅ Salvo em: {pasta-ativa}/egreen-cro/{YYYY-MM-DD-descricao-curta}.md

Próximo passo: {sugestão, ex: usar o diagnóstico como briefing em /egreen-copywriting ou revisar /egreen-landing}
```

---

## Notas de estilo

- Nunca recomendar mudança de página como "prática recomendada" genérica sem ancorar na pesquisa feita nesta conversa — evitar listas soltas de "100 dicas de CRO".
- Nunca inventar dado de analytics, heatmap ou pesquisa que o usuário não forneceu — se a ferramenta não existir, sinalizar como lacuna e sugerir como uma versão simplificada poderia ser feita sem ferramenta paga.
- Se o diagnóstico apontar para um problema de mensagem/copy, encaminhar explicitamente para a skill `egreen-copywriting` (ou `egreen-copy` para reescrever a página inteira) em vez de escrever a copy final aqui.
- Entregar o diagnóstico e as hipóteses em formato de tabela/lista clara. Se o usuário pedir arquivo, gerar no formato apropriado usando a skill de documento correspondente; caso contrário, entregue na conversa (e salve o Markdown conforme o Passo Final).
