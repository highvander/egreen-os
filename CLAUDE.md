# EGreen OS — Agentic OS para Marketing Digital de Infoprodutos

## O que é este projeto

Sistema de skills para criação e venda de infoprodutos. Cada skill representa uma atividade do pipeline de marketing, invocada via slash command. Idioma de trabalho: **português brasileiro**.

---

## REGRA 0 — Estrutura multi-produto

Cada produto criado no EGreen OS vive em sua própria pasta raiz (`produto-01/`, `produto-02/`, etc.).
O produto ativo é sempre indicado por `memoria/produto-ativo.md`.

```
memoria/
  formatos.md          ← referência permanente do OS (nunca apagar)
  produto-ativo.md     ← aponta para a pasta do produto em uso
produto-01/
  memoria/             ← egreen-nicho.md, egreen-produto.md, egreen-funil.md, egreen-design.md deste produto
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
{pasta-ativa}/memoria/egreen-nicho.md
{pasta-ativa}/memoria/egreen-produto.md
{pasta-ativa}/memoria/egreen-funil.md
```

Se `memoria/produto-ativo.md` não existir, ou se qualquer arquivo de memória
tiver `status: vazio` no frontmatter ou estiver ausente:

> **PARE.** O OS não está configurado.
> Execute `/egreen-setup` para realizar a entrevista inicial e configurar o projeto antes de usar outras skills.

---

## REGRA 2 — Carregar memória antes de qualquer skill

Após verificar o gate, leia TODOS os arquivos existentes em `{pasta-ativa}/memoria/` antes de executar a skill solicitada.

- `{pasta-ativa}/memoria/egreen-nicho.md`, `egreen-produto.md`, `egreen-funil.md` — contexto do produto ativo
- `memoria/formatos.md` — referência permanente dos formatos disponíveis (e-book, curso simples, curso completo, desafio, comunidade, mentoria)
- `{pasta-ativa}/memoria/egreen-design.md` — sistema de design do produto. Se existir, **toda skill visual deve carregá-lo antes de gerar qualquer output visual**
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

**Para criar o produto inteiro do zero — nicho, oferta, funil, identidade, copy, landing, anúncios — use `/egreen-lancamento`.** É o orquestrador mestre: invoca todas as skills abaixo na ordem certa, decide os pontos de escolha com 5 frameworks de validação de mercado (Mom Test, Jobs to Be Done, Lean Startup, pretotipagem de Savoia, PMF Pyramid de Dan Olsen + teste Sean Ellis) e para em 4 gates críticos para aprovação. Use as skills individuais da tabela abaixo diretamente só quando quiser rodar uma etapa isolada.

Execute nesta ordem para um novo infoproduto (ou deixe o `/egreen-lancamento` orquestrar):

