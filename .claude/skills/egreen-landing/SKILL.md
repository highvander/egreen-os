---
name: egreen-landing
description: >
  Gera a página de vendas HTML completa do infoproduto em 6 seções (S1→S6).
  Carrega memória do produto, lê output do /egreen-copy como insumo, aplica
  design tokens de egreen-design.md e brand-voice.md. Aprovação seção a seção.
  Salva HTML único auto-contido em {pasta-ativa}/egreen-landing/.
  Requer egreen-design.md para identidade visual. Avisa se brand-voice.md
  ou egreen-copy estiverem ausentes antes de qualquer geração.
---

# /egreen-landing — Página de Vendas HTML

Skill que gera a página de vendas HTML completa do produto ativo em 6 seções (S1→S6), com aprovação entre cada uma. Output: arquivo HTML único, auto-contido, mobile-first, sem JavaScript, pronto para deploy.

---

## Passo 0 — Gate + Carregamento de Memória

### 0.1 Gate obrigatório (REGRA 1)

Leia `memoria/produto-ativo.md` para obter `{pasta-ativa}`.

Verifique:
```
{pasta-ativa}/memoria/egreen-nicho.md
{pasta-ativa}/memoria/egreen-produto.md
{pasta-ativa}/memoria/egreen-funil.md
```

Se `memoria/produto-ativo.md` não existir, ou qualquer arquivo acima tiver `status: vazio` ou estiver ausente:

> **PARE.** O OS não está configurado. Execute `/egreen-setup` antes de continuar.

### 0.2 Carregar memória do produto (REGRA 2)

Leia todos os arquivos existentes em `{pasta-ativa}/memoria/`:
- `egreen-nicho.md` — público-alvo, dores, objeções comuns
- `egreen-produto.md` — promessa, diferencial, mecanismo único
- `egreen-funil.md` — oferta, bônus, preços, garantia

### 0.3 Avisos bloqueantes

Verifique cada arquivo abaixo **em ordem**, um por vez. Para cada ausente, exiba o aviso, aguarde resposta e registre a escolha antes de verificar o próximo.

**Se `{pasta-ativa}/memoria/egreen-design.md` não existir:**
```
⚠️ egreen-design.md não encontrado.
Sem ele, o HTML será gerado com estilo genérico (cores, tipografia e espaçamento padrão — sem a identidade visual da sua marca).

1. Continuar com estilo genérico
2. Parar e rodar /egreen-design primeiro
```

**Se `{pasta-ativa}/memoria/brand-voice.md` não existir:**
```
⚠️ brand-voice.md não encontrado.
O copy pode ficar inconsistente com a voz da marca (vocabulário, tom, regras de escrita).

1. Continuar sem guia de voz
2. Parar e rodar /egreen-brand primeiro
```

**Se não houver arquivo em `{pasta-ativa}/egreen-copy/` (buscar o mais recente por data no nome):**
```
⚠️ Nenhum output de /egreen-copy encontrado.
A landing gerará copy próprio a partir da memória do produto. Para maior consistência, rode /egreen-copy antes.

1. Gerar copy próprio a partir da memória
2. Parar e rodar /egreen-copy primeiro
```

Se o usuário escolher "2" em qualquer aviso: encerrar a skill imediatamente.
Se escolher "1": registrar e avançar para o próximo aviso.

---

## Passo 1 — Confirmar Insumos

Após resolver os avisos, exibir resumo:

```
Vou gerar a landing page de [nome do produto de egreen-produto.md].

Insumos:
- egreen-design.md: [✅ carregado com tokens / ⚠️ estilo genérico]
- brand-voice.md: [✅ carregado / ⚠️ ausente]
- egreen-copy: [✅ YYYY-MM-DD-nome.md / ⚠️ gerando copy próprio]

Estrutura: 6 seções (S1→S6), aprovação entre cada uma.
Arquivo final: HTML único auto-contido, mobile-first, sem JavaScript.

1. Pode gerar
2. Quero ajustar algo antes
```

Se "2": perguntar o que ajustar e aguardar resposta antes de continuar.

---

## Passo 2 — Geração Seção a Seção

