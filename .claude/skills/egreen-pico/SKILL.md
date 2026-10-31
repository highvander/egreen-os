---
name: egreen-pico
description: >
  Planeja e roteiriza um Pico de Vendas para um produto perpétuo (Fase 5 do VTSD): um evento com data marcada (aulas ao vivo, live única ou desafio) somado a uma mudança temporária e REAL na oferta (bônus exclusivos, condição de pagamento, sessões ao vivo), que gera um pico de faturamento sem mexer na oferta base. Entrega em 6 blocos aprovados um a um: Definições do pico (tipo, nome, tema, calendário, mudança na oferta, metas com cálculo reverso de leads), Roteiro das aulas, Copy da página de inscrição, Sequência de e-mails do pico (convite, confirmação, aquecimento, lembretes, pré-abertura, carrinho aberto, encerramento, via `egreen-emails`), Plano de apoio (stories, anúncios, página de vendas do pico) e Cronograma mestre. Proíbe escassez falsa: tudo que "acaba" precisa acabar de verdade. Use sempre que o usuário pedir "pico de vendas", "evento de vendas", "semana de aulas", "fazer uma live de vendas", "campanha com bônus por tempo limitado", "aulas para vender o curso", "e-mails de convite/lembrete/carrinho aberto", "/egreen-pico" — mesmo sem citar VTSD. Pré-requisito: oferta base definida (`/egreen-oferta`).
---

# Pico de Vendas

Um Pico de Vendas é uma janela curta e datada em que o produto perpétuo ganha **uma condição melhor e real**, apresentada num **evento** que gera atenção concentrada. O produto e a oferta base não mudam; muda o que existe só dentro da janela.

Esta skill planeja o pico inteiro e roteiriza as peças centrais. As peças longas são escritas pelas skills especializadas, chamadas no momento certo:

| Peça | Quem escreve |
|---|---|
| Definições, aulas, página de inscrição, cronograma | esta skill |
| E-mails do pico | `egreen-emails` (Sequência 4 — Pico), com os dados desta skill |
| Pitch da última aula ou VSL do pico | `egreen-vsl` (Rota A — Webinar) |
| Página de vendas do pico | `egreen-copy` + `egreen-landing` com a oferta do pico |
| Stories da captação e do carrinho | `egreen-stories` |
| Anúncios de captação | `egreen-mandala` |

---

## Regras globais

- **Aprovação bloco a bloco.** Um bloco por mensagem. Não avance sem aprovação.
- **Uma pergunta por vez** quando precisar coletar algo.
- **Escassez só se for real.** Tudo que a comunicação diz que "acaba" precisa acabar de verdade na data dita: bônus, condição, preço, vagas. Proibido contador falso, reabrir carrinho "por demanda" depois de dizer que fechou para sempre, vagas inventadas.
- **Aula entrega valor de verdade.** O conteúdo das aulas resolve uma parte real do problema (uma fase do Mecanismo). Aula que é só pitch disfarçado derruba comparecimento da aula seguinte.
- **Light Copy:** argumentativa, específica, sem promessa vaga, sem sensacionalismo.
- **Números honestos.** Metas e taxas de conversão são estimativas de planejamento, não previsão garantida. Diga isso no documento.

---

## Passo 0 — Gate e memória

Aplique REGRA 1 e REGRA 2 do `CLAUDE.md` e leia:

```
memoria/produto-ativo.md                       → pasta ativa
{pasta-ativa}/memoria/egreen-produto.md        → produto, formato, preço
{pasta-ativa}/memoria/egreen-nicho.md          → público
{pasta-ativa}/memoria/egreen-funil.md          → posição na esteira, order bump, upsell
{pasta-ativa}/memoria/egreen-oferta.md         → oferta base (entregáveis, bônus, garantia, stack)
{pasta-ativa}/memoria/egreen-argumentos.md     → promessa, mecanismo, Big Idea, inimigo, objeções, urgências ocultas
{pasta-ativa}/memoria/brand-voice.md           → (se existir) tom
{pasta-ativa}/memoria/egreen-pico.md           → (se existir) pico anterior: aprender com ele
{pasta-ativa}/egreen-analise/                  → (se existir) taxas reais de conversão de campanhas anteriores
```

