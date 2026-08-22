---
name: egreen-produto
description: >-
  Use quando o usuário disser que quer explorar ideias de produto digital, descobrir
  o que pode criar para sua especialidade, ou pedir uma lista de possíveis infoprodutos
  para um nicho. Também dispara com "que produto eu posso criar", "ideias de infoproduto",
  "o que eu posso vender", "quero explorar produtos", "me dá ideias de produto" ou qualquer
  variação que envolva gerar ou listar opções de infoproduto a partir de uma especialidade.
allowed-tools: Read, WebSearch, Write
model: sonnet
---

# Ideias de Produto Final

Skill autossuficiente. A partir da especialidade do usuário, faz a pesquisa de
mercado do nicho e entrega 50 ideias diversas de infoproduto em 15 formatos,
em UMA tabela agrupada por formato, salva automaticamente em `egreen-pesquisa/`.
Em seguida, quando o usuário escolhe uma das ideias, encerra orientando que ele
siga os próximos passos da aula do Leandro. Nada além disso. Sem concepção.

> **Idioma:** responda sempre em português do Brasil, com acentuação correta.
> **Travessão proibido** em qualquer texto gerado. Use vírgula, ponto ou dois
> pontos.
>
> **Para a metodologia detalhada da pesquisa, consulte o arquivo de referência
> `references/metodologia-vtsd.md`.** Esta skill usa apenas as Seções 1 e 2
> (princípios e Light Copy), Seção 4 (Pesquisa de Mercado) e Seção 6 (auto-
> revisão). Carregue esse arquivo antes de pesquisar.

---

## Fluxo

### Passo 0. Abertura e pergunta única

Esta skill não lê nenhum arquivo de configuração, `.env` nem produto ativo.
Comece direto pela pergunta única, sem rodeio nem menu de opções.

Use exatamente este texto:

```
Vou pesquisar o mercado do seu nicho e te entregar 50 ideias de infoproduto
em 15 formatos diferentes.

Qual é a sua especialidade? O que você ensina ou entrega para as pessoas?
(ex: "Tarô", "Emagrecimento feminino", "Marketing digital para pequenos negócios")
```

Aguarde a resposta. Não faça nenhuma outra pergunta antes dela.

### Passo 1. Pesquisa de mercado

Acione a skill `pesquisa-mercado` passando a especialidade informada como
nicho. Ela faz a pesquisa profunda dos 9 eixos com busca real na web. Se a
skill `pesquisa-mercado` não estiver disponível neste ambiente, faça a pesquisa
você mesmo seguindo a Seção 4 do arquivo de referência, com busca real na web
(no mínimo uma busca dedicada por eixo).

A pesquisa serve apenas como insumo para gerar as 50 ideias. Não é entregue
como relatório separado, não vira documento, não vira HTML. Antes de mandar a
tabela, mostre ao usuário UM parágrafo curto (3 a 5 linhas) com os achados que
vão guiar as ideias: dores dominantes do nicho, faixa de preço típica do
mercado e 1 ou 2 oportunidades de posicionamento mais claras. Esse parágrafo é
contexto, não relatório. Não cite os 9 eixos um por um.

### Passo 2. Tabela com 50 ideias

Com base na pesquisa, gere 50 ideias DIVERSAS de infoproduto. Não são
variações da mesma ideia, são 50 conceitos distintos entre si (ângulo, método,
público ou promessa diferentes). Use os temas do nicho que a pesquisa revelou:
dores que o público sofre, dúvidas que ele pesquisa, desejos que quer realizar,
assuntos adjacentes que consome. Evite ideias genéricas, busque ângulos
específicos e concretos do nicho pesquisado.

**Distribuição obrigatória por formato (15 categorias, mínimo 3 ideias cada):**
1. Mentoria em grupo
2. Mentoria individual
3. Curso gravado
4. Curso ao vivo (turma fechada)
5. Ebook
6. Template ou kit pronto
7. Consultoria
8. Comunidade paga (assinatura)
9. Workshop (evento curto e intensivo)
10. Serviço (feito para o cliente)
11. Agente GPT (assistente personalizado para uma dor do nicho)
12. Mini-SaaS ou ferramenta web (microaplicativo de página única)
13. Planilha pronta (cálculo, automação ou diagnóstico)
14. Checklist (lista validada passo a passo, baixo ticket)
15. Desafio (jornada de 3, 7, 21 ou 30 dias com entrega diária)