Para cada seção:
1. Gerar HTML da seção
2. Mostrar preview do texto (legível, sem tags HTML visíveis)
3. Mostrar bloco HTML em code block
4. Aguardar: `1. Aprovar e seguir para [próxima seção] / 2. Quero ajustar esta seção`
5. Se "2": perguntar o que mudar → regenerar só aquela seção → pedir aprovação novamente

**Regras globais de copy para todas as seções:**
- Sem travessão
- Sem ponto de exclamação
- Sem "mesmo que" / "sem precisar"
- Toda promessa tem número, prazo ou situação concreta
- CTA sempre em 1ª pessoa ("Quero", "Preciso", "Vou")
- Se `brand-voice.md` carregado: usar vocabulário autorizado, evitar proibidos, seguir dimensões de tom

---

### S1 — Above the Fold

**Objetivo:** Parar o scroll. Criar curiosidade sem revelar o produto completo.

**Insumo preferencial:** Bloco de headline do egreen-copy (se disponível).
**Fallback:** Gerar headline a partir da promessa de `egreen-produto.md`.

**Elementos obrigatórios:**
- `<h1>`: headline curiosa ou não-óbvia — premissa, aviso ou ensinamento, não o resultado. Máx 12 palavras.
- `<p class="subheadline">`: para quem é + o que recebe, sem exclamação
- `<a class="cta-primary">`: texto em 1ª pessoa e orientado a valor (ex: "Quero garantir meu acesso")
- `<p class="cta-support">`: microcopy abaixo do botão (ex: "Acesso imediato. Sem compromisso.")
- `<!-- PLACEHOLDER: hero-image.jpg -->` comentado para imagem de fundo ou ilustração
- Sem `<nav>` ou links de menu

**HTML esperado:**
```html
<h1>[headline curiosa — máx 12 palavras]</h1>
<p class="subheadline">[para quem é + o que recebe]</p>
<!-- PLACEHOLDER: hero-image.jpg -->
<a href="#s6-cta" class="cta-primary">[texto CTA em 1ª pessoa]</a>
<p class="cta-support">[microcopy — ex: Acesso imediato. Sem compromisso.]</p>
```

---

### S2 — Prova Social

**Objetivo:** Construir credibilidade antes de apresentar o produto.

**Insumo preferencial:** Blocos de prova social do egreen-copy.
**Fallback:** Criar com dados de `egreen-nicho.md` e `egreen-produto.md`.

**Elementos obrigatórios:**
- 2-3 cards de depoimento, cada um com:
  - Citação: resultado específico + prazo (sem elogios genéricos)
  - Assinatura: Nome + situação antes
  - Se não houver depoimentos reais: `<!-- PLACEHOLDER: Depoimento — [resultado] + [prazo] + [nome] -->`
- Números agregados se existirem (ex: "127 alunos", "4.9/5") — exatos, não arredondados
- Logos de clientes ou mídias se mencionados em `egreen-produto.md` ou `egreen-funil.md`

**HTML esperado:**
```html
<div class="testimonial-grid">
  <div class="testimonial-card">
    <blockquote>"[resultado específico em prazo específico]"</blockquote>
    <cite>— [Nome], [situação antes]</cite>
  </div>
  <!-- repetir para 2-3 depoimentos -->
</div>
<!-- [números agregados se existirem] -->
```

---

### S3 — Problema / Identificação

**Objetivo:** Fazer o leitor pensar "isso sou eu". Construir identificação antes de qualquer menção à solução.

**Insumo preferencial:** Bloco de agitação de problema do egreen-copy.
**Fallback:** Dores de `egreen-nicho.md`.

**Elementos obrigatórios:**
- `<h2>`: nomeia a dor específica (não a genérica)
- 3-5 `<p>` em 1ª pessoa como se o avatar estivesse falando
- Zero menção ao produto, à solução ou ao preço nesta seção
- Se `brand-voice.md` carregado: usar expressões e linguagem autorizadas

**HTML esperado:**
```html
<h2>[dor específica — em 1ª pessoa ou nomeando o avatar]</h2>
<p>[parágrafo em 1ª pessoa descrevendo a situação do avatar]</p>
<p>[parágrafo intensificando a dor — consequência específica]</p>
<p>[parágrafo com tentativa frustrada anterior — sem culpar o avatar]</p>
```

---

### S4 — Mecanismo Único

**Objetivo:** Mostrar por que os outros métodos falham e como este produto resolve a causa raiz.

