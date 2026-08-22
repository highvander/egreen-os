---
name: egreen-lancamento
description: >
  Orquestrador mestre do EGreen OS. Cria o projeto completo de um infoproduto do zero — nicho, produto, posicionamento, currículo/conteúdo de entrega, funil, identidade, copy, landing, VSL/webinar, e-mails, anúncios, pós-venda, afiliados e métricas — invocando automaticamente as skills egreen-* na ordem certa, decidindo os pontos de escolha com base em 5 frameworks de validação amplamente reconhecidos (Mom Test, Jobs to Be Done, Lean Startup/Running Lean, The Right It/pretotipagem de Savoia, Product-Market Fit Pyramid de Dan Olsen + teste Sean Ellis), em vez de perguntar micro-detalhe a cada etapa. Para em 4 gates críticos para aprovação do usuário; o resto roda de forma encadeada. Use esta skill sempre que o usuário pedir para "criar o produto do zero", "montar o lançamento completo", "fazer todo o pipeline", "orquestrar a criação do infoproduto", "do nicho ao anúncio", ou pedir orientação de "quais as melhores linhas pra esse produto dar certo, incluindo o funil" — mesmo sem citar o nome de nenhuma skill ou framework especificamente.
allowed-tools: Skill, Read, AskUserQuestion, TodoWrite, WebSearch
---

# `/egreen-lancamento` — Orquestrador Completo de Infoproduto

Esta skill não produz conteúdo diretamente. Ela **invoca as outras skills `egreen-*` em sequência**, usando 5 frameworks de validação reconhecidos no mercado para decidir o que fazer em cada ponto de escolha, e para em 4 gates críticos para o usuário aprovar antes de comprometer mais trabalho.

**Antes de tudo, leia `references/frameworks-validacao.md`** — é a fonte dos critérios de decisão usados nas Fases 1 a 4 abaixo. Não improvise os critérios; use os desta referência.

---

## Princípio central

Cada fase deste pipeline corresponde a uma camada da **Product-Market Fit Pyramid** (Dan Olsen): cliente-alvo → necessidade mal atendida → proposta de valor → oferta/funil → UX/mensagem. **Nunca pule uma camada de baixo pra construir a de cima** — não faz sentido escrever copy (camada 5) sem proposta de valor definida (camada 3), e não faz sentido definir proposta de valor sem saber a necessidade real (camada 2). Se o usuário pedir para pular direto pra uma fase avançada (ex: "só quer a landing page"), avise que as camadas abaixo não estão validadas e pergunte se quer mesmo pular ou rodar o pipeline completo primeiro.

---

## Passo 0 — Diagnóstico de progresso e gate de instalação

1. Verifique o gate de instalação (REGRA 1 do `CLAUDE.md`): leia `memoria/produto-ativo.md`. Se não existir, invoque a skill `egreen-setup` primeiro — esta skill não roda sem produto ativo configurado.
2. Com a pasta ativa identificada, verifique **o que já existe** em `{pasta-ativa}/memoria/` e nas pastas de output de cada skill (`{pasta-ativa}/egreen-pesquisa/`, `{pasta-ativa}/egreen-concepcao/`, `{pasta-ativa}/egreen-curriculo/` ou `{pasta-ativa}/egreen-experiencia/` conforme o formato, `{pasta-ativa}/egreen-posicionamento/`, `{pasta-ativa}/egreen-funil/`, `{pasta-ativa}/egreen-growth/`, `{pasta-ativa}/egreen-metricas/`, `{pasta-ativa}/memoria/design.md`, `{pasta-ativa}/memoria/brand-voice.md`, `{pasta-ativa}/egreen-copy/`, `{pasta-ativa}/egreen-landing/`, `{pasta-ativa}/egreen-emails/`, `{pasta-ativa}/egreen-mandala/`, `{pasta-ativa}/egreen-vsl/`, `{pasta-ativa}/egreen-posvenda/`).
3. Monte um **TodoWrite** com as 9 fases abaixo, marcando como concluídas as que já têm output salvo, e mostre ao usuário um resumo curto:
   ```
   Progresso do lançamento — {nome do produto}:
   ✅ Fase 1 — Nicho (concluída em {data})
   ✅ Fase 2 — Produto & posicionamento (concluída em {data})
   ⏳ Fase 3 — Oferta & funil (não iniciada)
   ...
   ```
4. Pergunte (via AskUserQuestion): retomar de onde parou, refazer uma fase específica, ou rodar tudo do zero. Não refaça trabalho aprovado sem essa confirmação — outputs já salvos representam decisão do usuário.

---

## FASE 1 — Cliente-alvo & necessidades mal atendidas (PMF camada 1-2)

**Skills invocadas:** `egreen-nicho`, `egreen-pesquisa`

