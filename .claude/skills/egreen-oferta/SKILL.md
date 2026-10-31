---
name: egreen-oferta
description: >
  Monta a oferta completa do infoproduto em 7 blocos aprovados um a um: Mecanismo nomeado (Furadeira), Entregáveis em 9 categorias derivados das fases do método, Matriz de Objeções (nenhuma objeção fica sem resposta), Bônus que eliminam objeções específicas, Garantia, Stack de valor com preço e pagamento, e Consolidação. Inspirada na lógica do Gerador de Oferta do VTSD (Ladeira), com melhorias: lê a concepção da memória em vez de perguntar tudo de novo, checa custo de entrega × ticket, faz ancoragem completa (valor total vs preço), oferece opções de garantia e só permite urgência real. Use sempre que o usuário pedir "montar oferta", "criar bônus", "stack de valor", "qual garantia usar", "o que entregar no curso", "ancoragem de preço", "oferta irresistível", "/egreen-oferta" — mesmo sem citar VTSD. Roda depois de `egreen-concepcao` e antes de `egreen-copy`/`egreen-landing`/`egreen-vsl`. Não escreve copy de página: entrega a oferta estruturada que a copy vai vender.
---

# Oferta: Mecanismo, Entregáveis, Bônus, Garantia, Stack

Esta skill transforma a concepção do produto (Promessa, Benefícios, Consumidor) em uma **oferta fechada**: o que a pessoa recebe, por quanto, com qual segurança e por que vale mais do que custa.

Ela não escreve a página de vendas. Ela entrega a matéria-prima que `egreen-copy`, `egreen-landing`, `egreen-vsl`, `egreen-mandala` e `egreen-posvenda` usam.

---

## Regras globais

- **Aprovação bloco a bloco.** Apresente um bloco, espere aprovação ou ajuste, só então siga. Nunca junte dois blocos na mesma mensagem.
- **Uma pergunta por vez** quando precisar coletar algo.
- **Não pergunte o que já está na memória.** Reaproveite a concepção; pergunte só o que falta.
- **Urgência só se for real** (data de fechamento, vagas limitadas de verdade, bônus de fundador com prazo). Proibido contador falso, "últimas vagas" fictícias ou encerramento simulado em produto perpétuo.
- **Honestidade nos números.** Valores de referência de entregáveis e bônus não são preço comprovado; metas de resultado não são garantia. Diga isso no documento final.
- **Proibido** usar imagens aleatórias da web ou inventar depoimentos/resultados.
- Linguagem do EGreen: Promessa (não "Quadro"), Benefícios (não "Decorados"), Mecanismo (não "Furadeira"). Os termos VTSD podem aparecer entre parênteses na primeira menção.

---

## Passo 0 — Gate e memória

Aplique REGRA 1 e REGRA 2 do `CLAUDE.md`. Depois leia:

```
memoria/produto-ativo.md                       → pasta ativa
memoria/formatos.md                            → faixa de preço e escopo por formato
{pasta-ativa}/memoria/egreen-produto.md        → produto, formato, preço
{pasta-ativa}/memoria/egreen-nicho.md          → público, dores
{pasta-ativa}/memoria/egreen-funil.md          → posição do produto na esteira, order bump/upsell previstos
{pasta-ativa}/memoria/brand-voice.md           → (se existir) tom dos nomes de bônus e entregáveis
{pasta-ativa}/memoria/egreen-argumentos.md     → (se existir) Promessa, Mecanismo nomeado, objeções, urgências ocultas, Big Idea
{pasta-ativa}/egreen-concepcao/                → arquivo mais recente: Promessa, Benefícios, Baldes, Identidade do Consumidor, Escopo Mínimo Viável
{pasta-ativa}/egreen-curriculo/ ou egreen-experiencia/  → (se existir) módulos/missões já desenhados
{pasta-ativa}/egreen-pesquisa/                 → (se existir) concorrentes e preços praticados
```

Monte internamente os **5 insumos**:

| Insumo | Fonte preferida | Se faltar |
|---|---|---|
| Promessa | concepção | pergunte |
| Mecanismo (fases do método) | currículo/experiência, concepção | pergunte: "Quais são as etapas do seu método, do zero ao resultado?" |
| Identidade do Consumidor | concepção | pergunte |
| Objeções | concepção, pesquisa | pergunte: "Por que alguém do seu público NÃO compraria?" (peça 5 a 8) |
| Benefícios em 5 categorias: Financeiro, Tempo, Autoestima, Reputação, Crescimento | concepção (reclassifique) | complete com o usuário |

Mostre um resumo curto dos 5 insumos e confirme antes do Bloco 1. Se não houver concepção, recomende rodar `/egreen-concepcao` antes, mas aceite seguir coletando tudo aqui se o usuário preferir.