**Insumo preferencial:** Bloco de mecanismo/solução do egreen-copy.
**Fallback:** Diferencial de `egreen-produto.md`.

**Elementos obrigatórios:**
- `<h2>`: nomeia por que os outros falham (sem atacar concorrentes pelo nome)
- Parágrafo nomeando o inimigo concreto (método antigo, crença errada, obstáculo sistêmico)
- `<p class="mechanism-name">`: nome próprio do mecanismo único
- Explicação em linguagem simples de como funciona diferente
- Sem mencionar preço nesta seção

**HTML esperado:**
```html
<h2>[por que os outros métodos falham — enquadramento do problema raiz]</h2>
<p>[nomeia o inimigo concreto]</p>
<p class="mechanism-name">[Nome do Mecanismo Único]</p>
<p>[como funciona diferente em linguagem simples]</p>
```

---

### S5 — Value Stack / Oferta

**Objetivo:** Mostrar que o valor recebido é muito maior que o preço.

**Insumo preferencial:** Blocos de oferta e bônus do egreen-copy + dados de `egreen-funil.md`.
**Fallback:** Construir inteiramente a partir de `egreen-funil.md`.

**Elementos obrigatórios:**
- `<h2>` da oferta
- Lista de value stack com produto principal + todos os bônus de `egreen-funil.md`:
  - Cada item: nome + o que resolve em 1 linha + valor declarado
- Linha de total riscado vs preço real
- Se houver order bump em `egreen-funil.md`: mencionar como oferta adicional após a tabela

**HTML esperado:**
```html
<h2>[headline da oferta]</h2>
<div class="value-stack">
  <div class="value-stack-item">
    <span>[Produto Principal: nome]</span>
    <span>R$ [valor]</span>
  </div>
  <div class="value-stack-item">
    <span>[Bônus 1: nome] — [o que resolve em 1 linha]</span>
    <span>R$ [valor]</span>
  </div>
  <!-- repetir para cada bônus -->
  <div class="value-stack-item value-stack-total">
    <span>Total</span>
    <span class="price-original">R$ [soma total]</span>
  </div>
  <div class="value-stack-item">
    <span>Hoje por apenas</span>
    <span class="price-real">R$ [preço real]</span>
  </div>
</div>
```

---

### S6 — CTA + Garantia + FAQ

**Objetivo:** Remover última barreira e converter.

**Insumo preferencial:** Bloco de fechamento do egreen-copy + dados de `egreen-funil.md`.
**Fallback:** Objeções de `egreen-nicho.md` + garantia de `egreen-funil.md`.

**Elementos obrigatórios:**
- `<h2>`: urgência real (sem criar escassez falsa)
- CTA principal (mesmo texto e href de S1)
- Bloco de garantia: prazo + o que cobre
- FAQ com 3-5 itens em `<details>/<summary>` com objeções reais de `egreen-nicho.md`
- CTA final repetido abaixo do FAQ
- Sem links externos que desviem da conversão

**HTML esperado:**
```html
<h2>[headline de oferta com urgência real]</h2>
<a href="#s6-cta" class="cta-primary">[mesmo texto CTA de S1]</a>
<div class="garantia">
  <p>[prazo] dias de garantia incondicional. [O que cobre.]</p>
</div>
<div class="faq">
  <details>
    <summary>[objeção real do avatar — ex: "E se eu não tiver tempo?"]</summary>
    <p>[resposta direta e curta]</p>
  </details>
  <!-- repetir para 3-5 objeções -->
</div>
<a href="#s6-cta" class="cta-primary">[mesmo texto CTA]</a>
```

---

## Passo 3 — Consolidar e Salvar (REGRA 3)

Após aprovação de S6, montar o HTML completo com a estrutura abaixo. Substituir cada marcador `[SX conteúdo aprovado]` pelo conteúdo interno da seção aprovada (apenas o conteúdo dentro da `<div class="container">`, sem a tag `<section>` externa).

Determinar `{slug-produto}`: pegar o nome do produto de `egreen-produto.md`, converter para minúsculas, substituir espaços e acentos por hífens (ex: "Método Foco" → "metodo-foco").

Salvar em: `{pasta-ativa}/egreen-landing/YYYY-MM-DD-landing-{slug-produto}.html`

