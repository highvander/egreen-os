---
name: egreen-setup
description: >-
  Use quando o usuário acabou de clonar o repositório e quer configurar o EGreen OS, ou quando os arquivos de memória estiverem vazios e precisarem ser preenchidos.
  Dispara com "instalar", "setup inicial", "configurar o sistema", "primeiro uso", "rodar /egreen-setup", "novo produto", ou quando qualquer outra skill recusar por falta de configuração.
allowed-tools: Read, Write, Edit, Glob, Bash, AskUserQuestion, Skill
model: sonnet
---

# Instalar — Setup Inicial do EGreen OS

Cria uma pasta de produto nova (`produto-01/`, `produto-02/`, etc.), conduz entrevista sobre nicho e produto, preenche os arquivos de memória e desbloqueia o pipeline de skills. Nunca sobrescreve um produto existente.

Não faz pesquisa profunda — isso é trabalho de `/egreen-nicho` e `/egreen-produto`. Objetivo: coletar o mínimo necessário para liberar o gate em 5-8 minutos.

---

## Pré-check — Determinar pasta do novo produto

1. Liste as pastas existentes que correspondam ao padrão `produto-*/` na raiz do projeto.
2. Encontre o número mais alto (ex: se existem `produto-01/` e `produto-02/`, o próximo é `produto-03/`).
3. Se nenhuma existir, o próximo é `produto-01/`.
4. **Não perguntar ao usuário** — determinar automaticamente.

Guarde a pasta do novo produto (ex: `produto-03`) em memória para usar em todas as fases.

---

## Fase 1 — Nicho

Faça as 4 perguntas abaixo **uma por vez**, esperando a resposta antes de seguir.
Se a resposta for vaga, pedir concretude uma única vez. Registrar o que vier.

**Pergunta 1:**
> "Qual mercado você quer atuar?
> *(ex: saúde feminina, finanças pessoais, marketing digital, emagrecimento, relacionamento)*"

**Pergunta 2:**
> "Quem é o seu cliente ideal? Me descreva em 2-3 frases — não a persona de livro,
> o cliente real que você imagina atendendo."

**Pergunta 3:**
> "Qual a principal dor ou problema que você resolve para essa pessoa?
> O que tira o sono dela?"

**Pergunta 4:**
> "Você conhece concorrentes que já vendem para esse público?
> Quem você admira ou referencia nesse nicho?
> *(pode dizer 'nenhum ainda' se não souber)*"

---

## Fase 2 — Produto

**Pergunta 5:**
> "Você já tem um produto definido ou está criando do zero?"

**Pergunta 6 — Formato:**

> "Qual formato de produto você quer criar ou já tem?
>
> 1. E-book (R$37–97) — PDF, resolve problema específico, produção rápida
> 2. Curso Simples (R$97–497) — 3-7 aulas em vídeo, área de membros
> 3. Curso Completo (R$700–2.500+) — 30-60+ módulos, plataforma completa
> 4. Desafio 7-21 dias (R$37–297) — missões diárias, WhatsApp/Telegram
> 5. Comunidade (R$297–997/mês) — recorrente, canais temáticos, networking
> 6. Mentoria (R$2k–25k+) — encontros ao vivo, acompanhamento direto
>
> Digite o número (ou descreva se for diferente):"

**Pergunta 7:**
> "Qual o ticket que você imagina cobrar? (em R$)
> *(pode ser uma faixa, ex: entre R$197 e R$297)*"

**Pergunta 8:**
> "Em uma frase: qual a transformação que o seu produto entrega?
> Formato sugerido: 'Ajudo [quem] a [resultado] sem [objeção principal]'"

---

## Fase 3 — Funil

**Pergunta 9:**
> "Quer mapear o funil de vendas agora ou prefere deixar para depois?
>
> 1. Mapear agora (recomendado — invoca /egreen-funil)
> 2. Deixar para depois
>
> Digite o número:"

- **Opção 1:** invocar a skill `/egreen-funil`. O `egreen-funil.md` será preenchido por ela.
- **Opção 2:** salvar `{pasta-ativa}/memoria/egreen-funil.md` com `status: a-mapear` e seguir.

---

## Fase 4 — Criar estrutura de pastas e salvar memória

### 4A. Criar pastas do produto

Criar toda a estrutura de pastas para o novo produto:

```
{pasta-nova}/
  memoria/
  egreen-nicho/
  egreen-pesquisa/
  egreen-produto/
  egreen-concepcao/
  egreen-funil/
  egreen-copy/
  egreen-landing/
  egreen-mandala/
  egreen-carrossel/
  egreen-editorial/
  egreen-slides/
  egreen-meta-ads/
  egreen-google-ads/
  egreen-analise/
```

