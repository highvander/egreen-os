# EGreen OS — Agentic OS para Marketing Digital de Infoprodutos

Sistema de skills para criar e vender infoprodutos digitais do zero ao anúncio. Cada etapa do pipeline — nicho, produto, funil, copy, conteúdo, tráfego, análise — é uma skill independente, invocada como slash command dentro do Claude Code. Idioma de trabalho: português brasileiro.

---

## Pré-requisito

[Claude Code](https://claude.ai/code), CLI ou extensão (VS Code / JetBrains), com acesso a este projeto.

---

## Instalação

```bash
git clone https://github.com/highvander/egreen-os
cd egreen-os
```

Abra a pasta no Claude Code e rode:

```
/egreen-setup
```

A entrevista inicial cria a pasta do produto (`produto-01/`), configura a memória e libera o resto do pipeline. Sem isso rodado, nenhuma outra skill funciona — é o gate de instalação do sistema.

---

## Como usar: dois jeitos

### 1. Modo orquestrado (recomendado para começar do zero)

```
/egreen-lancamento
```

Roda o pipeline inteiro sozinho — nicho, produto, posicionamento, currículo, funil, identidade, copy, landing, e-mails, anúncios, pós-venda, métricas — invocando cada skill na hora certa. Decide os pontos de escolha usando 5 frameworks de validação de mercado reconhecidos (Mom Test, Jobs to Be Done, Lean Startup, pretotipagem de Savoia, PMF Pyramid + teste Sean Ellis) em vez de perguntar micro-detalhe a cada passo. Para em 4 gates para você aprovar antes de seguir: nicho validado, produto/posicionamento aprovado, oferta/funil aprovado, sinal de mercado testado. Se a sessão cair no meio, retomar `/egreen-lancamento` continua de onde parou.

Use este modo quando: está começando um produto do zero, ou quer que o sistema guie a sequência inteira sem você ter que lembrar qual skill vem depois de qual.

### 2. Modo manual (skill por skill)

Chame a skill certa diretamente quando só precisa de uma etapa isolada — revisar uma página que não converte, escrever só um e-mail, montar só o programa de afiliados. As tabelas abaixo dizem qual skill usar e em que momento.

Toda skill lê sozinha a memória do produto ativo (nicho, produto, funil, design, voz de marca) antes de perguntar qualquer coisa — não repita contexto que já foi definido em uma skill anterior.

---

## Estrutura multi-produto

Cada produto vive na própria pasta raiz, isolada das demais. Rodar `/egreen-setup` de novo **nunca sobrescreve** o produto anterior — cria `produto-02/`, `produto-03/`, etc. O produto em edição no momento é sempre o indicado por `memoria/produto-ativo.md`.

```
egreen-os/
  memoria/
    formatos.md            ← referência permanente do OS (e-book, curso, desafio, comunidade, mentoria)
    produto-ativo.md       ← aponta para a pasta do produto em uso
  produto-01/
    memoria/
      egreen-nicho.md, egreen-produto.md, egreen-funil.md, egreen-design.md, brand-voice.md
    egreen-pesquisa/
    egreen-concepcao/
    egreen-curriculo/       ou egreen-experiencia/
    egreen-posicionamento/
    egreen-identidade/
    egreen-funil/
    egreen-growth/
    egreen-metricas/
    egreen-copy/            egreen-copywriting/
    egreen-conteudo/
    egreen-landing/
    egreen-vsl/
    egreen-emails/
    egreen-mandala/
    egreen-stories/
    egreen-carrossel/       egreen-editorial/       egreen-slides/
    egreen-posvenda/
    egreen-afiliados/
    egreen-meta-ads/        egreen-google-ads/
    egreen-cro/
    egreen-analise/
    egreen-seo/             egreen-seo-estrategia/
  produto-02/               ← criado pelo próximo /egreen-setup
    ...
  .claude/skills/           ← skills do sistema
```

Pastas `produto-*/` ficam fora do controle de versão — os dados de cada produto vivem só na sua máquina.

---

## Qual skill eu uso agora? (perguntas comuns)

| Sua situação | Skill |
|---|---|
| Quero criar um produto do zero e não sei por onde começar | `/egreen-lancamento` |
| Preciso validar se um nicho tem demanda real | `/egreen-pesquisa` |
| Tenho o nicho, preciso de ideias de produto | `/egreen-produto` |
| Escolhi o produto, preciso da promessa e dos benefícios | `/egreen-concepcao` |
| Preciso decidir como me diferencio da concorrência | `/egreen-posicionamento` |
| Preciso desenhar os módulos/aulas do curso | `/egreen-curriculo` |
| Vou lançar um Desafio, Comunidade ou Mentoria e preciso do roteiro de entrega | `/egreen-experiencia` |
| Preciso decidir preço, order bump, upsell | `/egreen-funil` |
| Preciso saber de onde vai vir o tráfego e como reter cliente | `/egreen-growth` |
| Preciso escrever a página de vendas inteira | `/egreen-copy` (texto) + `/egreen-landing` (HTML) |
| Preciso só de um anúncio, e-mail ou headline avulsos | `/egreen-copywriting` |
| Preciso do roteiro de um webinar ou VSL | `/egreen-vsl` |
| Minha página existe mas não converte | `/egreen-cro` |
| Minha campanha está rodando mas não sei se o número é bom | `/egreen-metricas` (plano) ou `/egreen-analise` (performance real) |
| Preciso da copy de checkout, onboarding ou pedido de depoimento | `/egreen-posvenda` |
| Quero montar um programa de afiliados | `/egreen-afiliados` |
| Preciso de conteúdo orgânico pro Instagram | `/egreen-carrossel`, `/egreen-editorial` ou `/egreen-slides` |
| Não sei sobre o que postar, ou quero autoridade/plano editorial | `/egreen-conteudo` |
| Quero vender direto pelo Direct do Instagram (Stories) | `/egreen-stories` |
| Preciso subir campanha no Meta ou Google Ads | `/egreen-meta-ads` / `/egreen-google-ads` |
| Quero saber se meu site está bem posicionado no Google | `/egreen-seo` |
| Quero planejar uma estratégia de SEO/conteúdo orgânico | `/egreen-seo-estrategia` |
| Quero apagar tudo e recomeçar o produto ativo | `/egreen-reset` |

---

## Pipeline completo, por fase

### Fase 0 — Fundação

| Comando | Quando usar | O que entrega |
|---|---|---|
| `/egreen-setup` | Sempre o primeiro comando de um produto novo | Entrevista inicial, cria `produto-XX/`, configura memória |
| `/egreen-design` | Depois do setup, antes de qualquer peça visual | Paleta, tipografia, componentes — `memoria/design.md` |
| `/egreen-brand` | Depois do design, antes de qualquer copy | Tom, arquétipo, vocabulário, amostras — `memoria/brand-voice.md` |

### Fase 1 — Pesquisa e validação

| Comando | Quando usar | O que entrega |
|---|---|---|
| `/egreen-pesquisa` | Antes de escolher produto, ou quando pedirem pesquisa de mercado de um nicho | Relatório em 9 eixos com busca real na web |
| `/egreen-produto` | Depois da pesquisa, na hora de decidir o que vender | 50 ideias em 15 formatos |
| `/egreen-concepcao` | Depois de escolher o produto | Promessa, 50 benefícios, 5 baldes, identidade do consumidor |

### Fase 2 — Estratégia e conteúdo de entrega

| Comando | Quando usar | O que entrega |
|---|---|---|
| `/egreen-posicionamento` | Antes de definir identidade visual ou escrever copy | Escada competitiva, canvas, positioning statement |
| `/egreen-identidade` | Depois do posicionamento, antes do `/egreen-design` | Onliness statement (diferenciação radical) |
| `/egreen-curriculo` | Produto é Curso Simples ou Curso Completo | Módulos, aulas, objetivo e prática de cada uma |
| `/egreen-experiencia` | Produto é Desafio, Comunidade ou Mentoria | Missões diárias, estrutura de canais/rituais, ou roteiro de sessão |
| `/egreen-ebook` | Produto é e-book de implementação rápida | E-book curto pronto pra vender |
| `/egreen-material` | Precisa transformar conteúdo bruto em material didático visual | Slides/material de aula formatado |
| `/egreen-funil` | Depois do conteúdo de entrega definido | Arquitetura de oferta: tripwire, order bump, upsell, preço |
| `/egreen-growth` | Precisa decidir de onde vem o tráfego e como reter cliente | Motor de aquisição + Customer Value Journey em 8 etapas |
| `/egreen-metricas` | Antes de gerar qualquer tráfego real | Plano de medição, KPIs, segmentação por intenção |

### Fase 3 — Produção de venda

| Comando | Quando usar | O que entrega |
|---|---|---|
| `/egreen-copy` | Precisa da copy completa da página de vendas | 15 blocos em Markdown (Light Copy) |
| `/egreen-copywriting` | Precisa de uma peça avulsa (anúncio, e-mail, headline, CTA) | Copy pontual com diagnóstico Schwartz/Halbert/Wiebe |
| `/egreen-landing` | Copy pronta, precisa virar página | HTML completo da página de vendas |
| `/egreen-vsl` | Precisa de roteiro de vídeo de venda longo | Script de Webinar/live ou VSL gravada |
| `/egreen-emails` | Precisa de sequência de e-mail pré-venda | Boas-vindas, nutrição, lançamento |
| `/egreen-mandala` | Precisa de anúncio argumentativo ou roteiro de vídeo curto | 4 tipos de anúncio + versão Reels/TikTok/Stories |
| `/egreen-stories` | Precisa de sequência de Stories pra vender pelo Direct | Roteiro story a story (Stories 10X) + fechamento no Inbox Lucrativo |

### Fase 4 — Conteúdo orgânico

| Comando | Quando usar | O que entrega |
|---|---|---|
| `/egreen-carrossel` | Conteúdo de curiosidade atemporal pro Instagram | Carrossel 7-9 slides |
| `/egreen-editorial` | Conteúdo com dado, pesquisa ou polêmica | Carrossel editorial 6 slides |
| `/egreen-brand-carrossel` | Carrossel usando o sistema de marca (Principal) | Carrossel com identidade fixa |
| `/egreen-slides` | Apresentação/pitch/aula | Slides HTML |
| `/egreen-conteudo` | Sem posicionamento editorial, falta ideia, quer autoridade ou plano de 30 dias | Estratégia/argumento de conteúdo (BrandsDecoded) — não gera peça visual final |

### Fase 5 — Tráfego pago

| Comando | Quando usar | O que entrega |
|---|---|---|
| `/egreen-meta-auth` | Antes do primeiro `/egreen-meta-ads` | Autenticação configurada |
| `/egreen-meta-ads` | Subir campanha no Meta | Campanha Sales/Leads, preview obrigatório, PAUSED por padrão |
| `/egreen-google-ads` | Subir campanha no Google | Campanha via MCP |

### Fase 6 — Pós-venda e crescimento

| Comando | Quando usar | O que entrega |
|---|---|---|
| `/egreen-posvenda` | Cliente comprou, precisa de checkout/onboarding/upsell/depoimento | Copy de order bump, onboarding, upsell, pedido de depoimento |
| `/egreen-afiliados` | Quer recrutar afiliados/parceiros | Estrutura do programa + carta de convite |

### Fase 7 — Diagnóstico e otimização

| Comando | Quando usar | O que entrega |
|---|---|---|
| `/egreen-cro` | Página existe mas não converte como esperado | Diagnóstico de conversão + hipóteses priorizadas |
| `/egreen-analise` | Campanha rodando, precisa saber se está indo bem | ROAS, CPL, CPA, scorecard, diagnóstico de vazamento |
| `/egreen-seo` | Site publicado, quer auditoria de SEO/GEO/AEO | Relatório completo (.docx) |
| `/egreen-seo-estrategia` | Quer planejar estratégia de SEO/conteúdo antes de auditar | Pauta de conteúdo priorizada |

### Utilitário

| Comando | Quando usar | O que entrega |
|---|---|---|
| `/egreen-reset` | Quer apagar a memória do produto ativo | Backup opcional + limpeza |

---

## Créditos

- Skill `/egreen-slides` baseada em [frontend-slides](https://github.com/zarazhangrui/frontend-slides) por Zara Zhang — licença MIT
- `/egreen-mandala` baseada na Mandala de Anúncios de Leandro Ladeira (VTSD/Fluxo)
- `/egreen-stories` baseada no método Stories 10X de Leandro Ladeira (VTSD/Fluxo)
