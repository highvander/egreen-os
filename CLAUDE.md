# VTSD OS — Agentic OS para Marketing Digital de Infoprodutos

## O que é este projeto

Sistema de skills para criação e venda de infoprodutos. Cada skill representa uma atividade do pipeline de marketing, invocada via slash command. Idioma de trabalho: **português brasileiro**.

---

## REGRA 0 — Estrutura multi-produto

Cada produto criado no VTSD OS vive em sua própria pasta raiz (`produto-01/`, `produto-02/`, etc.).
O produto ativo é sempre indicado por `memoria/produto-ativo.md`.

```
memoria/
  formatos.md          ← referência permanente do OS (nunca apagar)
  produto-ativo.md     ← aponta para a pasta do produto em uso
produto-01/
  memoria/             ← nicho.md, produto.md, funil.md, design.md deste produto
  01-nicho/
  02-pesquisa-mercado/
  03-produto/
  04-concepcao/
  05-funil/
  06-copy/
  06-landing/
  06-mandala/
  07-carrossel/
  07-editorial/
  07-apresentacao/
  08-trafego-meta/
  08-trafego-google/
  09-analise/
produto-02/            ← criado pelo próximo /instalar
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
> Execute `/instalar` para realizar a entrevista inicial e configurar o projeto antes de usar outras skills.

---

## REGRA 2 — Carregar memória antes de qualquer skill

Após verificar o gate, leia TODOS os arquivos existentes em `{pasta-ativa}/memoria/` antes de executar a skill solicitada.

- `{pasta-ativa}/memoria/nicho.md`, `produto.md`, `funil.md` — contexto do produto ativo
- `memoria/formatos.md` — referência permanente dos formatos disponíveis (e-book, curso simples, curso completo, desafio, comunidade, mentoria)
- `{pasta-ativa}/memoria/design.md` — sistema de design do produto. Se existir, **toda skill visual deve carregá-lo antes de gerar qualquer output visual**

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
| 0 | `/instalar` | Entrevista inicial, cria pasta produto-XX/, configura memoria/, pode invocar /funil |
| 0 | `/design` | Entrevista de marca, gera {pasta-ativa}/memoria/design.md (paleta, tipografia, componentes) |
| 1 | `/nicho` | Pesquisa, validação e posicionamento de nicho |
| 1.5 | `/pesquisa-mercado` | Pesquisa profunda de nicho em 9 eixos com busca real na web (opcional: `/produto` chama automaticamente; use direto para relatório completo + HTML com gráficos SVG) |
| 2 | `/produto` | Pesquisa nicho, gera 50 ideias em 15 formatos, usuário escolhe o produto |
| 2.5 | `/concepcao` | Concepção do produto escolhido: Promessa, 50 Benefícios, 5 Baldes, Identidade do Consumidor |
| 3 | `/funil` | Mapeia funil completo, gera opções de produtos |
| 4 | `/copy-pagina-vendas` | Copy completa de página de vendas em 15 blocos, padrão Light Copy (só texto, entrega Markdown no chat) |
| 4 | `/landing` | Página de vendas HTML completa |
| 4 | `/mandala` | Anúncios argumentativos pela Mandala de Anúncios (4 tipos: Ultra Segmentado, Problema-Solução, Pesquisa Científica, Atualidades Trend) |
| 5 | `/carrossel` | Carrossel de curiosidade atemporal para Instagram (7-9 slides, 3 modos visuais) |
| 5 | `/editorial` | Carrossel editorial 6 slides (dados, pesquisa, polêmica, contas malucas) |
| 5 | `/apresentacao` | Slides de apresentação |
| 6 | `/trafego-conexao` | Configura autenticação com Meta Ads (MCP OAuth ou App com token permanente no .env) |
| 6 | `/trafego-criar-campanha` | Sobe campanha Meta Ads (Sales ou Leads), preview YAML obrigatório, status PAUSED por padrão |
| 6 | `/trafego-google` | Campanhas Google Ads via MCP |
| 7 | `/analise` | Métricas, relatórios, otimização |
| — | `/analista-seo` | Auditoria completa SEO, GEO e AEO de qualquer URL (relatório .docx) |

---

## Mapa skill → pasta de output

Todos os caminhos são relativos à pasta do produto ativo (`{pasta-ativa}/`).

| Skill | Salva output em |
|---|---|
| `/instalar` | `{pasta-ativa}/memoria/` e atualiza `memoria/produto-ativo.md` |
| `/design` | `{pasta-ativa}/memoria/` |
| `/nicho` | `{pasta-ativa}/01-nicho/` |
| `/pesquisa-mercado` | `{pasta-ativa}/02-pesquisa-mercado/` |
| `/produto` | `{pasta-ativa}/02-pesquisa-mercado/` (tabela 50 ideias) |
| `/concepcao` | `{pasta-ativa}/04-concepcao/` |
| `/funil` | `{pasta-ativa}/05-funil/` |
| `/copy-pagina-vendas` | `{pasta-ativa}/06-copy/` |
| `/landing` | `{pasta-ativa}/06-landing/` |
| `/mandala` | `{pasta-ativa}/06-mandala/` |
| `/carrossel` | `{pasta-ativa}/07-carrossel/` |
| `/editorial` | `{pasta-ativa}/07-editorial/` |
| `/brand-carrossel` | `{pasta-ativa}/07-carrossel/` |
| `/apresentacao` | `{pasta-ativa}/07-apresentacao/` |
| `/trafego-conexao` | `{pasta-ativa}/08-trafego-meta/` |
| `/trafego-criar-campanha` | `{pasta-ativa}/08-trafego-meta/` |
| `/trafego-google` | `{pasta-ativa}/08-trafego-google/` |
| `/analise` | `{pasta-ativa}/09-analise/` |
| `/analista-seo` | `{pasta-ativa}/analista-seo/` |

---

## Convenção de nomes de output

Todos os arquivos gerados pelas skills devem ser nomeados:

```
YYYY-MM-DD-descricao-curta.ext
```

Exemplo: `2026-05-30-carrossel-lancamento-curso.html`
