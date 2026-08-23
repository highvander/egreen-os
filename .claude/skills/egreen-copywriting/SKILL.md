---
name: egreen-copywriting
description: "Escreve ou revisa copy persuasiva (anuncios, paginas de venda, landing pages, e-mails, cartas de venda, headlines, CTAs) combinando tres escolas: o diagnostico de consciencia e sofisticacao de mercado de Eugene Schwartz (Breakthrough Advertising), a validacao de mercado e estrutura AIDA de resposta direta de Gary Halbert, e a mineracao de Voice of Customer (VoC) de Joanna Wiebe (conversion copywriting / Copyhackers). A skill escolhe quais tecnicas aplicar de acordo com a necessidade real do pedido, nao aplica as tres sempre. Use esta skill sempre que o usuario pedir para escrever, revisar ou melhorar qualquer copy de venda ou marketing - anuncio, e-mail de venda, headline, CTA, roteiro de video de vendas, ou copy de post pago - mesmo que ele nao mencione os nomes Schwartz, Halbert ou Wiebe explicitamente. Para a copy completa dos 15 blocos de uma página de vendas no padrão Light Copy, usar `egreen-copy` em vez desta; esta skill cobre os demais formatos e serve de reforço teórico para qualquer copy avulsa."
---

# Copywriting Persuasivo (Schwartz + Halbert + Wiebe)

Esta skill combina três camadas complementares de copywriting persuasivo. Elas não competem entre si — respondem perguntas diferentes:

| Camada | Autor | Pergunta que responde |
|---|---|---|
| Diagnóstico | Eugene Schwartz | Em que estado mental está o leitor, e o mercado já está cansado dessa promessa? |
| Validação e estrutura | Gary Halbert | Existe mercado faminto de verdade, e a copy segue uma arquitetura que converte? |
| Linguagem | Joanna Wiebe | As palavras usadas são as palavras reais do cliente, ou são "copy de departamento de marketing"? |

**Princípio-chave: nem todo pedido precisa das três camadas com a mesma intensidade.** Um post curto de Instagram não pede uma pesquisa de VoC de duas semanas. Uma carta de venda longa de infoproduto pede as três a fundo. A Fase 0 desta skill existe justamente para calibrar isso — não pule direto para escrever.

**Relação com `egreen-copy`:** `egreen-copy` gera a copy completa dos 15 blocos de página de vendas no padrão Light Copy. Esta skill (`egreen-copywriting`) cobre os demais formatos avulsos — anúncio, e-mail, headline, CTA, roteiro de VSL — e pode ser usada para reforçar/revisar um bloco específico que já saiu do `egreen-copy` com o diagnóstico Schwartz/Halbert/Wiebe.

---

## Passo 0 — Carregar memória do produto ativo

Antes de perguntar qualquer coisa ao usuário, leia:

```
memoria/produto-ativo.md                    → pasta ativa
{pasta-ativa}/memoria/egreen-nicho.md              → avatar, dores, linguagem do público
{pasta-ativa}/memoria/egreen-produto.md            → produto, preço, promessa
{pasta-ativa}/memoria/egreen-funil.md              → oferta, estágio do funil
{pasta-ativa}/memoria/brand-voice.md        → voz de marca (se existir)
```

Se `brand-voice.md` existir: use vocabulário autorizado, evite palavras proibidas, siga as dimensões de tom e o guia do/don't do arquivo. As amostras de copy servem como âncora de estilo — priorize-as como fonte de VoC junto com a Fase 3 (Wiebe) abaixo.

Use os dados carregados para pular perguntas da Fase 0/2 abaixo cujas respostas já estejam na memória (avatar, dor, ângulo de oferta). Se `memoria/produto-ativo.md` não existir ou os arquivos estiverem com `status: vazio`, aplique o framework normalmente com as perguntas diretas ao usuário — este passo não bloqueia a skill.

---

## FASE 0 — Triagem: quanto de cada camada este pedido precisa?

Antes de escrever qualquer linha, classifique o pedido em 2 eixos:

**Eixo 1 — Tamanho/formato do texto**
- Curto (headline, CTA, anúncio de 1-2 linhas, post social) → aplicar Schwartz de forma leve (só o diagnóstico de estágio), Halbert como checklist rápido, Wiebe se houver dados de cliente disponíveis
- Médio (e-mail, anúncio longo) → aplicar as três camadas de forma completa
- Longo (carta de venda avulsa, roteiro de VSL) → aplicar as três camadas a fundo, incluindo pesquisa de mercado dedicada (ver Fase 2)

**Eixo 2 — Informação disponível**
- Se o usuário já tem reviews, tickets de suporte, transcrições de venda ou pesquisas de cliente → priorizar a camada Wiebe (VoC) com mais peso
- Se o usuário não tem esses dados → sinalizar a lacuna, mas seguir com Schwartz + Halbert e perguntar 2-3 perguntas diretas ao usuário para simular a pesquisa (nunca inventar citações de clientes que não existem)
- Se o produto/mercado é novo ou pouco conhecido pelo público → dar mais peso ao diagnóstico de estágio de consciência de Schwartz (provavelmente está em "inconsciente" ou "consciente do problema")
- Se o produto está em mercado maduro e disputado → dar mais peso à sofisticação de mercado de Schwartz (evitar promessa genérica já "queimada" pelos concorrentes) e à diferenciação

Declare ao usuário, em uma frase, qual combinação você vai aplicar e por quê, antes de seguir (ex: "Como é um anúncio curto para um produto novo, vou focar no diagnóstico de estágio de consciência e numa estrutura AIDA enxuta — sem pesquisa de VoC extensa, a menos que você tenha depoimentos de clientes para eu usar").

---