**Sem `egreen-oferta.md`:** avise que o pico precisa de uma oferta base aprovada e recomende `/egreen-oferta` antes. Se o usuário quiser seguir mesmo assim, colete em uma pergunta: entregáveis principais, preço, garantia.

Depois pergunte, uma por vez, só o que não estiver na memória:

1. **Base de contatos hoje:** tamanho da lista de e-mail, seguidores no Instagram, grupo de WhatsApp (números aproximados).
2. **Vai investir em anúncio para captação?** Se sim, orçamento aproximado.
3. **Já fez algum pico ou lançamento?** Se sim, resultados (inscritos, comparecimento, vendas).
4. **Data desejada** para o pico (ou "quero que você sugira").

---

## Bloco 1 — Definições do pico

### 1. Tipo de evento
Recomende um, explicando por quê, com base no ticket, no tamanho da base e no formato do produto:

| Tipo | Como é | Quando usar |
|---|---|---|
| **Série de aulas** (3 aulas em 3 a 7 dias) | Aulas ao vivo ou estreias gravadas, oferta abre na última | Padrão. Mid e high ticket, base pequena a média |
| **Live única** (60 a 120 min) | Uma aula longa com pitch no final | Low ticket, base pequena, primeiro pico |
| **Desafio** (5 a 7 dias) | Uma missão por dia, oferta abre no último dia | Produtos de hábito ou execução (desafio, comunidade) |
| **Janela sem evento** (3 a 5 dias) | Só condição especial comunicada por e-mail e stories | Base aquecida, intervalo curto desde o último pico |

### 2. Nome e tema do evento
- 5 opções de nome (curtos, com resultado ou cena, ex: "Semana da Varanda Produtiva").
- Tema ligado à **Big Idea** e ao **Mecanismo**: as aulas ensinam de verdade uma ou duas fases do método.

### 3. Mudança temporária na oferta (o motivo real para comprar agora)
Proponha 2 ou 3 combinações. Opções:
- **Bônus exclusivos do pico** (só para quem compra na janela; depois saem da oferta)
- **Sessão ao vivo** com o expert (mentoria em grupo, plantão, análise) só para a turma do pico
- **Condição de pagamento** (mais parcelas, desconto no Pix) com data de fim
- **Preço especial** com data de fim, voltando ao preço normal depois
- **Bônus de ação rápida** para as primeiras 24h (real, com horário de corte)

**Teste de realidade obrigatório** para cada item: "Depois da data de fechamento, isso volta ao normal ou deixa de existir?" Se a resposta for "não, continua igual", o item não pode ser usado como urgência.

Também verifique o **custo de entrega** de itens ao vivo (horas do expert × número de compradores esperado).

### 4. Calendário
Monte a linha do tempo com datas reais (use a data desejada ou sugira uma, evitando feriados e fins de semana para aulas):

```
Captação        D-14 a A1-1    anúncios, conteúdo, e-mails de convite
Aquecimento     após inscrição e-mails pós-cadastro, grupo
Aulas           A1, A2, A3     (horário fixo, ex: 20h)
Pré-abertura    entre A2 e A3  antecipa que a condição especial vem aí
Carrinho aberto C0 (fim da A3) a C0+3 ou C0+5
Encerramento    C-final, hora definida (ex: 23h59)
```

### 5. Metas com cálculo reverso
Pergunte quantas vendas o usuário quer (ou sugira a partir da base). Calcule para trás, usando taxas reais de `egreen-analise/` se houver; senão, use faixas de referência e marque como estimativa:

