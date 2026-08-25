---
name: egreen-conteudo
description: >
  Sistema de estratégia de conteúdo e autoridade pessoal/de marca — do "não sei sobre o que falar" até "meu texto não está bom", passando por mineração de repertório, transformação de matéria-prima em volume editorial, estudo de creators sem cópia, ganchos de descoberta (celebridade/empresa/notícia/analogia/lista), estrutura argumentativa de carrossel, conteúdo de autoridade pra público empresarial, auditoria editorial estilo David Ogilvy, e um plano de implementação de 30 dias. Baseado no manual BrandsDecoded (7 metodologias: Rony Meisler, Gary Vee, engenharia reversa de creators, ganchos de descoberta, arquitetura de carrossel, autoridade empresarial, edição Ogilvy). Use sempre que o usuário pedir ideias de conteúdo, não souber sobre o que postar, quiser transformar uma reunião/aula/vídeo em vários posts, quiser se inspirar em um creator sem copiar, quiser um gancho usando notícia/celebridade/empresa em alta, quiser estruturar um carrossel argumentativo, quiser conteúdo que gere autoridade com público empresarial/executivo, quiser auditar um texto antes de publicar, ou quiser um plano de 30 dias pra sair do zero numa operação editorial — mesmo sem citar BrandsDecoded, Meisler, Gary Vee ou Ogilvy. Esta skill só é acionada sob demanda — não faz parte do fluxo automático de `/egreen-lancamento`. Gera ideias/argumento/roteiro de conteúdo; a produção visual final de carrossel é feita por `egreen-carrossel`/`egreen-editorial`/`egreen-brand-carrossel`.
---

# Conteúdo e Autoridade (BrandsDecoded)

Sistema de estratégia editorial em 7 metodologias + plano de implementação, baseado no manual BrandsDecoded — Guia Mestre de Conteúdo. Skill autônoma, acionada só quando o usuário pede — não roda automaticamente dentro de `/egreen-lancamento` ou qualquer outra skill.

**Princípio central (atravessa todos os módulos):** repertório antes de opinião · mecanismo antes de estética · interpretação antes de resumo · critério antes de ranking · evidência antes de certeza · comunidade antes de produto · diagnóstico antes de reescrita · consistência antes de volume.

---

## Passo 0 — Carregar memória do produto ativo (se existir)

```
memoria/produto-ativo.md                    → pasta ativa
{pasta-ativa}/memoria/nicho.md              → nicho, avatar (se existir)
{pasta-ativa}/memoria/produto.md            → produto (se já definido)
{pasta-ativa}/memoria/brand-voice.md        → voz de marca (se existir)
```

Esta skill **não bloqueia** se não houver produto ativo — o Módulo 1 (Meisler) é feito justamente pra quem ainda não sabe qual produto vai criar. Se a memória existir, use pra pré-preencher perguntas (nicho, público, voz) e pule o que já estiver respondido. Se `brand-voice.md` existir, aplique nas peças finais de qualquer módulo.

---

## Passo 1 — Identifique o problema do usuário

Se o usuário já pediu algo específico (ex: "quero um carrossel de contraste sobre X"), pule direto pro módulo correspondente. Caso contrário, pergunte qual situação descreve melhor o momento dele:

```
Qual é a sua situação agora?

1. Não sei sobre o que falar / não tenho posicionamento editorial claro
2. Tenho material (reunião, aula, vídeo) mas faltam ideias de conteúdo
3. Quero me inspirar em um creator/concorrente sem copiar
4. Preciso de alcance — ideias que furam a bolha atual
5. Preciso de conteúdo que gere autoridade com público empresarial/executivo
6. Tenho um texto pronto e quero revisar antes de publicar
7. Quero montar a operação inteira do zero (plano de 30 dias)
```

Mapeamento pergunta → módulo:
- 1 → Módulo 1 (Meisler)
- 2 → Módulo 2 (Gary Vee)
- 3 → Módulo 3 (Creators / engenharia reversa)
- 4 → Módulo 4 (Descoberta) + Módulo 5 (Carrossel) se o formato final for carrossel
- 5 → Módulo 6 (Autoridade empresarial)
- 6 → Módulo 7 (Ogilvy)
- 7 → Módulo 8 (Implementação 30 dias)

---

## MÓDULO 1 — Do repertório ao produto (Rony Meisler)

**Quando usar:** início de posicionamento, reposicionamento, ou criação de produto — quando o usuário tem experiência mas não enxerga linha editorial ou oportunidade de negócio coerente.

Consulte `references/01-meisler-repertorio.md` e execute as 6 fases em ordem (Repertório → Assunto → Audiência → Comunidade → Escuta → Produto), sem pular nenhuma. Aplique o filtro de validação antes de propor qualquer produto.

Se o usuário já tem produto definido em `memoria/produto.md`, use a Fase 6 pra checar se o produto atual bate com a demanda/repertório reais, sinalizando gap em vez de aceitar cegamente.

---

## MÓDULO 2 — Matéria-prima em volume (Gary Vee)

**Quando usar:** depois de reunião, aula, podcast, vídeo, entrevista, anotação extensa — quando o usuário quer transformar isso em vários conteúdos.

Consulte `references/02-garyvee-materia-prima.md`. Peça a matéria-prima completa (transcrição/notas) e execute Capture → Extraia → Multiplique → Adapte → Distribua → Aprofunde. Entregue os 30 conteúdos como formato + hook + ideia central + desenvolvimento (estrutura, não o texto final de cada peça — se o usuário quiser o texto completo de uma peça específica, desenvolva só essa). Aplique o teste de duplicação antes de entregar a lista final.

---

## MÓDULO 3 — Aprenda com creators sem copiar

