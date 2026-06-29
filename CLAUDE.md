# Evergreen — Agentic OS para Marketing Digital de Infoprodutos

## O que é este projeto

Sistema de skills para criação e venda de infoprodutos. Cada skill representa uma atividade do pipeline de marketing, invocada via slash command. Idioma de trabalho: **português brasileiro**.

---

## REGRA 0 — Estrutura multi-produto

Cada produto criado no Evergreen vive em sua própria pasta raiz (`produto-01/`, `produto-02/`, etc.).
O produto ativo é sempre indicado por `memoria/produto-ativo.md`.

```
memoria/
  formatos.md          ← referência permanente do OS (nunca apagar)
  produto-ativo.md     ← aponta para a pasta do produto em uso
produto-01/
  memoria/             ← nicho.md, produto.md, funil.md, design.md deste produto
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
produto-02/            ← criado pelo próximo /egreen-setup
  ...
```

**Pasta ativa** = valor do campo `produto:` em `memoria/produto-ativo.md`.
Todas as skills usam `{pasta-ativa}/` como raiz para leitura e escrita.

---

## REGRA 1 — Gate de instalação (verificar ANTES de qualquer skill)

1. Leia `memoria/produto-ativo.md` para obter a pasta ativa (ex: `produto-01`).
2. Verifique os arquivos de memória do produto ativo:

```
{pasta-ativa}/memoria/nicho.md
{pasta-ativa}/memoria/produto.md
{pasta-ativa}/memoria/funil.md
```

Se `memoria/produto-ativo.md` não existir, ou se qualquer arquivo de memória
tiver `status: vazio` no frontmatter ou estiver ausente:

> **PARE.** O OS não está configurado.
> Execute `/egreen-setup` para realizar a entrevista inicial e configurar o projeto antes de usar outras skills.

---

## REGRA 2 — Carregar memória antes de qualquer skill

Após verificar o gate, leia TODOS os arquivos existentes em `{pasta-ativa}/memoria/` antes de executar a skill solicitada.

- `{pasta-ativa}/memoria/nicho.md`, `produto.md`, `funil.md` — contexto do produto ativo
- `memoria/formatos.md` — referência permanente dos formatos disponíveis (e-book, curso simples, curso completo, desafio, comunidade, mentoria)
- `{pasta-ativa}/memoria/design.md` — sistema de design do produto. Se existir, **toda skill visual deve carregá-lo antes de gerar qualquer output visual**
- `{pasta-ativa}/memoria/brand-voice.md` — voz de marca. Se existir, **toda skill de conteúdo de texto deve carregá-lo antes de gerar qualquer texto**

---

## REGRA 3 — Salvar output ao final de qualquer skill

Toda skill que gera conteúdo aprovado (pesquisa, concepção, copy, carrossel, landing page, etc.)
**deve automaticamente salvar o arquivo na pasta correta** ao concluir, sem esperar o usuário pedir.

O fluxo padrão de encerramento de qualquer skill é:

1. Conteúdo gerado e aprovado pelo usuário
2. Skill salva o arquivo em `{pasta-ativa}/{pasta-da-skill}/` (ver mapa abaixo)
3. Skill exibe confirmação com o caminho completo do arquivo salvo
4. Skill oferece próximo passo do pipeline

**Formato da confirmação obrigatória:**
```
✅ Salvo em: {pasta-ativa}/{pasta}/{YYYY-MM-DD-descricao-curta.ext}

Próximo passo: {skill ou ação sugerida}
```

Nunca encerrar uma skill sem ter salvo o output. Se o conteúdo não couber em um único arquivo,
salvar em múltiplos arquivos e listar todos na confirmação.

---

## Pipeline de Skills

Execute nesta ordem para um novo infoproduto:

| # | Slash Command | O que faz |
|---|---|---|
| 0 | `/egreen-setup` | Entrevista inicial, cria pasta produto-XX/, configura memoria/, pode invocar /egreen-funil |
| 0 | `/egreen-design` | Entrevista de marca, gera {pasta-ativa}/memoria/design.md (paleta, tipografia, componentes) |
| 0 | `/egreen-brand` | Entrevista de voz, gera {pasta-ativa}/memoria/brand-voice.md (tom, arquétipo, vocabulário, do/don't, amostras de copy). Execute antes de /egreen-copy |
| 1 | `/egreen-nicho` | Pesquisa, validação e posicionamento de nicho |
| 1.5 | `/egreen-pesquisa` | Pesquisa profunda de nicho em 9 eixos com busca real na web (opcional: `/egreen-produto` chama automaticamente; use direto para relatório completo + HTML com gráficos SVG) |
| 2 | `/egreen-produto` | Pesquisa nicho, gera 50 ideias em 15 formatos, usuário escolhe o produto |
| 2.5 | `/egreen-concepcao` | Concepção do produto escolhido: Promessa, 50 Benefícios, 5 Baldes, Identidade do Consumidor |
| 3 | `/egreen-funil` | Mapeia funil completo, gera opções de produtos |
| 4 | `/egreen-copy` | Copy completa de página de vendas em 15 blocos, padrão Light Copy (só texto, entrega Markdown no chat) |
| 4 | `/egreen-landing` | Página de vendas HTML completa |
| 4 | `/egreen-emails` | Sequências de email completas: Boas-vindas (5 emails), Nutrição (6 emails), Lançamento (9 emails) |
| 4 | `/egreen-mandala` | Anúncios argumentativos pela Mandala de Anúncios (4 tipos: Ultra Segmentado, Problema-Solução, Pesquisa Científica, Atualidades Trend) |
| 5 | `/egreen-carrossel` | Carrossel de curiosidade atemporal para Instagram (7-9 slides, 3 modos visuais) |
| 5 | `/egreen-editorial` | Carrossel editorial 6 slides (dados, pesquisa, polêmica, contas malucas) |
| 5 | `/egreen-slides` | Slides de apresentação |
| 6 | `/egreen-meta-auth` | Configura autenticação com Meta Ads (MCP OAuth ou App com token permanente no .env) |
| 6 | `/egreen-meta-ads` | Sobe campanha Meta Ads (Sales ou Leads), preview YAML obrigatório, status PAUSED por padrão |
| 6 | `/egreen-google-ads` | Campanhas Google Ads via MCP |
| 7 | `/egreen-analise` | Performance do funil: ROAS, CPL, CPA, email, scorecard 0-100, diagnóstico de vazamentos, plano de ação, relatório HTML |
| — | `/egreen-seo` | Auditoria completa SEO, GEO e AEO de qualquer URL (relatório .docx) |

---

## Mapa skill → pasta de output

Todos os caminhos são relativos à pasta do produto ativo (`{pasta-ativa}/`).

| Skill | Salva output em |
|---|---|
| `/egreen-setup` | `{pasta-ativa}/memoria/` e atualiza `memoria/produto-ativo.md` |
| `/egreen-design` | `{pasta-ativa}/memoria/` |
| `/egreen-brand` | `{pasta-ativa}/memoria/` |
| `/egreen-nicho` | `{pasta-ativa}/egreen-nicho/` |
| `/egreen-pesquisa` | `{pasta-ativa}/egreen-pesquisa/` |
| `/egreen-produto` | `{pasta-ativa}/egreen-pesquisa/` (tabela 50 ideias) |
| `/egreen-concepcao` | `{pasta-ativa}/egreen-concepcao/` |
| `/egreen-funil` | `{pasta-ativa}/egreen-funil/` |
| `/egreen-copy` | `{pasta-ativa}/egreen-copy/` |
| `/egreen-landing` | `{pasta-ativa}/egreen-landing/` |
| `/egreen-emails` | `{pasta-ativa}/egreen-emails/` |
| `/egreen-mandala` | `{pasta-ativa}/egreen-mandala/` |
| `/egreen-carrossel` | `{pasta-ativa}/egreen-carrossel/` |
| `/egreen-editorial` | `{pasta-ativa}/egreen-editorial/` |
| `/egreen-brand-carrossel` | `{pasta-ativa}/egreen-carrossel/` |
| `/egreen-slides` | `{pasta-ativa}/egreen-slides/` |
| `/egreen-meta-auth` | `{pasta-ativa}/egreen-meta-ads/` |
| `/egreen-meta-ads` | `{pasta-ativa}/egreen-meta-ads/` |
| `/egreen-google-ads` | `{pasta-ativa}/egreen-google-ads/` |
| `/egreen-analise` | `{pasta-ativa}/egreen-analise/` |
| `/egreen-seo` | `{pasta-ativa}/egreen-seo/` |

---

## Convenção de nomes de output

Todos os arquivos gerados pelas skills devem ser nomeados:

```
YYYY-MM-DD-descricao-curta.ext
```

Exemplo: `2026-05-30-carrossel-lancamento-curso.html`