```
Vendas desejadas:              {V}
Conversão de quem assistiu:    {c}%   (referência: 3% a 10%)
Assistentes necessários:       V ÷ c
Comparecimento dos inscritos:  {a}%   (referência: 20% a 40% ao vivo)
Inscritos necessários:         assistentes ÷ a
Inscritos vindos da base:      {estimativa a partir da lista e seguidores}
Inscritos a captar com anúncio: diferença
Custo por inscrito estimado:   R$ {x}  → orçamento necessário: R$ {y}
```

Se o orçamento necessário passar do que o usuário disse que tem, diga claramente e proponha ajuste (meta menor, mais tempo de captação, mais conteúdo orgânico).

Aprovação.

---

## Bloco 2 — Roteiro das aulas

Para série de 3 aulas (adapte para live única: os 3 atos viram 3 blocos de uma aula só; para desafio: uma missão por dia seguindo a mesma progressão):

| Aula | Função | Conteúdo |
|---|---|---|
| **Aula 1 — A virada** | Mudar como a pessoa vê o problema | Big Idea, inimigo, por que as tentativas anteriores falharam, visão geral do Mecanismo, primeira vitória rápida |
| **Aula 2 — O método na prática** | Provar que funciona e que ela consegue | 1 ou 2 fases do Mecanismo ensinadas de verdade, caso real, tarefa prática para fazer até a aula 3 |
| **Aula 3 — O caminho completo** | Mostrar o resto do caminho e abrir a oferta | Revisão da tarefa, o que falta para a Promessa, objeções respondidas, apresentação da oferta do pico |

Para cada aula entregue:

```
AULA {N} — {Título com benefício}
Data e hora: {…}   Duração: {…} min
Promessa da aula: "Ao final desta aula você vai {resultado concreto}."
Estrutura:
  00–05  Abertura: {gancho, quem é o expert em 2 frases, regra do jogo}
  05–xx  {bloco de conteúdo}
  xx–xx  {bloco de conteúdo}
  xx–xx  Engajamento: {pergunta para o chat / enquete}
  xx–fim Fechamento: {tarefa} + {gancho para a próxima aula}
Objeção trabalhada: "{objeção de egreen-argumentos.md}"
Urgência oculta usada: "{urgência de egreen-argumentos.md}"
Tarefa: {ação concreta até a próxima aula}
```

Na **Aula 3**, o bloco de oferta segue o roteiro de pitch do `egreen-vsl` (Rota A). Diga ao usuário que esse trecho será escrito por `/egreen-vsl` com a oferta do pico, e entregue aqui só a passagem de conteúdo para oferta (a "ponte").

Aprovação.

---

## Bloco 3 — Página de inscrição

Copy curta, para captação:

```
Pré-headline: {para quem é, 1 linha}
Headline: {nome do evento + resultado}
Subheadline: {datas, formato, gratuito}
O que você vai aprender:
  • Aula 1 — {promessa da aula 1}
  • Aula 2 — {promessa da aula 2}
  • Aula 3 — {promessa da aula 3}
Para quem é: {3 bullets a partir dos Baldes da concepção}
Quem conduz: {release curto do expert, 2 a 3 linhas}
CTA: {texto do botão}
Campos do formulário: nome, e-mail, WhatsApp (opcional, com consentimento explícito)
Página de obrigado: {próximo passo único: entrar no grupo ou adicionar na agenda}
```

Gere 3 opções de headline. Inclua o aviso de consentimento LGPD no formulário.
Para a versão em HTML, indique `/egreen-landing` (Modo Captura) usando esta copy. Se o usuário quiser a copy salva no formato padrão de captura, ela também pode ser gerada por `/egreen-copy` (Modo Captura, tipo "evento de pico").

Aprovação.

---

## Bloco 4 — Sequência de e-mails do pico

Monte o **briefing** e invoque `egreen-emails` com a Sequência 4 — Pico:

```
Evento: {nome}   Tipo: {tipo}
Aulas: A1 {data hora}, A2 {data hora}, A3 {data hora}
Link de inscrição: {placeholder}   Link das aulas: {placeholder}
Carrinho: abre C0 {data hora}, fecha {data hora}
Oferta do pico: {oferta base + mudança temporária real}
O que acaba e quando: {item → data/hora}
Objeções prioritárias: {3}
Urgências ocultas a usar: {2 ou 3}
```

Se o usuário preferir não chamar a outra skill agora, entregue só o briefing e o cronograma de envios (Bloco 6) e siga.

---

## Bloco 5 — Plano de apoio

Checklist com as peças complementares, quem faz e quando:

| Peça | Skill | Quando |
|---|---|---|
| Anúncios de captação (2 a 4 criativos, foco Descoberta e Relacionamento) | `/egreen-mandala` | Pronto antes de D-14 |
| Stories de captação (convite + bastidores) | `/egreen-stories` | Durante a captação |
| Stories do carrinho aberto (prova, objeção, fechamento no Inbox) | `/egreen-stories` | C0 até o fim |
| Pitch da Aula 3 / VSL do pico | `/egreen-vsl` | Antes da A1 |
| Página de vendas do pico (oferta base + condição do pico + data de fim) | `/egreen-copy` + `/egreen-landing` | Antes da A3 |
| Order bump / upsell para compradores do pico | `/egreen-posvenda` | Antes de C0 |
| Grupo de WhatsApp/Telegram dos inscritos (regras + mensagens-chave) | esta skill, se pedido | Antes da captação |

Recomende a ordem de produção conforme o prazo até A1. Aprovação.

---

## Bloco 6 — Cronograma mestre e consolidação

Tabela única, em ordem cronológica, com datas reais:

| Data | Hora | Fase | Ação / Peça | Canal | Status |
|---|---|---|---|---|---|
| {dd/mm} | — | Captação | Anúncios no ar | Meta Ads | a fazer |
| {dd/mm} | 9h | Captação | E-mail convite 1 | E-mail | a fazer |
| ... | | | | | |

Depois, documento final com: Definições (Bloco 1), Roteiro das aulas (Bloco 2), Página de inscrição (Bloco 3), Briefing de e-mails (Bloco 4), Plano de apoio (Bloco 5), Cronograma (Bloco 6), Metas e ressalvas.

**Pós-pico:** inclua no documento um checklist de análise para depois do fechamento: inscritos, comparecimento por aula, vendas por dia, conversão, CPL, ROAS, o que funcionou. Recomende `/egreen-analise` ao fim e salvar os números reais em `memoria/egreen-pico.md` para o próximo pico usar como referência.

---

## Passo Final — Salvar output

```
{pasta-ativa}/egreen-pico/{YYYY-MM-DD}-pico-{slug-do-evento}.md   → documento completo
{pasta-ativa}/memoria/egreen-pico.md                              → resumo do pico atual
```

O resumo em memória tem frontmatter `status: planejado` (depois `realizado`) e: nome, tipo, datas das aulas, janela de carrinho, oferta do pico, o que acaba e quando, metas e, após o pico, os números reais. As outras skills (e-mails, copy, stories, vsl) leem esse arquivo pela REGRA 2.

Confirmação:
```
✅ Salvo em: {pasta-ativa}/egreen-pico/{YYYY-MM-DD}-pico-{slug-do-evento}.md
✅ Memória atualizada: {pasta-ativa}/memoria/egreen-pico.md

Próximo passo: {primeira peça do plano de apoio pela ordem de produção, ex: /egreen-mandala para os anúncios de captação}
```

---

## Notas de estilo

- Nomes de evento e de aula concretos e visuais, nada de "Imersão Transformadora".
- Toda data no formato dd/mm (dia da semana) e hora de Brasília.
- Se `brand-voice.md` existir, títulos e copy seguem o tom dele.