1. Antes de invocar, informe ao próprio processo de entrevista dessas skills os princípios de **Mom Test** (perguntar comportamento passado, nunca opinião sobre futuro) e **Jobs to Be Done** (reconstruir o gatilho/timeline da decisão, não só demografia) — ver `references/frameworks-validacao.md` §1-2. Ao interagir com o usuário durante essas skills, oriente as perguntas nessa direção mesmo que a skill original pergunte de forma mais genérica.
2. Invoque `egreen-nicho` e, em seguida, `egreen-pesquisa` (pesquisa profunda em 9 eixos com busca real).
3. Ao final, aplique o critério **Lean Startup**: declare explicitamente qual é **a hipótese mais arriscada** deste nicho (quase sempre: "esse problema é doloroso o suficiente pra alguém pagar por solução?") e que evidência concreta (não opinião) sustenta ou não essa hipótese.

**GATE 1 — Nicho aprovado.** Apresente ao usuário: nicho, avatar, dor real (com evidência de comportamento passado, não só declaração), e a hipótese mais arriscada identificada. Pergunte via AskUserQuestion: aprovar e seguir / ajustar nicho / parar aqui. Não avance para a Fase 2 sem aprovação explícita.

---

## FASE 2 — Produto & proposta de valor (PMF camada 3)

**Skills invocadas:** `egreen-produto`, `egreen-concepcao`, `egreen-posicionamento`

1. Invoque `egreen-produto` (gera as 50 ideias). Ao ajudar o usuário a escolher, priorize ideias que respondem diretamente à necessidade mal atendida mapeada na Fase 1 — não a ideia "mais criativa", a que mais resolve a dor com evidência real.
2. Invoque `egreen-concepcao` para o produto escolhido (Promessa, 50 Benefícios, 5 Baldes, Identidade do Consumidor).
3. Invoque `egreen-posicionamento` (Dunford + Ries & Trout) — reaproveite nicho/concorrentes já mapeados na Fase 1, não repita o intake.

**GATE 2 — Produto e posicionamento aprovados.** Apresente produto escolhido, promessa, e positioning statement. AskUserQuestion: aprovar e seguir / ajustar / parar aqui.

---

## FASE 2B — Conteúdo de entrega (currículo/experiência)

**Skills invocadas:** `egreen-curriculo` (Curso Simples/Completo) ou `egreen-experiencia` (Desafio/Comunidade/Mentoria) — invoque a que corresponde ao formato definido em `produto.md`. Para E-book, invoque `egreen-ebook`.

Desenhe agora o conteúdo real de entrega do produto — módulos/aulas ou missões/rituais/sessões — antes de desenhar preço e oferta na Fase 3. O que sai daqui vira os Entregáveis (Bloco 07) da copy mais adiante e a evidência de valor do funil.

Sem gate formal aqui — segue direto para a Fase 3, mas não pule esta fase mesmo que o usuário só peça "a landing page": sem currículo definido, a página vende algo que ainda não foi desenhado.

---

## FASE 3 — Oferta & funil (PMF camada 4)

**Skills invocadas:** `egreen-funil`, `egreen-growth`, `egreen-metricas`

1. Invoque `egreen-funil` (Brunson/Hormozi/Gadzhi) — arquitetura de oferta: tripwire, order bump, upsell, preço.
2. Invoque `egreen-growth` (Patel/Deiss) — motor de aquisição e Customer Value Journey completa, reaproveitando o funil de oferta da Fase 3.1 dentro do mapeamento Convert/Ascend.
3. Invoque `egreen-metricas` (Kaushik) — plano de medição. **Rode isto antes de qualquer tráfego real ser gerado**, para que a instrumentação já exista quando a Fase 4 testar o mercado.

**GATE 3 — Oferta, funil e plano de medição aprovados.** Apresente preço, estrutura de oferta, mapa CVJ resumido e o que será medido. AskUserQuestion: aprovar e seguir / ajustar / parar aqui.

---

## FASE 4 — Teste de risco de mercado (pretotipagem — Savoia)

Este é o gate mais importante do pipeline. **Não pule para produção completa (Fase 5-6) sem passar por aqui**, a menos que o usuário assuma explicitamente o risco.

1. Formule com o usuário a **hipótese XYZ** (ver `references/frameworks-validacao.md` §4): "pelo menos X% de Y vai Z" — ex: "pelo menos 15% de quem vir a página vai deixar o e-mail na lista de espera".
2. Proponha o pretotype mais barato possível: uma landing mínima (hero + promessa + CTA de lista de espera, não a página completa de vendas) — pode ser gerada com uma versão reduzida de `egreen-landing` (só S1 + S6) ou apenas com a copy do Bloco 01 de `egreen-copy`.
3. Se o usuário tiver Meta/Google Ads configurado (`egreen-meta-auth`), sugira um teste pago pequeno (`egreen-meta-ads` ou `egreen-google-ads`, status PAUSED até revisão, orçamento mínimo) para gerar tráfego real e medir o sinal — nunca subir campanha sem preview aprovado pelo usuário.
4. Registre o resultado medido contra a hipótese XYZ.

**GATE 4 — Sinal de mercado validado.** Apresente o resultado (medido, não estimado) contra a hipótese. Três caminhos, via AskUserQuestion:
- **Sinal acima do limiar** → seguir para Fase 5 (produção completa)
- **Sinal abaixo do limiar** → recomendar voltar à Fase 1 ou 2 (nicho/produto), não insistir na mesma direção com mais orçamento — sinalizar isso claramente como recomendação, não decisão automática
- **Pular este gate** (usuário quer ir direto para produção sem testar) → permitido, mas registre explicitamente no resumo final do Passo 6 que este risco foi assumido sem validação de mercado