Garanta pelo menos 3 ideias em cada categoria. As 5 categorias finais (Agente
GPT, Mini-SaaS, Planilha, Checklist, Desafio) nunca podem ficar de fora, mesmo
em nicho pouco tecnológico. As 5 ideias restantes vão para as categorias com
maior aderência ao nicho pesquisado.

Apresente a lista agrupada por formato, com subtítulo por categoria e tabela:

```
### Mentoria em grupo

| # | Nome | Público-alvo resumido | Faixa de preço |
|---|------|----------------------|----------------|
| 1 | ... | ... | R$ ... |
```

Numeração contínua de 1 a 50, sem reiniciar a cada categoria. Use Light Copy
nas descrições (sem exageros, sem ponto de exclamação, sem travessão, sem
"mesmo que" nem "sem precisar").

### Passo 2B. Salvar tabela em `egreen-pesquisa/`

Imediatamente após exibir a tabela completa, salve o arquivo sem esperar aprovação do usuário.

Nome do arquivo: `YYYY-MM-DD-50-ideias-{slug-do-nicho}.md`
Slug: nicho em ASCII minúsculo, espaços viram hífen (ex: `genealogia-amadora`, `emagrecimento-feminino`).
Pasta: `egreen-pesquisa/`

Estrutura do arquivo:

```markdown
---
nicho: {especialidade informada}
gerado_por: /egreen-produto
gerado_em: YYYY-MM-DD
---

# 50 Ideias de Infoproduto — {especialidade}

{parágrafo de contexto do Passo 1}

{tabela completa com as 50 ideias, agrupada por formato, numeração 1-50}
```

Após salvar, exiba uma linha de confirmação:

```
✅ Salvo em: egreen-pesquisa/YYYY-MM-DD-50-ideias-{slug}.md
```

---

### Passo 3. Convite à escolha

Depois da tabela, em uma única linha, convide o usuário a escolher uma das 50
ideias. Use exatamente este texto:

```
Me diga o número (de 1 a 50) da ideia que mais te interessou. Se preferir
parar por aqui, é só dizer "encerrar".
```

Aguarde a resposta.

Aceite tanto número puro (ex: "12") quanto nome aproximado da ideia (ex:
"Acne sem Roacutan"). Se a resposta for ambígua, trouxer mais de uma ideia,
ou pedir uma ideia que não aparece na tabela, peça que confirme um único
número entre 1 e 50 antes de encerrar.

### Passo 4. Encerramento

Quando o usuário escolher uma ideia válida (número de 1 a 50, ou nome
aproximado que resolve para uma única ideia da tabela), responda usando
EXATAMENTE este texto, sem nenhum acréscimo, sem prefácio, sem repetir o
nome da ideia, sem comentário extra:

```
Ok agora siga os próximos passos de acordo com a orientação do Leandro na aula.
```

Se o usuário disser "encerrar", "não", "não quero", ou qualquer recusa clara,
responda com este texto:

```
Sem problema. Se mudar de ideia, abra um novo chat e seguimos a partir dali.
```

Não gere arquivo, não gere documento, não pergunte se o usuário quer
conceber agora. O texto de encerramento é o output final do chat.

---

## O que esta skill NÃO faz

Para evitar invenção de fluxos extras:

- Não conduz concepção do produto (Promessa, Identidade do Consumidor,
  promessa de valor, oferta).
- Não pede nome, tipo, preço, ou qualquer outro dado depois da especialidade
  e do número escolhido.
- Não gera arquivo além da tabela de 50 ideias (sem HTML, PDF, docx, relatório extra).
- Não repete o nome da ideia escolhida no encerramento, nem comenta a
  escolha. Apenas envia o texto exato do Passo 4.
- Não oferece prosseguir para outra fase no mesmo chat depois que o usuário
  fizer a escolha.

Depois que o usuário fizer a escolha, ele segue a aula do Leandro para os
próximos passos. Quem quiser conceber a ideia escolhida usa OUTRA skill, em
outro chat.