Usar Bash: `mkdir -p {pasta-nova}/memoria {pasta-nova}/01-nicho ...`

### 4B. Salvar `{pasta-nova}/memoria/egreen-nicho.md`

```markdown
---
status: preenchido
preenchido_por: /egreen-setup
atualizado_em: YYYY-MM-DD
---

# Nicho

**Mercado:** [resposta 1 — mercado amplo]
**Nicho:** [resposta 1 — especificação, se houver]

# Avatar

**Perfil:** [resposta 2]
**Dor principal:** [resposta 3]
**Desejos inferidos:** [derivar da dor, 2-3 pontos]
**Objeções comuns:** [inferir do nicho, 2-3 pontos]

# Referências de mercado

**Concorrentes / referências:** [resposta 4]
**Diferencial a explorar:** [inferir das respostas anteriores]
```

### 4C. Salvar `{pasta-nova}/memoria/egreen-produto.md`

```markdown
---
status: preenchido
preenchido_por: /egreen-setup
atualizado_em: YYYY-MM-DD
---

# Produto

**Nome:** [se informado, senão "a definir"]
**Formato:** [resposta 6]
**Ticket:** [resposta 7]
**Estágio:** [ideia | em desenvolvimento | pronto — inferir da resposta 5]

# Proposta de valor

**Transformação:** [resposta 8]
**Para quem:** [do avatar em egreen-nicho.md]
**Diferencial:** [inferir das respostas]

# Próximos passos

**Ação sugerida:** [ver Fase 5]
```

### 4D. Salvar `{pasta-nova}/memoria/egreen-funil.md` (quando opção 2 na Fase 3)

```markdown
---
status: a-mapear
preenchido_por: /egreen-setup
atualizado_em: YYYY-MM-DD
---

<!-- Funil ainda não mapeado. Execute /egreen-funil para mapear. -->
```

### 4E. Atualizar `memoria/egreen-produto-ativo.md`

Sobrescrever com o novo produto ativo:

```markdown
---
produto: {pasta-nova}
nome: [nome do produto, ou nicho se nome for "a definir"]
atualizado_em: YYYY-MM-DD
---
```

---

## Fase 5 — Resumo e próximos passos

Mostrar confirmação com o que foi configurado:

```
✓ {pasta-nova}/memoria/egreen-nicho.md — preenchido
✓ {pasta-nova}/memoria/egreen-produto.md — preenchido
✓ {pasta-nova}/memoria/egreen-funil.md — [preenchido via /egreen-funil | marcado para mapear]
✓ memoria/egreen-produto-ativo.md — aponta para {pasta-nova}

Produto "{nome}" configurado em {pasta-nova}/.
O EGreen OS está pronto para usar.
```

Em seguida, sugerir o próximo passo com base no estado do produto:

**Se produto está em estágio "ideia" ou "a definir":**
> "Próximo passo: `/egreen-produto` — pesquisa o nicho a fundo e gera 50 ideias de produto
> em 15 formatos para você escolher."

**Se produto está definido mas sem concepção:**
> "Próximo passo: `/egreen-concepcao` — define a promessa central, 50 benefícios,
> 5 baldes de conteúdo e a identidade do consumidor."

**Se produto está pronto e funil não mapeado:**
> "Próximo passo: `/egreen-funil` — mapeia o funil completo com opções de front-end,
> order bump, OTO e sequência de email."

**Se tudo preenchido:**
> "Próximo passo: `/egreen-nicho` para validar o posicionamento com pesquisa real,
> ou `/egreen-landing` para criar a página de vendas."

Mencionar `/egreen-design` se identidade visual ainda não foi configurada:
> "Quando tiver logo e cores definidas, rode `/egreen-design` para configurar
> o sistema de design — carrosseis e landing pages vão usar automaticamente."

---

## Regras

1. Perguntar **uma coisa por vez** — nunca enfileirar perguntas
2. **Nunca sobrescrever pasta de produto existente** — sempre criar pasta nova com próximo número
3. Registrar **o que vier** — se a resposta for vaga, inferir e deixar claro que inferiu
4. Não inventar dados — marcar com "a definir" se o usuário não souber
5. **Não** fazer perguntas além das listadas — profundidade é tarefa das skills do pipeline
6. Setup deve levar no máximo 8 minutos
7. Ao salvar os arquivos, **remover os comentários HTML** de placeholder — substituir pelo conteúdo real
8. Atualizar `memoria/egreen-produto-ativo.md` **sempre** ao final — é o que todas as outras skills usam para saber onde escrever
