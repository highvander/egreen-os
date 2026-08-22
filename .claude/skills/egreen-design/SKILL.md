---
name: egreen-design
description: >
  Conduz entrevista de marca e gera o sistema de design completo do infoproduto
  em memoria/egreen-design.md. Cobre princípios, paleta com tokens CSS, tipografia,
  sistema de espaçamento/raio/sombra, componentes UI básicos, componentes de
  domínio do produto e aplicações principais (landing, carrossel, slides, email).
  Deve ser executada antes de qualquer skill visual. O arquivo gerado é lido
  automaticamente pela REGRA 2 do OS antes de cada skill.
---

# /egreen-design — Sistema de Design do Infoproduto

Skill que conduz uma entrevista de marca e gera `memoria/egreen-design.md` — o sistema de design completo do produto atual. Esse arquivo é lido automaticamente antes de qualquer skill visual (`/egreen-landing`, `/egreen-carrossel`, `/egreen-editorial`, `/egreen-slides`, `/egreen-pesquisa` HTML).

**Não gera HTML, não gera componentes de código.** Gera apenas o documento de sistema de design em Markdown, estruturado e rico, pronto para ser lido por outras skills como fonte única de verdade visual.

---

## O que esta skill faz

1. Conduz entrevista de marca em 10 perguntas (uma por vez).
2. Com base nas respostas, gera a paleta completa com tokens CSS, escala tipográfica, sistema de espaçamento e componentes aplicados ao produto.
3. Salva `memoria/egreen-design.md` com o sistema completo.
4. Instrui onde colocar os arquivos de marca em `memoria/assets/`.

---

## Passo 1 — Verificar memória existente

Antes de começar, leia `memoria/egreen-nicho.md` e `memoria/egreen-produto.md` se existirem. Use as informações já disponíveis para pular perguntas redundantes ou pré-preencher sugestões.

Verifique também se `memoria/egreen-design.md` já existe. Se existir, pergunte:

```
Um sistema de design já existe para este produto.

1. Atualizar o sistema atual (entrevista focada nas mudanças)
2. Recriar do zero (nova entrevista completa)
```

---

## Passo 2 — Entrevista de marca

Faça **uma pergunta por vez**. Aguarde a resposta antes de passar para a próxima. Se o usuário já forneceu a informação no contexto ou na memória, pule a pergunta e informe: "Já tenho [X] da memória do produto."

### Pergunta 1 — Identidade da marca

> "Qual o **nome da marca** e, em uma frase curta, qual é o conceito central dela? (ex: 'Linkme — conectar gerações através da genealogia')"

### Pergunta 2 — Produto e público

> "Quem compra este produto e qual transformação ele entrega? Uma frase cada. (ex: 'Adultos 40+ curiosos sobre a própria história. Saem sem saber nada de genealogia e chegam com a árvore familiar documentada.')"

### Pergunta 3 — Personalidade visual

> "Escolha **3 palavras** que descrevem a personalidade visual da marca. Exemplos: editorial · vivo · sóbrio · pop · técnico · acolhedor · premium · minimalista · vibrante · confiável · ousado · íntimo."

### Pergunta 4 — Cor principal

> "Qual a **cor principal da marca** (hex)? Se ainda não definiu, descreva a sensação que quer transmitir e eu sugiro opções."

### Pergunta 5 — Logo e arquivos de marca

> "Tem logo? Se sim, como se chama o arquivo? (ex: `logo.png`, `logo-branco.png`). Se não tem ainda, diga 'sem logo' e continuamos com wordmark em texto."

### Pergunta 6 — Tipografia

> "Tem preferência de fonte? Se não, diga o tom que quer (ex: 'serifada editorial', 'sans geométrica moderna', 'humanista amigável') e eu escolho e justifico."

### Pergunta 7 — Cores semânticas do domínio

> "No contexto do seu produto, quais estados ou categorias precisam de cor própria? Exemplos de outros produtos: 'confirmado / pendente / destaque / alerta'. Liste os que fazem sentido para o seu nicho."

### Pergunta 8 — Superfícies de aplicação