**Quando usar:** o usuário quer se inspirar em um creator/concorrente específico, ou o feedback recebido foi "seu conteúdo parece genérico".

Consulte `references/03-creators-engenharia-reversa.md`. Execute os 5 passos em ordem (A. estrutura recorrente → B. mecanismo vs estética → C. tradução pro nicho → D. filtro do que não copiar → E. versão original). **Não pule etapa** — pular direto pra "versão original" sem passar pelo filtro D é o erro mais comum e produz conteúdo derivativo. Aplique o teste de originalidade no final: se uma ideia poderia sair do creator original quase igual, descartar.

---

## MÓDULO 4 — Conteúdos que furam a bolha (Descoberta)

**Quando usar:** o usuário quer alcance fora da audiência atual, usando atenção emprestada de algo já reconhecido.

Consulte `references/04-descoberta-atencao-emprestada.md`. Pergunte qual das 5 entradas o usuário prefere (ou sugira a mais adequada ao contexto):
- A. Celebridade usada pro negócio
- B. Empresa do momento como estudo de caso
- C. Notícia fora do nicho, até ser
- D. Comparação que explica ideia difícil
- E. Lista que ajuda o cliente a decidir

Execute a lógica de pesquisa (usar WebSearch quando disponível para fatos/notícias recentes verificáveis — nunca inventar fato, fonte ou data), gere as 10 opções, selecione e desenvolva conforme a referência. Sempre separar fato de interpretação de hipótese.

---

## MÓDULO 5 — Carrossel como argumento

**Quando usar:** o usuário quer a estrutura/argumento de um carrossel (a produção visual final fica com `egreen-carrossel`/`egreen-editorial`/`egreen-brand-carrossel`).

Consulte `references/05-carrossel-argumento.md`. Pergunte qual das 4 estruturas (Contraste / Opinião impopular / Caso conhecido / Lista específica) ou sugira a mais adequada ao objetivo do usuário. Gere as 10 ideias, selecione as 3 melhores, e para a escolhida monte a sequência de slides usando a arquitetura recomendada (capa → contexto → virada → desenvolvimento → síntese → ação). Ao final, ofereça encaminhar pra `egreen-carrossel` (curiosidade atemporal), `egreen-editorial` (dado/pesquisa/polêmica) ou `egreen-brand-carrossel` (sistema de marca) pra produção visual.

---

## MÓDULO 6 — Radar de empresários (Autoridade)

**Quando usar:** o público-alvo do conteúdo são pares/decisores do setor (não o consumidor final do produto).

Consulte `references/06-autoridade-empresarial.md`. Pergunte qual das 3 estruturas (Ranking com critério / Decisão empresarial desmontada / Tese sobre o futuro do setor) — cada uma aumenta a exigência de rigor. Use WebSearch pra pesquisa real de players/decisões/mudanças de mercado quando disponível. Nunca atribuir intenção a empresa sem evidência; sempre apresentar o melhor argumento contra a própria tese.

---

## MÓDULO 7 — Edite como Ogilvy

**Quando usar:** antes de publicar qualquer peça (post, e-mail, página, roteiro, artigo, proposta, carrossel) — inclusive peças que saíram de outra skill do sistema (`egreen-copy`, `egreen-emails`, `egreen-vsl`, etc.), quando o usuário quiser uma segunda camada de revisão de clareza/voz.

Consulte `references/07-ogilvy-edicao.md`. **Nunca reescreva de cara.** Produza primeiro o diagnóstico completo (problema geral, críticos, moderados, o que preservar, corte, clareza da ação, notas 0-10) e só depois pergunte se o usuário quer a versão corrigida. Se `brand-voice.md` existir, use como referência de tom na auditoria. Rode o checklist editorial final antes de considerar a peça pronta pra publicar.

---

## MÓDULO 8 — Implemente o sistema (plano de 30 dias)

**Quando usar:** o usuário quer sair do zero e montar uma operação editorial real, não só uma peça isolada.

Consulte `references/08-implementacao-30-dias.md`. Apresente o plano semana a semana (Fundação → Produção → Distribuição e escuta), adaptando aos recursos/tempo reais do usuário — pergunte quanto tempo por semana ele tem disponível antes de prometer o cronograma padrão. Ofereça o ritual semanal de revisão como rotina contínua, não só como etapa única do plano de 30 dias.

---

## Passo Final — Salvar output

```
{pasta-ativa}/egreen-conteudo/{YYYY-MM-DD-descricao-curta}.md
```

Se não houver produto ativo configurado (uso do Módulo 1 antes de qualquer `/egreen-setup`), informe ao usuário que o output não tem pasta de produto pra salvar automaticamente e ofereça entregar só no chat, ou sugerir rodar `/egreen-setup` primeiro se ele quiser manter isso registrado no sistema.

Confirmação (quando houver pasta ativa):
```
✅ Salvo em: {pasta-ativa}/egreen-conteudo/{YYYY-MM-DD-descricao-curta}.md

Próximo passo: {sugestão, ex: produzir a peça em egreen-carrossel, ou revisar com Módulo 7 antes de publicar}
```

---

## Notas de estilo

- Nunca inventar autoridade, fato, dado, fonte, data ou resultado que o usuário não forneceu ou que não venha de busca real verificável.
- Cada módulo é independente — não force o usuário a passar por todos; entre direto no que ele pediu.
- Separar sempre fato de interpretação de hipótese, em qualquer módulo que envolva pesquisa (3, 4, 6).
- Créditos: metodologia adaptada do manual BrandsDecoded — Guia Mestre de Conteúdo (Rony Meisler, Gary Vee, David Ogilvy como referências citadas no material original).