Defina a **faixa de ticket**, que guia o volume de entregáveis:
- **Low ticket:** até R$ 297
- **Mid ticket:** R$ 298 a R$ 997
- **High ticket:** acima de R$ 997

---

## Bloco 1 — Mecanismo nomeado

"Nomear cria realidade": um método com nome próprio parece único e defensável.

**Se `egreen-argumentos.md` já tem o Mecanismo nomeado (vindo da concepção), mostre nome + fases e peça só confirmação. Não gere opções novas.** Caso contrário:

1. Liste as fases do método (3 a 6), cada uma com verbo de ação e resultado parcial.
2. Proponha **5 nomes** para o método. Mistura de estilos: descritivo ("Método Varanda Produtiva"), sigla com sentido, metáfora, número + resultado ("Os 4 Passos da Colheita Contínua"), nome do expert + método.
3. Para cada nome: uma frase explicando por que funciona para esse público.
4. Recomende um. Aprovação.

---

## Bloco 2 — Entregáveis

Gere sugestões nas **9 categorias**, sempre **derivadas das fases do Mecanismo**:

| # | Categoria | Regra de geração |
|---|---|---|
| 1 | Aulas gravadas | 1 aula (ou módulo) por fase + 1 de abertura ou fechamento. Título com benefício + uma metáfora curta que torna a aula visual |
| 2 | Ao vivo / mentoria | Encontros coletivos, plantões, análises. Indique frequência |
| 3 | Modelos / templates | Documentos prontos para preencher |
| 4 | Checklists / guias rápidos | 1 por fase quando fizer sentido |
| 5 | Scripts / prompts | Textos prontos para falar, escrever ou usar com IA |
| 6 | Ferramentas | Calculadoras, planilhas, calendários, diários |
| 7 | Suporte / comunidade | Grupo, canal de dúvidas, troca entre alunos |
| 8 | Portfólio / casos reais | Exemplos, antes e depois (só se houver casos reais ou se forem produzidos de verdade) |
| 9 | Desafios / missões | 1 missão por fase com nome gamificado e ação concreta |

Feche cada categoria com uma frase de valor (o que aquilo poupa ao aluno).

### Recomendação de pacote
Recomende uma seleção enxuta conforme o ticket. Low ticket: foco em aulas + materiais de consulta + missões. High ticket: acompanhamento ao vivo e ferramentas ganham peso.

### Checagem de custo de entrega (obrigatória)
Para cada item ao vivo ou individual, estime horas do expert por mês e diga se escala no ticket:

```
⚠️ Custo de entrega: "Plantão ao vivo mensal" = ~2h/mês do expert.
   Com 300 alunos a R$ 97, ok se for coletivo; inviável se for individual.
```

Peça ao usuário para escolher os entregáveis (lista numerada; ele responde com os números ou ajustes). Aprovação.

---

## Bloco 3 — Matriz de objeções

Tabela com **todas** as objeções dos insumos (se existir `egreen-argumentos.md`, comece pelas objeções principais e secundárias de lá e reaproveite o argumento mais forte como resposta):

| Objeção | Resposta (argumento) | Onde é respondida |
|---|---|---|
| "Minha varanda não pega sol" | Há folhas e temperos que crescem com 3h de luz indireta | Bônus 1 + FAQ |
| "Vai sujar o apartamento" | Vaso autoirrigável fechado não escorre água | Aula 2 + FAQ |

Destinos possíveis: entregável, bônus, garantia, FAQ, copy (headline, dor, prova), anúncio.

Regras:
- **Nenhuma objeção órfã.** Toda objeção tem pelo menos um destino.
- Objeções que nenhum entregável resolve viram **candidatas a bônus** no Bloco 4.
- Objeção de preço ("é caro") nunca vira bônus: é respondida no Stack (Bloco 6) e na garantia.

Aprovação.

---

## Bloco 4 — Bônus

Pergunte antes: "Você já tem algum bônus pronto ou crio do zero?" Se tiver, encaixe e complete até 3.

Para cada bônus (padrão: 3):

```
BÔNUS {N} — {Nome}
O que é: {formato e uma frase}
O que inclui: {3 a 5 itens}
Objeção eliminada: "{objeção exata da matriz}"
Valor de referência: R$ {X}  ({base: preço de material similar, horas de trabalho, etc.})
Custo de produção: {baixo/médio/alto} — {o que precisa ser feito}
```

Regras:
- Bônus **acelera, facilita ou protege** o resultado. Não é conteúdo aleatório para inflar valor.
- Bônus não pode ser mais desejado que o produto principal (senão a pessoa compra pelo bônus e pede reembolso).
- Prefira bônus de baixo custo de produção em low ticket.
- Se houver Pico de Vendas ou lançamento, marque quais bônus são **temporários de verdade** (podem ser usados como urgência real).

Aprovação.

---

## Bloco 5 — Garantia

Apresente 3 opções com prós e contras para este ticket e esta objeção principal:

| Tipo | Como funciona | Quando usar |
|---|---|---|
| Incondicional | X dias, reembolso sem justificativa (mínimo legal de 7 dias no Brasil para compra online) | Low ticket, público desconfiado, padrão de mercado |
| Condicional por ação | "Fez todas as missões e não teve resultado X? Devolvo" | Mid/high ticket, quando o resultado depende de execução |
| Dupla | Incondicional curta + condicional longa | Quando a objeção principal é "não vai funcionar para mim" |

Recomende uma e explique por quê. Pergunte também o **tempo de acesso** (6 meses, 1 ano, vitalício) e recomende conforme custo de hospedagem e atualização.

Garantia de resultado financeiro ("ganhe X ou devolvo") só se o usuário puder cumprir de verdade; nunca sugira por padrão.

Aprovação.

---

## Bloco 6 — Stack, preço e pagamento

### 1. Sanity check de preço
- Compare o preço informado com: valor da transformação (benefício financeiro/tempo dos insumos), faixa do formato em `formatos.md`, preços de concorrentes (se houver pesquisa).
- Se o preço parecer desalinhado, **sugira** ajuste com justificativa em 2 linhas. A decisão é do usuário.

### 2. Stack de valor
Tabela com **todos** os entregáveis escolhidos + bônus:

| Item | Valor de referência |
|---|---|
| Método {Nome} — {N} aulas | R$ ... |
| ... | ... |
| Bônus 1 — ... | R$ ... |
| **Valor total de referência** | **R$ ...** |
| **Preço** | **R$ ...** |
| **Razão de valor** | **{total ÷ preço}x** |

Mire em razão de valor entre 5x e 10x. Abaixo de 3x: a oferta precisa de mais valor (ou o preço está alto). Acima de 20x: os valores de referência perderam credibilidade, reduza.

### 3. Ancoragem pelo resultado
Uma frase comparando preço com o benefício financeiro ou de tempo dos insumos ("R$ 97 = menos de 2 meses da economia na feira").

### 4. Pagamento
Pergunte: Pix, cartão (quantas parcelas), boleto. Mostre o valor da parcela aproximado ("12x de ~R$ 9,90, sujeito a juros da plataforma").

### 5. Urgência (opcional)
Pergunte se existe algum motivo **real** para comprar agora: preço de lançamento com data, turma com vagas limitadas de verdade, bônus temporário. Se não existir, a oferta segue sem urgência de prazo e a copy trabalha o custo da inação, usando as Urgências Ocultas de `egreen-argumentos.md` quando houver.

Aprovação.

---

## Bloco 7 — Consolidação

Documento final, nesta ordem:

1. **Promessa** (uma frase)
2. **Mecanismo** — nome + fases
3. **Entregáveis** — por categoria, com frase de valor
4. **Bônus** — nome, o que inclui, objeção eliminada
5. **Stack de valor** — tabela + razão de valor + ancoragem pelo resultado
6. **Garantia** — tipo, prazo, tempo de acesso
7. **Preço e pagamento** — condições, urgência real (se houver)
8. **Matriz de objeções** — tabela completa (a copy usa no FAQ)
9. **Big Idea da oferta** — 1 parágrafo: "Você não está vendendo X, está oferecendo Y"
10. **Próximos passos sugeridos** — order bump e upsell derivados desta oferta (ideia de 1 linha cada, para `/egreen-posvenda`)
11. **Ressalvas** — valores de referência não são preço comprovado; metas não são resultado garantido

---

## Passo Final — Salvar output

Salve dois arquivos:

```
{pasta-ativa}/egreen-oferta/{YYYY-MM-DD}-oferta-{produto-slug}.md    → documento completo do Bloco 7
{pasta-ativa}/memoria/egreen-oferta.md                               → resumo para as outras skills
```

O resumo em memória tem frontmatter `status: aprovado` e as seções: Promessa, Mecanismo, Entregáveis (lista), Bônus (nome + objeção), Stack (total, preço, razão), Garantia, Pagamento, Urgência real, Matriz de objeções. Se já existir, sobrescreva (a oferta aprovada mais recente vale).

Confirmação:
```
✅ Salvo em: {pasta-ativa}/egreen-oferta/{YYYY-MM-DD}-oferta-{produto-slug}.md
✅ Memória atualizada: {pasta-ativa}/memoria/egreen-oferta.md

Próximo passo: /egreen-copy (página de vendas usando esta oferta)
```

---

## Notas de estilo

- Nomes de entregáveis e bônus concretos e visuais ("Guia Varanda Sem Sol"), nunca genéricos ("Material Extra").
- Frases curtas. Sem exagero ("revolucionário", "incrível", "garantido").
- Valores sempre em R$ com base explicada.
- Se `brand-voice.md` existir, nomes e frases de valor seguem o tom dele.