> "Em quais superfícies o design vai ser aplicado? Marque os que se aplicam:
> 1. Página de vendas (landing)
> 2. Carrossel Instagram
> 3. Slides de apresentação
> 4. Relatório HTML (pesquisa de mercado)
> 5. Email marketing
> 6. Área de membros / plataforma"

### Pergunta 9 — Direção editorial

> "Qual direção editorial combina mais com a marca?
> 1. **Pergaminho / Arquivo** — papel, editorial, sensação de curadoria, bordas finas, tipografia generosa
> 2. **Estúdio / Digital** — fundo branco limpo, sombras suaves, produto SaaS contemporâneo
> 3. **Energia / Pop** — cores cheias, contraste alto, ritmo visual acelerado
> 4. **Premium / Escuro** — fundos escuros, detalhes dourados ou luminosos, exclusividade"

### Pergunta 10 — Confirmação

Mostre um resumo antes de gerar:

```
Resumo da marca antes de gerar o sistema:

- Nome: [nome]
- Conceito: [frase]
- Público: [perfil]
- Transformação: [resultado]
- Personalidade: [3 palavras]
- Cor principal: [hex] — [nome da cor]
- Logo: [arquivo ou "wordmark em texto"]
- Fonte: [família] — [justificativa em uma frase]
- Estados semânticos: [lista]
- Superfícies: [lista]
- Direção: [opção escolhida]

1. Gerar o sistema de design
2. Ajustar algo antes
```

---

## Passo 3 — Gerar o sistema de design

Com base nas respostas, gere o `memoria/egreen-design.md` completo, seguindo a estrutura abaixo. O nível de detalhe deve ser equivalente ao do exemplo de referência em `docs/egreen-design-exemplo.md` — com tokens CSS nomeados, escalas completas, regras de uso e componentes aplicados ao domínio do produto.

### Estrutura obrigatória do documento gerado

```markdown
# [Nome da Marca] — Sistema de Design

[Uma linha: produto, versão, mês/ano, status]

> [Parágrafo de 2-4 linhas descrevendo a essência visual da marca — o que o sistema comunica e por quê as escolhas fazem sentido para o produto e o público.]

---

## 1. Princípios

[4-5 princípios numerados. Cada um: título em negrito + 1-2 frases explicando a diretriz.
Exemplos: "A cor é gesto, não preenchimento.", "Densidade calma para público 40+."]

---

## 2. Marca

[Tabela: Variação | Arquivo | Quando usar]
[Incluir: logo principal, logo versão branca/escura, ícone/monograma se houver]
[Regra de tamanho mínimo. Fundos permitidos e proibidos.]

---

## 3. Cor

### 3.1 Primária — [Nome da cor principal]

[Tabela: Token | Hex | Uso]
[5 tokens: 500 (brand), 400 (hover), 600 (active), 100 (tag suave), 50 (focal)]
[Regra de proporção: máx % de tela, quando usar e quando não usar]

### 3.2 Cores semânticas de domínio

[Uma sub-seção por estado/categoria identificado na Pergunta 7]
[Tabela: Família | Token 500 | Hex | Significado]
[Cada família com ramps 100/300/500/700 para: tag suave, ícone, fundo cheio, texto]

### 3.3 Neutros

[Base de fundo (paper ou white). Cor de texto principal. Escala neutral-50 → neutral-900.]

---

## 4. Tipografia

**Família:** [Nome da fonte] — [link Google Fonts se open source] — [justificativa em 1 frase]
**Pesos disponíveis:** [lista de pesos]

### Escala

[Tabela: Token | px | Peso | Tracking | Uso]
[Tokens obrigatórios: Display, H1, H2, H3, Body, Small, Micro]

### Padrões de uso

[Bullet: quando usar itálico, quando usar tabular-nums, quando usar UPPERCASE eyebrow]
[Regras específicas para dados do domínio do produto]

---

## 5. Sistema

[Tabela: Categoria | Valores]
[Categorias: Espaço (grade de 4), Raio (sm/md/lg/xl/2xl/full), Sombra (xs/sm/md/lg/xl), Borda, Easing]
[Todas as sombras com viés de cor warm se fundo paper, frio se fundo branco puro]

---

## 6. Componentes UI

### Botão
[Variantes: primary / secondary / ghost / text]
[Tamanhos: sm / md / lg com medidas]
[Estados: default / hover / active / disabled / loading]
[Regras de ícone e gap]

### Formulário
[Input padrão: borda, raio, padding, fundo]
[Tratamento especial para campos do domínio do produto]
[Radio, checkbox]

### Tag
[Pílula: tamanho, raio, fonte]
[Tons disponíveis com seus significados (baseados nas cores semânticas §3.2)]

---

## 7. Componentes de domínio

[Específicos para o produto. 3-5 componentes de alto uso no produto]
[Cada componente: campos canônicos + variações Direção A / Direção B se aplicável]
[Ex para curso: Card de Módulo, Card de Aula, Barra de Progresso, Badge de Status]
[Ex para comunidade: Card de Membro, Feed de Post, Tag de Nível]
[Ex para e-book: Capa, Bloco de Citação, Callout de Destaque, Rodapé de Seção]

---

## 8. Aplicações

[Tabela: Superfície | Tamanho de design | Notas]
[Apenas as superfícies marcadas na Pergunta 8]
[Incluir especificações de canvas para cada superfície: px, orientação, notas de grid]

---

## 9. Arquivos de marca

[Instruções claras de onde colocar cada arquivo:]
[memoria/assets/logo.png — uso principal]
[memoria/assets/logo-branco.png — uso em fundos escuros]
[memoria/assets/favicon.png — 32×32px]
[memoria/assets/foto-autor.jpg — seção de autoridade]
[Lista outros arquivos relevantes para o produto]

[Se algum arquivo ainda não existe, marcar como: (pendente — soltar em memoria/assets/ quando tiver)]

---

## 10. Próximos passos

[3-5 itens numerados: o que ainda falta definir, criar ou testar]
[Ex: "Escolher direção Pergaminho vs Estúdio após visualizar mockups"]
[Ex: "Criar templates de email com a paleta definida"]
[Ex: "Definir variações de dark mode"]
```