---

## FASE 5 — Identidade & voz

**Skills invocadas:** `egreen-identidade`, `egreen-design`, `egreen-brand`

1. Invoque `egreen-identidade` (Neumeier/Pentagram) — onliness statement consistente com o positioning statement da Fase 2.
2. Invoque `egreen-design` — traduz a onliness statement em paleta, tipografia, componentes.
3. Invoque `egreen-brand` — voz de marca, para ser usada por todas as skills de copy a seguir.

Sem gate formal aqui — cada uma dessas skills já tem aprovação interna por bloco/seção.

---

## FASE 6 — Produção completa (PMF camada 5 — UX/mensagem)

**Skills invocadas (na ordem que o usuário priorizar):** `egreen-copy` (página de vendas em 15 blocos) ou `egreen-copywriting` (peças avulsas), `egreen-landing`, `egreen-emails`, `egreen-mandala` (anúncio + roteiro de vídeo curto), `egreen-vsl` (webinar/VSL, se o funil tiver esse formato), `egreen-carrossel`/`egreen-editorial`/`egreen-slides`, `egreen-posvenda` (checkout, onboarding, upsell, pedido de depoimento — precisa estar pronto antes da Fase 8, não depois)

Pergunte ao usuário a ordem de prioridade dessas peças em vez de assumir uma sequência fixa — nem todo produto precisa de todas ao mesmo tempo. Se o usuário quiser programa de afiliados, invoque `egreen-afiliados` também nesta fase. Cada skill já tem seu próprio fluxo de aprovação e salvamento; não duplique esses passos aqui.

---

## FASE 7 — CRO pré-lançamento

**Skill invocada:** `egreen-cro`

Antes de subir tráfego pesado, rode o diagnóstico de conversão (Peep Laja) na landing/funil produzido na Fase 6 — foco nos passos 1 (técnico) e 2 (heurístico) do processo, que não dependem de tráfego real ainda existir.

---

## FASE 8 — Subida de campanhas

**Skills invocadas:** `egreen-meta-auth` (se ainda não configurado), `egreen-meta-ads`, `egreen-google-ads`

Sempre status PAUSED por padrão e preview obrigatório antes de qualquer ativação real — segue a regra própria dessas skills, não sobrescreva isso.

---

## FASE 9 — Pós-lançamento: PMF real + performance

**Skill invocada:** `egreen-analise`

1. Com os primeiros compradores/leads reais, sugira aplicar o **teste Sean Ellis** (ver `references/frameworks-validacao.md` §5): "como você se sentiria se não pudesse mais usar/ter [produto]?" — 40%+ "muito decepcionado" é o sinal de PMF real.
2. Invoque `egreen-analise` para ROAS, CPL, CPA, scorecard e diagnóstico de vazamento com dados reais de campanha.
3. Se o PMF (Sean Ellis) estiver baixo mas a campanha estiver "otimizada", sinalize isso explicitamente: o problema não está na mídia, está numa camada mais baixa da pirâmide (proposta de valor ou até cliente-alvo) — recomendar voltar à Fase 1/2, não só ajustar criativo/lance.
4. Se o vazamento for de conversão de página, encaminhar para `egreen-cro`. Se for de mensagem, para `egreen-copywriting`.

---

## Passo Final — Resumo do lançamento

Ao final de cada sessão de trabalho com esta skill (não só ao terminar tudo), gere/atualize um resumo em:

```
{pasta-ativa}/memoria/status-lancamento.md
```

Conteúdo mínimo:
```markdown
# Status do Lançamento — {produto}
Atualizado em: {data}

## Progresso
- [x] Fase 1 — Nicho (aprovado em {data})
- [x] Fase 2 — Produto & posicionamento (aprovado em {data})
- [ ] Fase 3 — Oferta & funil
...

## Riscos assumidos
- {ex: "Gate 4 pulado — produção seguiu sem validação de mercado, por decisão do usuário em {data}"}

## Próximo passo
{fase pendente + skill a invocar}
```

Exiba a confirmação padrão:
```
✅ Salvo em: {pasta-ativa}/memoria/status-lancamento.md

Próximo passo: {fase pendente}
```

---

## Notas de estilo

- Esta skill nunca gera conteúdo final ela mesma — sempre invoca a skill `egreen-*` correta via Skill tool. Se uma etapa não tiver skill correspondente ainda, avise o usuário em vez de inventar o processo.
- Nos 4 gates, use sempre AskUserQuestion — nunca assuma aprovação silenciosa e siga em frente sozinho.
- Se o usuário interromper a sessão e retomar depois, o Passo 0 deve identificar corretamente onde parou usando os arquivos já salvos, não repetir fases concluídas.
- Trate os frameworks de `references/frameworks-validacao.md` como critério de decisão, não como texto a despejar no usuário — cite-os quando ajudam a explicar uma recomendação, não como aula teórica solta.
