---
name: egreen-google-ads
description: >
  Cria estrutura completa de campanha Google Ads para infoprodutos.
  Gera CSV pronto pra importar no Google Ads Editor com campanhas Search
  organizadas por cluster de palavras-chave, grupos de anúncios, RSAs,
  extensões e palavras-chave negativas. Lê contexto de memoria/egreen-nicho.md
  e memoria/egreen-produto.md. Salva em trafego-google/.
---

# /egreen-google-ads — Estrutura de campanha Google Ads

Skill que monta a campanha inteira em CSV pronto pra importar no Google Ads Editor. Sai do briefing direto pro CSV — sem montar grupo por grupo na mão na interface do Google.

## Dependências

- **Contexto do nicho:** `memoria/egreen-nicho.md` (nicho, público, posicionamento)
- **Contexto do produto:** `memoria/egreen-produto.md` (produto escolhido, preço, promessa)
- **Outputs vão em:** `trafego-google/YYYY-MM-DD-google-ads-<slug>/`

---

## Workflow

### Passo 1 — Briefing

Ler `memoria/egreen-nicho.md` e `memoria/egreen-produto.md` antes de perguntar qualquer coisa. Pular as perguntas já respondidas pela memória.

Se faltar informação, perguntar uma por vez:

1. **Produto/oferta a anunciar?** (nome, preço, link da página de vendas)
2. **Quem é o público?** (perfil, dor que resolve)
3. **Região:** nacional ou por estado/cidade?
4. **Orçamento diário?** (R$/dia)
5. **Objetivo:** compra direta / lead / WhatsApp / formulário?
6. **Landing page:** URL da página de vendas ou de captura?

### Passo 2 — Pesquisa de palavras-chave

Fazer busca real (WebSearch) para os termos do nicho e produto. Filtrar por **intenção comercial/transacional** (descartar informacionais).

Gerar:
- 30 a 50 termos-semente baseados no nicho e produto
- Agrupados em **clusters** (ex: "comprar-curso-X", "aprender-X-online", "melhor-curso-X")

### Passo 3 — Estrutura de campanha

**Padrão recomendado para infoprodutos:**

```
Campanha 1: <Produto> — Search Geral
├── Grupo: <Cluster 1>
│   ├── 10-15 keywords (mix de exata, frase, ampla modificada)
│   ├── 3 RSAs (15 headlines + 4 descriptions cada)
│   └── 10-15 keywords negativas no grupo
├── Grupo: <Cluster 2>
│   └── ...
└── ... (1 grupo por cluster do Passo 2)

Campanha 2: <Produto> — Concorrentes (opcional)
├── Keywords com nomes de produtos/cursos concorrentes
└── Copy com diferencial direto

Lista de negativas globais: termos genéricos descartados, grátis, pirata, torrent
```

### Passo 4 — Copies (RSAs)

Para cada grupo, gerar 3 RSAs (Responsive Search Ads):

**15 headlines** por anúncio (máx 30 caracteres cada):
- 5 com keyword principal
- 3 com diferenciais concretos (garantia, prazo de resultado, formato)
- 3 com CTA ("Garanta sua vaga", "Acesse agora", "Comece hoje")
- 2 com prova social (número de alunos, resultado específico)
- 2 com proposta de valor do produto

**4 descriptions** (máx 90 caracteres cada):
- 1 com promessa principal + CTA
- 1 com diferencial técnico + CTA
- 1 com garantia ou urgência (se aplicável)
- 1 com prova social + CTA

**Restrições do Google:**
- Headline: 30 caracteres (contar antes de entregar)
- Description: 90 caracteres (contar antes de entregar)
- Sem emojis, sem caps lock, sem repetição de palavras
- Sem afirmações superlativas não-comprovadas ("o melhor", "número 1") sem fonte

Aplicar princípios Light Copy: argumento concreto, dado específico, sem lero-lero.

### Passo 5 — Extensões

Gerar CSVs separados para cada extensão:

- **Sitelinks** (4-6): "Sobre o método", "Depoimentos", "Garantia", "Perguntas frequentes", "Acesse agora"
- **Snippets estruturados:** lista de módulos, formatos do produto, benefícios
- **Promoção** (se aplicável): desconto, condição especial, prazo

### Passo 6 — Configurações da campanha

Gerar arquivo `configuracoes.md` com:

- **Estratégia de lance:** "Maximizar conversões" para começar (migrar pra "Maximizar conversões com tCPA" após 30+ conversões)
- **Orçamento diário:** conforme briefing
- **Segmentação geográfica:** nacional ou estados selecionados
- **Idioma:** Português
- **Dispositivos:** ajustes de lance recomendados (mobile +0%, desktop +0%, tablet -20%)
- **Programação:** sem restrição de horário inicialmente — deixar o Google otimizar
- **Conversões a configurar:** compra confirmada, lead cadastrado, clique no CTA

### Passo 7 — Gerar os CSVs

Estrutura de pastas final:

```
trafego-google/YYYY-MM-DD-google-ads-<slug>/
  campanhas.csv             ← linha por campanha
  grupos.csv                ← linha por grupo de anúncio
  keywords.csv              ← keywords + match type
  keywords-negativas.csv    ← negativas por grupo + lista global
  anuncios.csv              ← RSAs (headlines + descriptions)
  extensoes-sitelinks.csv
  extensoes-snippets.csv
  extensoes-promocao.csv    (se aplicável)
  configuracoes.md          ← config + checklist de import
```

**Formato dos CSVs:** seguir padrão de importação do Google Ads Editor (colunas: Campaign, Ad group, Keyword, Match type, Status, Max CPC, Headline 1…15, Description 1…4, etc.).

### Passo 8 — Resumo + próximos passos

Mostrar ao usuário:

```
Campanha pronta: trafego-google/YYYY-MM-DD-google-ads-<slug>/

Estrutura:
- <N> campanhas
- <N> grupos de anúncio
- <N> palavras-chave (positivas)
- <N> palavras-chave negativas
- <N> RSAs

Para subir:
1. Abrir Google Ads Editor (desktop)
2. Conta → Importar → CSV
3. Subir campanhas.csv primeiro, depois grupos, keywords, anúncios, extensões
4. Revisar status (tudo "pausado" inicialmente — ativar manualmente)
5. Conferir conversões configuradas no Google Tag Manager
6. Ativar campanha quando estiver tudo OK
```

---

## Regras

- **Nunca inventar dados de CPC.** Se perguntado sobre custo, dar faixa baseada em WebSearch com a concorrência real do nicho.
- **Sempre começar pausado.** Usuário revisa antes de ativar.
- **Não anunciar pra termos informacionais.** "Como fazer X" raramente converte em infoproduto — orientar pra conteúdo orgânico.
- **Match type:** começar com Phrase Match na maioria. Exact pra termos de alta intenção. Broad só com dados de conversão consistentes.
- **Lista de negativas global é obrigatória.** Sem ela, queima orçamento em buscas irrelevantes (grátis, pirata, torrent, YouTube, download).
- **Conversões antes de ativar.** Sem pixel de conversão configurado, o Google não otimiza. Alertar o usuário e pedir setup antes de ativar.
- Copies aplicam Light Copy: dado concreto, sem promessa vaga, sem exclamação, sem travessão.