## FASE 1 — Diagnóstico (Schwartz)

Sempre execute esta fase, mesmo que de forma rápida em pedidos curtos.

1. **Estágio de consciência do leitor** — classifique em um dos 5:
 - Completamente inconsciente (não sabe que tem o problema)
 - Consciente do problema (sabe do problema, não conhece solução)
 - Consciente da solução (sabe que soluções existem, não conhece esta marca)
 - Consciente do produto (conhece a marca, não está convencido)
 - Mais consciente (já quer, falta o empurrão final — geralmente é aqui que oferta/preço/urgência decidem)

 A abertura do texto muda radicalmente dependendo da resposta — nunca abra com oferta/preço para quem está nos dois primeiros estágios.

2. **Sofisticação de mercado** — o mercado já viu essa promessa repetida por concorrentes?
 - Baixa sofisticação → pode usar promessa direta
 - Média → precisa de um mecanismo único ("como" a promessa é entregue de um jeito diferente)
 - Alta → promessa direta já não funciona; focar em identificação, prova ou uma reformulação completa do ângulo

Consulte `references/schwartz-diagnostico.md` para o checklist completo com exemplos.

---

## FASE 2 — Validação e estrutura (Halbert)

1. **Teste da "multidão faminta"**: antes de investir na copy, valide com o usuário se existe demanda real e urgente — não existe copy que salve uma oferta para um mercado que não quer o produto. Se o usuário não souber responder, pergunte diretamente (ex: "existe alguma evidência de que esse público já procura ativamente por isso — buscas, perguntas repetidas, concorrentes vendendo bem?").
2. **Pesquisa mínima antes de escrever**: mesmo em pedidos curtos, pergunte por 2-3 informações concretas sobre o público/oferta antes de escrever (dor principal, objeção mais comum, prova/resultado real). Nunca invente estatísticas, depoimentos ou resultados que o usuário não forneceu — sinalize como placeholder se faltar.
3. **Estrutura AIDA** como esqueleto do texto:
 - Attention — abertura que quebra o padrão, sem rodeios
 - Interest — sustentar com um fato, história ou tensão relevante
 - Desire — construir o benefício de forma vívida e específica
 - Action — fechar com oferta e chamada clara (e urgência real, nunca fabricada)
4. **Edição implacável**: depois do primeiro rascunho, corte tudo que não avança a leitura — frases que não geram curiosidade para a próxima linha, jargão, qualificadores fracos ("nós acreditamos que talvez...").

Consulte `references/halbert-estrutura.md` para o checklist de validação e o template AIDA detalhado.

---

## FASE 3 — Linguagem real (Wiebe / VoC)

1. **Pergunte por fontes de linguagem real do cliente**: reviews, tickets de suporte, transcrições de chamadas de venda, respostas de pesquisa NPS, comentários em redes sociais. Se o usuário colar esse material, use-o. Se `brand-voice.md` tiver amostras de copy, use-as como fonte primária.
2. **Minere frases emocionalmente carregadas**, não só informativas — a frase que descreve o *sentimento* do resultado (ex.: "finalmente parei de me sentir perdido com isso") vale mais que uma frase técnica (ex.: "interface intuitiva").
3. **Prefira a palavra do cliente à palavra do departamento de marketing** sempre que ambas estiverem disponíveis — teste lado a lado se for um teste A/B.
4. **Se não houver dados de VoC disponíveis**, não invente citações. Diga isso ao usuário e ofereça duas saídas: (a) escrever com a melhor linguagem possível baseada no que ele descreveu sobre o público, sinalizando que idealmente seria validada com dados reais depois; ou (b) sugerir 3-5 perguntas que ele poderia fazer a clientes reais para coletar VoC antes da versão final.

Consulte `references/wiebe-voc.md` para o processo de mineração e exemplos de antes/depois.

---

## FASE 4 — Entrega

Ao entregar a copy final:

1. Mostre o texto pronto.
2. Em 2-3 linhas, explique as decisões-chave tomadas (estágio de consciência assumido, ângulo de sofisticação, se a linguagem veio de VoC real ou foi inferida).
3. Se algo foi assumido por falta de informação (prova, depoimento, estatística), sinalize claramente como placeholder a ser substituído por dado real antes de publicar.
4. Se o pedido for de formato curto, não force as três camadas em texto explicativo longo — a explicação deve ser proporcional ao tamanho do pedido.

---

## Passo Final — Salvar output

Depois da copy aprovada pelo usuário, salve em:

```
{pasta-ativa}/egreen-copywriting/{YYYY-MM-DD-descricao-curta}.md
```

Exiba a confirmação:

```
✅ Salvo em: {pasta-ativa}/egreen-copywriting/{YYYY-MM-DD-descricao-curta}.md

Próximo passo: {sugestão, ex: usar em /egreen-mandala ou /egreen-emails}
```

Se o pedido foi de formato muito curto (uma headline, um CTA isolado), ainda assim salve — a memória de copy avulsa aprovada é útil para reaproveitar em outras peças do mesmo produto.

---

## Notas de estilo

- Nunca fabricar depoimentos, números, estatísticas ou resultados de clientes que não foram fornecidos pelo usuário.
- Urgência e escassez na copy devem refletir uma condição real informada pelo usuário (prazo, estoque, vaga) — nunca fabricar urgência falsa.
- Adaptar o tom/vocabulário ao canal (e-mail, anúncio, página de vendas, script de vídeo) mesmo mantendo a mesma espinha dorsal AIDA.
- Se o usuário pedir explicitamente um arquivo (Word, PDF, apresentação), gerar a copy nesse formato usando a skill de documento apropriada; caso contrário, entregar direto na conversa (e salvar o Markdown conforme o Passo Final).