| # | Slash Command | O que faz |
|---|---|---|
| ★ | `/egreen-lancamento` | Orquestrador mestre: roda o pipeline completo do zero, decide pontos de escolha com 5 frameworks de validação de mercado, para em 4 gates para aprovação |
| 0 | `/egreen-setup` | Entrevista inicial, cria pasta produto-XX/, configura memoria/, pode invocar /egreen-funil |
| 0 | `/egreen-design` | Entrevista de marca, gera {pasta-ativa}/memoria/design.md (paleta, tipografia, componentes) |
| 0 | `/egreen-brand` | Entrevista de voz, gera {pasta-ativa}/memoria/brand-voice.md (tom, arquétipo, vocabulário, do/don't, amostras de copy). Execute antes de /egreen-copy |
| 1 | `/egreen-pesquisa` | Pesquisa profunda de nicho em 9 eixos com busca real na web (opcional: `/egreen-produto` chama automaticamente; use direto para relatório completo + HTML com gráficos SVG). `nicho.md` em si é preenchido pela entrevista de `/egreen-setup` |
| 2 | `/egreen-produto` | Pesquisa nicho, gera 50 ideias em 15 formatos, usuário escolhe o produto |
| 2.5 | `/egreen-concepcao` | Concepção do produto escolhido: Promessa, 50 Benefícios, 5 Baldes, Identidade do Consumidor |
| 2.7 | `/egreen-curriculo` | Currículo/módulos do Curso Simples ou Curso Completo (Backward Design + Bloom + Gagné) — o conteúdo de entrega em si |
| 2.7 | `/egreen-experiencia` | Missões diárias do Desafio, estrutura da Comunidade, ou roteiro de sessão da Mentoria (Atomic Habits + CMX/FeverBee + GROW) |
| 2.7 | `/egreen-ebook` | Ebook curto e prático de implementação imediata para produtos low ticket |
| 3 | `/egreen-funil` | Mapeia funil completo, gera opções de produtos |
| 4 | `/egreen-copy` | Copy completa de página de vendas em 15 blocos, padrão Light Copy (só texto, entrega Markdown no chat) |
| 4 | `/egreen-landing` | Página de vendas HTML completa |
| 4 | `/egreen-emails` | Sequências de email completas: Boas-vindas (5 emails), Nutrição (6 emails), Lançamento (9 emails) |
| 4 | `/egreen-mandala` | Anúncios argumentativos pela Mandala de Anúncios (4 tipos) + roteiro de vídeo curto (Reels/TikTok/Stories) |
| 4 | `/egreen-vsl` | Roteiro de vídeo de venda longo — Webinar/live (Perfect Webinar Script) ou VSL gravada (PASTOR) |
| 4.5 | `/egreen-posvenda` | Copy do momento da compra em diante: order bump/OTO, onboarding pós-compra, upsell, pedido de depoimento |
| 5 | `/egreen-carrossel` | Carrossel de curiosidade atemporal para Instagram (7-9 slides, 3 modos visuais) |
| 5 | `/egreen-editorial` | Carrossel editorial 6 slides (dados, pesquisa, polêmica, contas malucas) |
| 5 | `/egreen-brand-carrossel` | Carrossel editorial com identidade de marca do projeto (design system Principal) |
| 5 | `/egreen-slides` | Slides de apresentação |
| 5 | `/egreen-material` | Transforma conteúdo educacional em material didático visual (aula, treinamento, infográfico, dashboard de progresso) |
| 5 | `/egreen-stories` | Sequência de Stories do Instagram pelo método Stories 10X (Ladeira): tipo de sequência, esqueleto com os 38 Dispositivos de Engenharia Social, fechamento no Inbox Lucrativo |
| 6 | `/egreen-meta-auth` | Configura autenticação com Meta Ads (MCP OAuth ou App com token permanente no .env) |
| 6 | `/egreen-meta-ads` | Sobe campanha Meta Ads (Sales ou Leads), preview YAML obrigatório, status PAUSED por padrão |
| 6 | `/egreen-google-ads` | Campanhas Google Ads via MCP |
| 7 | `/egreen-analise` | Performance do funil: ROAS, CPL, CPA, email, scorecard 0-100, diagnóstico de vazamentos, plano de ação, relatório HTML |
| — | `/egreen-seo` | Auditoria completa SEO, GEO e AEO de qualquer URL (relatório .docx) |
| — | `/egreen-posicionamento` | Posicionamento de marca/produto (Dunford + Ries & Trout): escada competitiva, canvas e positioning statement |
| — | `/egreen-identidade` | Diferenciação de marca e identidade (Neumeier Brand Gap/Zag + Pentagram): onliness statement, insumo para `/egreen-design` |
| — | `/egreen-copywriting` | Copy persuasiva avulsa — anúncio, e-mail, headline, CTA, VSL (Schwartz + Halbert + Wiebe). Complementa `/egreen-copy` |
| — | `/egreen-conteudo` | Estratégia de conteúdo e autoridade pessoal/de marca: mineração de repertório, matéria-prima em volume, engenharia reversa de creators, ganchos de descoberta, argumento de carrossel, autoridade empresarial, auditoria estilo Ogilvy, plano de 30 dias (BrandsDecoded). Só sob demanda, fora do fluxo automático de `/egreen-lancamento` |
| — | `/egreen-growth` | Estratégia de aquisição e Customer Value Journey em 8 etapas (Patel + Deiss). Complementa `/egreen-funil` |
| — | `/egreen-cro` | Diagnóstico de conversão e priorização de testes A/B (Peep Laja / CXL) |
| — | `/egreen-metricas` | Plano de medição, KPIs e segmentação See-Think-Do-Care (Avinash Kaushik) |
| — | `/egreen-seo-estrategia` | Estratégia de SEO e pauta de conteúdo para tráfego orgânico (Fishkin + Dean) |
| — | `/egreen-afiliados` | Estrutura programa de afiliados (comissão, kit, regras) e copy de recrutamento (Cialdini + prática Hotmart/Eduzz/Kiwify) |
| — | `/egreen-reset` | Apaga a memória do produto atual e restaura o estado inicial do OS, com backup opcional. Não apaga outputs gerados |

---

## Mapa skill → pasta de output

Todos os caminhos são relativos à pasta do produto ativo (`{pasta-ativa}/`).

| Skill | Salva output em |
|---|---|
| `/egreen-lancamento` | `{pasta-ativa}/memoria/status-lancamento.md` (progresso do pipeline; cada fase salva no local da skill correspondente) |
| `/egreen-setup` | `{pasta-ativa}/memoria/` e atualiza `memoria/produto-ativo.md` |
| `/egreen-design` | `{pasta-ativa}/memoria/` |
| `/egreen-brand` | `{pasta-ativa}/memoria/` |
| `/egreen-pesquisa` | `{pasta-ativa}/egreen-pesquisa/` |
| `/egreen-produto` | `{pasta-ativa}/egreen-pesquisa/` (tabela 50 ideias) |
| `/egreen-concepcao` | `{pasta-ativa}/egreen-concepcao/` |
| `/egreen-curriculo` | `{pasta-ativa}/egreen-curriculo/` |
| `/egreen-experiencia` | `{pasta-ativa}/egreen-experiencia/` |
| `/egreen-ebook` | `{pasta-ativa}/egreen-ebook/` |
| `/egreen-funil` | `{pasta-ativa}/egreen-funil/` |
| `/egreen-copy` | `{pasta-ativa}/egreen-copy/` |
| `/egreen-landing` | `{pasta-ativa}/egreen-landing/` |
| `/egreen-emails` | `{pasta-ativa}/egreen-emails/` |
| `/egreen-mandala` | `{pasta-ativa}/egreen-mandala/` |
| `/egreen-vsl` | `{pasta-ativa}/egreen-vsl/` |
| `/egreen-posvenda` | `{pasta-ativa}/egreen-posvenda/` |
| `/egreen-carrossel` | `{pasta-ativa}/egreen-carrossel/` |
| `/egreen-editorial` | `{pasta-ativa}/egreen-editorial/` |
| `/egreen-brand-carrossel` | `{pasta-ativa}/egreen-carrossel/` |
| `/egreen-slides` | `{pasta-ativa}/egreen-slides/` |
| `/egreen-material` | `{pasta-ativa}/egreen-material/` |
| `/egreen-stories` | `{pasta-ativa}/egreen-stories/` |
| `/egreen-reset` | não gera output (apaga/restaura `memoria/`) |
| `/egreen-meta-auth` | `{pasta-ativa}/egreen-meta-ads/` |
| `/egreen-meta-ads` | `{pasta-ativa}/egreen-meta-ads/` |
| `/egreen-google-ads` | `{pasta-ativa}/egreen-google-ads/` |
| `/egreen-analise` | `{pasta-ativa}/egreen-analise/` |
| `/egreen-seo` | `{pasta-ativa}/egreen-seo/` |
| `/egreen-posicionamento` | `{pasta-ativa}/egreen-posicionamento/` |
| `/egreen-identidade` | `{pasta-ativa}/egreen-identidade/` |
| `/egreen-afiliados` | `{pasta-ativa}/egreen-afiliados/` |
| `/egreen-copywriting` | `{pasta-ativa}/egreen-copywriting/` |
| `/egreen-conteudo` | `{pasta-ativa}/egreen-conteudo/` |
| `/egreen-growth` | `{pasta-ativa}/egreen-growth/` |
| `/egreen-cro` | `{pasta-ativa}/egreen-cro/` |
| `/egreen-metricas` | `{pasta-ativa}/egreen-metricas/` |
| `/egreen-seo-estrategia` | `{pasta-ativa}/egreen-seo-estrategia/` |

---

## Convenção de nomes de output

Todos os arquivos gerados pelas skills devem ser nomeados:

```
YYYY-MM-DD-descricao-curta.ext
```

Exemplo: `2026-05-30-carrossel-lancamento-curso.html`