---

## Passo 4 — Salvar e finalizar

Salve o documento gerado em `memoria/egreen-design.md`.

Após salvar, mostre ao usuário:

```
Sistema de design gerado e salvo em memoria/egreen-design.md.

Arquivos de marca esperados em memoria/assets/:
[lista dos arquivos esperados com instrução de cada um]

As skills /egreen-landing, /egreen-carrossel, /egreen-editorial, /egreen-slides e /egreen-pesquisa
vão carregar automaticamente o sistema de design antes de gerar qualquer output.

Próximos passos recomendados:
[lista dos próximos passos do §10 do documento gerado]
```

**Nada além disso.** Não ofereça próxima skill, não gere HTML, não crie componentes de código.

---

## Regras de geração

- **Tokens CSS nomeados são obrigatórios.** Não use hex soltos no documento — sempre defina o token primeiro e use o hex como referência da tabela. Ex: `--orange-500` `#E94F1D`, não só `#E94F1D`.
- **Escala de cor sempre com 5 níveis.** 50 (focal), 100 (tag suave), 300 (ícone/detalhe), 500 (brand/cheio), 700 (text-on-light ou active). Derivar matematicamente a partir do hex fornecido.
- **Escala tipográfica sempre com 7 tokens.** Display, H1, H2, H3, Body, Small, Micro. Sem exceção.
- **Grade de espaço baseada em múltiplos de 4.** `4, 8, 12, 16, 24, 32, 48, 64, 80, 96`.
- **Componentes de domínio obrigatórios.** Mínimo 3 componentes específicos do produto — não componentes genéricos de UI. Derivar do tipo de produto (curso, e-book, comunidade, mentoria, desafio).
- **Direção editorial deve ser consistente.** Se o usuário escolheu "Pergaminho", todos os exemplos de componente usam essa linguagem. Sem misturar direções.
- **Sombras com viés quente ou frio conforme o fundo.** Fundo paper (`#FBF6EB` ou similar) → sombras com `rgba(warm, _)`. Fundo branco puro → sombras neutras `rgba(0,0,0,_)`.