**Estrutura HTML completa a ser gerada:**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Nome do Produto de egreen-produto.md]</title>
  <!-- Google Fonts (se egreen-design.md tiver fonte definida):
       Ex: <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
       Omitir se egreen-design.md ausente ou sem fonte especificada -->
  <style>
    /* === DESIGN TOKENS === */
    :root {
      /* Cores — usar tokens reais de egreen-design.md se carregado; usar genéricos abaixo se ausente */
      --brand-500: [hex de egreen-design.md ou #2563EB];
      --brand-400: [hex de egreen-design.md ou #3B82F6];
      --brand-100: [hex de egreen-design.md ou #DBEAFE];
      --neutral-900: [hex de egreen-design.md ou #111827];
      --neutral-600: [hex de egreen-design.md ou #4B5563];
      --neutral-50:  [hex de egreen-design.md ou #F9FAFB];
      --white: #FFFFFF;
      /* Tipografia — usar família de egreen-design.md se carregado */
      --font-display: [família de egreen-design.md ou 'Inter'], sans-serif;
      --font-body:    [família de egreen-design.md ou 'Inter'], sans-serif;
      /* Espaçamento (grade de 4) */
      --space-4:  4px;  --space-8:  8px;  --space-12: 12px;
      --space-16: 16px; --space-24: 24px; --space-32: 32px;
      --space-48: 48px; --space-64: 64px; --space-80: 80px;
      /* Raio */
      --radius-sm: 4px; --radius-md: 8px; --radius-lg: 16px; --radius-full: 9999px;
    }

    /* === RESET + BASE === */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: var(--font-body); color: var(--neutral-900); background: var(--white); line-height: 1.6; }
    img  { max-width: 100%; height: auto; display: block; }
    a    { text-decoration: none; }

    /* === LAYOUT === */
    .container { width: 100%; max-width: 720px; margin: 0 auto; padding: 0 var(--space-24); }
    section    { padding: var(--space-64) 0; }

    /* === BOTÃO CTA === */
    .cta-primary {
      display: block; width: 100%; max-width: 400px; margin: var(--space-24) auto 0;
      padding: var(--space-16) var(--space-32);
      background: var(--brand-500); color: var(--white);
      font-family: var(--font-display); font-size: 1.125rem; font-weight: 700;
      border-radius: var(--radius-md); text-align: center; cursor: pointer;
    }
    .cta-support { text-align: center; font-size: 0.875rem; color: var(--neutral-600); margin-top: var(--space-8); }

    /* === S1 ABOVE THE FOLD === */
    #s1-hero { background: var(--neutral-50); text-align: center; padding: var(--space-80) 0; }
    #s1-hero h1 { font-family: var(--font-display); font-size: 2rem; font-weight: 800; line-height: 1.2; margin-bottom: var(--space-16); }
    .subheadline { font-size: 1.125rem; color: var(--neutral-600); max-width: 560px; margin: 0 auto; }

    /* === S2 PROVA SOCIAL === */
    #s2-social-proof { background: var(--white); }
    .testimonial-grid { display: grid; gap: var(--space-24); margin-top: var(--space-32); }
    .testimonial-card { background: var(--neutral-50); border-radius: var(--radius-lg); padding: var(--space-24); }
    .testimonial-card blockquote { font-style: italic; margin-bottom: var(--space-12); }
    .testimonial-card cite { font-size: 0.875rem; font-weight: 600; color: var(--neutral-600); font-style: normal; }

    /* === S3 PROBLEMA === */
    #s3-problema { background: var(--neutral-50); }
    #s3-problema h2 { font-family: var(--font-display); font-size: 1.75rem; font-weight: 700; margin-bottom: var(--space-24); }
    #s3-problema p  { margin-bottom: var(--space-16); }

    /* === S4 MECANISMO === */
    #s4-mecanismo { background: var(--white); }
    #s4-mecanismo h2 { font-family: var(--font-display); font-size: 1.75rem; font-weight: 700; margin-bottom: var(--space-24); }
    .mechanism-name { font-size: 1.25rem; font-weight: 700; color: var(--brand-500); margin: var(--space-24) 0 var(--space-12); }

    /* === S5 VALUE STACK === */
    #s5-oferta { background: var(--neutral-50); }
    #s5-oferta h2 { font-family: var(--font-display); font-size: 1.75rem; font-weight: 700; margin-bottom: var(--space-32); }
    .value-stack          { border: 2px solid var(--brand-100); border-radius: var(--radius-lg); overflow: hidden; }
    .value-stack-item     { display: flex; justify-content: space-between; padding: var(--space-16) var(--space-24); border-bottom: 1px solid var(--brand-100); }
    .value-stack-item:last-child { border-bottom: none; }
    .value-stack-total    { background: var(--brand-100); font-weight: 700; }
    .price-real           { font-size: 2rem; font-weight: 800; color: var(--brand-500); }
    .price-original       { text-decoration: line-through; color: var(--neutral-600); font-size: 1rem; }

    /* === S6 CTA + GARANTIA + FAQ === */
    #s6-cta { background: var(--white); text-align: center; }
    #s6-cta h2 { font-family: var(--font-display); font-size: 1.75rem; font-weight: 700; margin-bottom: var(--space-24); }
    .garantia  { background: var(--neutral-50); border-radius: var(--radius-lg); padding: var(--space-24); margin: var(--space-32) auto; max-width: 480px; }
    .faq       { text-align: left; max-width: 600px; margin: var(--space-48) auto 0; }
    .faq details { border-bottom: 1px solid var(--brand-100); padding: var(--space-16) 0; }
    .faq summary { font-weight: 600; cursor: pointer; list-style: none; padding-right: var(--space-24); position: relative; }
    .faq summary::after { content: '+'; position: absolute; right: 0; }
    .faq details[open] summary::after { content: '−'; }
    .faq details p { margin-top: var(--space-12); color: var(--neutral-600); }

    /* === CTA STICKY MOBILE === */
    .cta-sticky { display: none; }
    @media (max-width: 767px) {
      .cta-sticky {
        display: block; position: fixed; bottom: 0; left: 0; right: 0;
        background: var(--white); padding: var(--space-12) var(--space-24);
        box-shadow: 0 -2px 16px rgba(0,0,0,0.1); z-index: 100;
      }
      .cta-sticky .cta-primary { margin: 0; }
      section { padding: var(--space-48) 0; }
    }

    /* === DESKTOP === */
    @media (min-width: 768px) {
      #s1-hero h1 { font-size: 2.75rem; }
      .testimonial-grid { grid-template-columns: repeat(3, 1fr); }
    }
  </style>
</head>
<body>

<!-- S1 ABOVE THE FOLD -->
<section id="s1-hero">
  <div class="container">
    [S1 conteúdo aprovado]
  </div>
</section>

<!-- S2 PROVA SOCIAL -->
<section id="s2-social-proof">
  <div class="container">
    [S2 conteúdo aprovado]
  </div>
</section>

<!-- S3 PROBLEMA -->
<section id="s3-problema">
  <div class="container">
    [S3 conteúdo aprovado]
  </div>
</section>

<!-- S4 MECANISMO -->
<section id="s4-mecanismo">
  <div class="container">
    [S4 conteúdo aprovado]
  </div>
</section>

<!-- S5 VALUE STACK -->
<section id="s5-oferta">
  <div class="container">
    [S5 conteúdo aprovado]
  </div>
</section>

<!-- S6 CTA + GARANTIA + FAQ -->
<section id="s6-cta">
  <div class="container">
    [S6 conteúdo aprovado]
  </div>
</section>

<!-- CTA STICKY MOBILE -->
<div class="cta-sticky">
  <a href="#s6-cta" class="cta-primary">[mesmo texto CTA de S1]</a>
</div>

</body>
</html>
```

### Confirmação obrigatória após salvar

```
✅ Salvo em: {pasta-ativa}/egreen-landing/YYYY-MM-DD-landing-{slug-produto}.html

Próximo passo: /egreen-meta-ads — subir campanha com a landing pronta
(ou /egreen-google-ads para campanhas no Google)
```

---

## O que esta skill NÃO faz

- Não audita landing pages existentes (sem URL)
- Não gera JavaScript interativo (countdown, pop-ups, animações)
- Não integra checkout — usar placeholder de link para Hotmart/Kiwify
- Não cria imagens — usar `<!-- PLACEHOLDER: nome-arquivo.jpg -->` no HTML
- Não define oferta ou bônus — lê de `egreen-funil.md` e/ou `egreen-copy`
