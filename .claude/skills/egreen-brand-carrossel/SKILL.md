---
name: egreen-brand-carrossel
description: >-
  Use quando o usuário pedir um carrossel de Instagram com identidade de marca do projeto,
  usando o design system Principal (headlines Impact/Anton, paleta índigo/rosa/papel, dados
  de marca de memoria/egreen-design.md). Também dispara com "/egreen-brand-carrossel", "carrossel editorial
  com marca", "carrossel Principal" ou qualquer pedido de carrossel que use a marca do projeto.
---


> **Marca = carregada de `memoria/egreen-design.md`.** HANDLE, TAGLINE, COPYRIGHT, LOGO e
> ASSINATURA vêm da memória do projeto — nunca inventar, nunca perguntar ao usuário.
> Se `memoria/egreen-design.md` estiver ausente ou com `status: vazio`, **PARE** e peça `/egreen-setup`.

> **Como usar:** ao invocar `/egreen-brand-carrossel`, forneça apenas TEMA, ÂNGULO e (opcionalmente)
> número de slides (Seção 2). O agente carrega a marca da memória (Seção 1, passo 0),
> segue o fluxo, monta do scaffold (Seção 5) e dos recipes (Seção 6), respeita os tokens
> (Seções 7–8) e termina pelo checklist (Seção 11).

---

## 1. Fluxo de geração (o que o agente faz)

0. **Carregar memória de marca** — ler `memoria/egreen-design.md` e extrair:
   HANDLE, TAGLINE, COPYRIGHT, LOGO (caminho do arquivo), ASSINATURA.
   Se ausente ou `status: vazio` → **PARAR. Executar `/egreen-setup` antes.**
   Se existir logo/imagem no campo LOGO → usar `background-image:url(...)` no `.avatar`;
   se for caminho relativo, resolver a partir da raiz do projeto.
1. **Ler o briefing** (Seção 2). Se faltar TEMA ou ÂNGULO, perguntar antes de prosseguir.
2. **Roteirizar:** quebrar o conteúdo em slides → escolher um **arquétipo** (Seção 6) para cada.
   - Slide 1 = sempre `cover`. Último = sempre `closing`.
   - Miolo alterna `solid` ↔ `photo`. Ver ritmo de cor na Seção 8.
3. **Marcar imagens:** cada slide com foto recebe um placeholder com instrução do que entra ali
   (ver Seção 9). Não desenhar ilustração no lugar da foto.
4. **Montar o HTML** a partir do scaffold (Seção 5) + colar os recipes (Seção 6),
   substituindo todos os `{{PLACEHOLDER}}` com os dados reais de `memoria/egreen-design.md`.
5. **Revisar** pelo checklist (Seção 11) e salvar em `carrossel/YYYY-MM-DD-carrossel-<slug>.html`.

**Saída:** um único arquivo HTML com todos os slides empilhados,
cada um exportável como imagem 1080×1350.

---

## 2. Formato de entrada (briefing)

O usuário fornece **apenas o conteúdo editorial**. Dados de marca vêm de `memoria/egreen-design.md`
(ver passo 0 do fluxo — nunca perguntar ao usuário).

Peça/aceite neste formato:

```md
TEMA: <assunto do carrossel>
ÂNGULO: <tese / recorte editorial>
SLIDES: 9            # opcional; padrão 6–9
CRÉDITO_IA: sim      # mostra crédito de IA no encerramento

# Roteiro (1 bloco por slide; o agente escolhe o arquétipo)
1. CAPA  — headline + gancho (pergunta)
2. ...   — headline + parágrafo(s)
...
```

Se vier só um texto corrido, o agente roteiriza sozinho e confirma a divisão.

---

## 3. Canvas

| Propriedade | Valor |
|---|---|
| Proporção | **4:5** (retrato Instagram) |
| Slide | **1080 × 1350 px** |
| Nº de slides | 6–9 |
| Cor | sRGB |

---

## 4. Estrutura de arquivos

```
/egreen-carrossel-<slug>.html      → todos os slides (este é o entregável)
/assets/                    → fotos finais (substituem os placeholders)
DESIGN_SYSTEM.md            → este guia
```

Mantenha tudo em **um HTML**. Fotos entram via `background-image` em `.photo` /`.img-card`
(ou nos placeholders enquanto não há imagem real).

---

## 5. Scaffold base (copiar como início do HTML)

Inclui import de fontes, tokens, o "palco" de cada slide e o header "Infos".
Cada slide é uma `<section class="slide ...">`.

```html
<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<title>Carrossel — Principal</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;900&family=Anton&display=swap" rel="stylesheet">
<style>
  :root{
    --c-indigo:#2C1950; --c-pink:#FF3B55; --c-paper:#F5F5F5; --c-black:#000;
    --c-text-light:#F5F5F5; --c-text-dark:#2C1950; --c-headline-pink:#FF3B55;
    /* Headline: Impact é a fonte do projeto; Anton é fallback web fiel (condensada/impactante) */
    --f-display:"Impact","Haettenschweiler","Anton",sans-serif;
    --f-body:"Inter",system-ui,sans-serif;
  }
  *{margin:0;padding:0;box-sizing:border-box}
  body{background:#111;display:flex;flex-direction:column;align-items:center;gap:24px;padding:24px}

  /* Palco: cada slide é 1080x1350 fixo */
  .slide{
    position:relative; width:1080px; height:1350px; overflow:hidden;
    font-family:var(--f-body); color:var(--c-text-light);
    flex:none;
  }
  .slide--indigo{background:var(--c-indigo)}
  .slide--pink{background:var(--c-pink)}
  .slide--paper{background:var(--c-paper)}

  /* Foto full-bleed + gradiente de legibilidade */
  .photo{position:absolute;inset:0;background-position:center;background-size:cover}
  .photo::after{content:"";position:absolute;inset:0;
    background:linear-gradient(rgba(0,0,0,0) 0%, rgba(0,0,0,.92) 100%)}

  /* Header "Infos" (em todos os slides) */
  .infos{position:absolute;top:24px;left:38px;right:38px;z-index:5;
    display:flex;justify-content:space-between;
    font-weight:700;font-size:11px;letter-spacing:0;text-transform:uppercase;
    color:var(--c-text-light)}
  .infos .right{display:flex;gap:40px}

  /* Tipografia */
  .display{font-family:var(--f-display);text-transform:uppercase;line-height:.95;
    letter-spacing:-2px;font-weight:400}
  .display--xl{font-size:120px;line-height:.92;letter-spacing:-3px}
  .display--lg{font-size:96px}
  .lead{font-weight:500;font-size:38px;line-height:1.22;letter-spacing:-1.5px}
  .body{font-weight:400;font-size:38px;line-height:1.22;letter-spacing:-1px}
  .emph{font-weight:700;font-size:40px;line-height:1.26;letter-spacing:-1.5px}
  .closing{font-weight:400;font-size:60px;line-height:1.08;letter-spacing:-2px}
  .caption{font-weight:700;font-size:28px;line-height:1.2;letter-spacing:-1px;text-transform:uppercase}

  /* Blocos de conteúdo */
  .content{position:absolute;left:38px;right:38px;top:120px;
    display:flex;flex-direction:column;gap:32px;z-index:2}
  .content--bottom{top:auto;bottom:56px;gap:32px}        /* foto/encerramento */
  .content--cover{top:auto;bottom:57px;gap:27px;align-items:center;text-align:center}
  .img-card{width:100%;border-radius:8px;background-position:center;background-size:cover}

  /* Chip de perfil */
  .perfil{display:flex;align-items:center;gap:18px}
  .perfil .avatar{width:57px;height:57px;border-radius:50%;
    background:#888 center/cover}
  .perfil .handle{font-weight:500;font-size:28px;letter-spacing:-.06em}
  .perfil .verified{width:24px;height:24px;border-radius:50%;
    background:#1d9bf0;display:grid;place-items:center;color:#fff;font-size:14px;font-weight:700}

  /* Chip de seta (indicador "continua") */
  .seta{width:44px;height:44px;border-radius:50%;background:var(--c-pink);
    display:grid;place-items:center;transform:rotate(15deg)}
  .seta svg{width:20px;height:20px;stroke:var(--c-paper);stroke-width:2;fill:none}

  /* Placeholder de imagem (enquanto não há foto real) */
  .ph{display:grid;place-items:center;background:repeating-linear-gradient(45deg,#3a3a3a,#3a3a3a 12px,#444 12px,#444 24px);
    color:#bbb;font-size:22px;text-align:center;padding:24px}
</style>
</head>
<body>

  <!-- COLE OS SLIDES AQUI (Seção 6) -->

</body>
</html>
```

> **Fonte da headline:** o projeto original usa **Impact** (instalada no sistema).
> Na web, o fallback `Anton` (Google Fonts, já importado) reproduz o caráter condensado
> e pesado com fidelidade. Mantenha MAIÚSCULA + tracking negativo.

---

## 6. Recipes de slide (copiar e preencher)

### A. `cover` — Capa (foto + headline + gancho)
```html
<section class="slide slide--indigo" data-screen-label="01">
  <header class="infos"><span>{{HANDLE}}</span>
    <span class="right"><span>{{TAGLINE}}</span><span>{{COPYRIGHT}}</span></span></header>
  <div class="photo ph" style="background-image:none">FOTO DE CAPA — tema do post, vertical</div>
  <div class="content content--cover">
    <div class="perfil"><div class="avatar"><!-- {{LOGO}} --></div>
      <span class="handle">{{HANDLE}}</span><span class="verified">✓</span></div>
    <h1 class="display display--xl">Headline curta e provocativa</h1>
    <p class="caption">Gancho em forma de pergunta?</p>
  </div>
</section>
```

### B. `solid` — Sólido com imagem (headline → card → tese)
```html
<section class="slide slide--pink" data-screen-label="02">
  <header class="infos"><span>{{HANDLE}}</span>
    <span class="right"><span>{{TAGLINE}}</span><span>{{COPYRIGHT}}</span></span></header>
  <div class="content">
    <h2 class="display display--lg">Afirmação em maiúscula.</h2>
    <div class="img-card ph" style="height:600px">FOTO — apoio ao argumento</div>
    <p class="emph" style="color:var(--c-text-dark)">Parágrafo-tese em destaque (negrito).</p>
  </div>
</section>
```
*Variante "respiro":* troque por `slide--paper`, headline com `style="color:var(--c-headline-pink)"`,
parágrafo com `class="emph" style="color:var(--c-text-dark)"`.
*Em `slide--indigo`:* headline pode ser `--c-pink` ou `--c-paper`; corpo `--c-paper`.

### C. `photo` — Foto/citação (seta → condução → continuação)
```html
<section class="slide slide--indigo" data-screen-label="03">
  <header class="infos"><span>{{HANDLE}}</span>
    <span class="right"><span>{{TAGLINE}}</span><span>{{COPYRIGHT}}</span></span></header>
  <div class="photo ph" style="background-image:none">FOTO full-bleed — protagonista</div>
  <div class="content content--bottom" style="gap:48px">
    <div class="seta"><svg viewBox="0 0 24 24"><path d="M4 12h16M14 6l6 6-6 6"/></svg></div>
    <p class="lead">Parágrafo de condução: dado + leitura.</p>
    <p class="body">Parágrafo de continuação que aprofunda.</p>
  </div>
</section>
```

### D. `closing` — Encerramento (perfil → frase/crédito)
```html
<section class="slide slide--pink" data-screen-label="09">
  <header class="infos"><span>{{HANDLE}}</span>
    <span class="right"><span>{{TAGLINE}}</span><span>{{COPYRIGHT}}</span></span></header>
  <div class="photo ph" style="background-image:none">FOTO — close de produto/marca</div>
  <div class="content content--bottom" style="gap:35px">
    <div class="perfil"><div class="avatar"><!-- {{LOGO}} --></div>
      <span class="handle">{{HANDLE}}</span><span class="verified">✓</span></div>
    <p class="closing">Produzido com apoio de Inteligência Artificial.</p>
  </div>
</section>
```

---

## 7. Tipografia (referência rápida)

| Classe | Família / peso | Tamanho | LH | Tracking | Uso |
|---|---|---|---|---|---|
| `.display--xl` | Impact/Anton | 100–134px | 0.92 | −3px | headline de capa/forte |
| `.display--lg` | Impact/Anton | 96–102px | 0.95 | −2/−3px | headline de slide |
| `.lead` | Inter Medium 500 | 36–40px | 1.22 | −1.5px | parágrafo de condução |
| `.emph` | Inter Bold 700 | 38–42px | 1.26 | −1.5px | parágrafo-tese (destaque) |
| `.body` | Inter Regular 400 | 38–40px | 1.22 | −1px | continuação |
| `.closing` | Inter Regular 400 | 60px | 1.08 | −2px | frase de encerramento |
| `.caption` | Inter Bold 700 | 28px | 1.2 | −1px | gancho da capa (MAIÚSC.) |
| `.infos` | Inter Bold 700 | 11px | 100% | 0 | header (MAIÚSC.) |
| `.handle` | Inter Medium 500 | 28px | 100% | −0.06em | @ do perfil |

Headlines **sempre maiúsculas**, line-height < 1. Um parágrafo-tese em negrito por slide.

---

## 8. Cor & ritmo

```css
--c-indigo:#2C1950;  --c-pink:#FF3B55;  --c-paper:#F5F5F5;  --c-black:#000;
```

| Fundo | Headline | Corpo |
|---|---|---|
| `--c-indigo` | `--c-pink` ou `--c-paper` | `--c-paper` |
| `--c-pink` | `--c-paper` | `--c-indigo` (negrito) / `--c-paper` |
| `--c-paper` | `--c-pink` | `--c-indigo` |
| foto+gradiente | `--c-paper` | `--c-paper` |

- **Alterne indigo ↔ rosa** entre slides do miolo.
- No máximo **1 slide claro** (`--c-paper`) por carrossel.
- Toda foto full-bleed leva o gradiente preto (já no `.photo::after`).
- Nunca rosa-sobre-rosa nem texto escuro sobre indigo.

---

## 9. Imagens

- Slides de foto usam placeholder `.ph` com **instrução do que entra** ("FOTO — close do produto").
- Não gerar ilustração/SVG no lugar de fotografia. Placeholder > foto errada.
- Ao receber assets reais: `background-image:url(assets/xxx.jpg)` em `.photo`/`.img-card`,
  remover a classe `.ph` e o texto.
- `.img-card` sempre com `border-radius:8px` (já no CSS).

---

## 10. Tom & conteúdo

- Português (BR), registro editorial-analítico.
- Headline: afirmação curta em MAIÚSCULA. Capa traz **gancho** (pergunta).
- Corpo: dado + interpretação; um parágrafo-tese em negrito por slide.
- Encerramento credita IA (se `CRÉDITO_IA: sim`) e repete o perfil.
- **Sem emoji. Sem hashtag** nos slides.

---

## 11. Checklist (rodar antes de entregar)

- [ ] Todos os slides 1080×1350 com header "Infos".
- [ ] Slide 1 = `cover` (perfil + gancho). Último = `closing` (perfil + crédito).
- [ ] Headlines Impact/Anton MAIÚSCULA, LH < 1, tracking apertado.
- [ ] Um parágrafo-tese em negrito por slide; corpo com tracking −1/−2px.
- [ ] Fundos alternam indigo ↔ rosa; no máx. 1 slide claro.
- [ ] Toda foto tem gradiente; placeholders com instrução clara.
- [ ] `.img-card` com radius 8px. Sem cores/fontes fora dos tokens.

---

## 12. Variantes irmãs

"Principal" é 1 de 4 estilos da mesma família (formato, header e tom iguais):
**Principal** (este), **Futurista**, **Autoral**, **Twitter**. Para um novo estilo,
herde Seções 1–6 e 9–11; redefina apenas tipografia (7) e cor (8).

---

## 13. Limites de caracteres por caixa de texto (verificado no Figma)

Medições extraídas dos 8 frames originais (4 templates × 2 variações de cor).
**As 2 variações de cor de cada template usam o MESMO texto** — só muda o `{{HANDLE}}`
entre as variações de uma mesma conta. Portanto a contagem por caixa é idêntica
entre as duas cores. Os valores de marca (`{{HANDLE}}`, `{{TAGLINE}}`, etc.) NÃO contam
para os limites de copy abaixo — são preenchidos pela pessoa.

> Contagem inclui espaços, acentos e pontuação; quebra de linha conta como 1.
> "Observado" = faixa real nos posts; "Limite" = teto recomendado para o copy caber
> sem estourar a caixa (o tamanho da fonte do headline **diminui conforme o texto cresce**).

### 13.1 Principal — 9 slides (headline Impact)

| Caixa | Papel | Fonte / tam. | Observado | **Limite** |
|---|---|---|---|---|
| `@handle` | perfil | Inter Medium 28 | 14–16 | **20** |
| capa: headline | título de capa | Impact 113 | 73 | **75** |
| capa: gancho | subtítulo/pergunta | Inter Bold 28 | 32 | **40** |
| headline de slide | título | Impact 96–134 | 24–46 | **50** |
| corpo-tese | destaque (negrito) | Inter Bold 38–42 | 181–248 | **250** |
| corpo-condução | lead | Inter Medium 36–40 | 162–193 | **195** |
| corpo-continuação | texto | Inter Regular 38–40 | 142–173 | **175** |
| encerramento | frase final | Inter Regular 60 | 47 | **55** |

*Headline Impact escala inversa: 24 chars → 134px; 46 chars → 96px; 73 chars → 113px (capa, 3 linhas).*

### 13.2 Futurista — headline Inter pesado + títulos gigantes

| Caixa | Papel | Fonte / tam. | Observado | **Limite** |
|---|---|---|---|---|
| `@handle` | perfil | Inter Medium 28 | 14–16 | **20** |
| capa: headline | título de capa | Inter Bold 95 | 53 | **55** |
| capa: subtítulo | apoio da capa | Inter Bold 40 | 62 | **65** |
| título de seção | título gigante | Inter Medium/Reg 116–128 | 22–33 | **35** |
| corpo grande | lead destacado | Inter Medium 48–64 | 104–172 | **175** |
| corpo | texto | Inter Medium 36–38 | 181–192 | **195** |
| label "arraste" | UI | Inter Bold 18 | 19 | **20** |

### 13.3 Autoral — Instrument Serif + Inter Bold (expressivo)

| Caixa | Papel | Fonte / tam. | Observado | **Limite** |
|---|---|---|---|---|
| `@handle` | perfil | Inter Medium 28 | 14 | **20** |
| display serif (capa) | título de capa | Instrument Serif 96 | 116 | **120** |
| display serif (seção) | título curto | Instrument Serif 128 | 39 | **45** |
| frase-impacto grande | destaque | Inter Bold 60–104 | 27–123 | **125** |
| frase-impacto média | subtítulo | Inter Bold 50–67 | 117–161 | **165** |
| corpo | texto | Inter Medium/Bold 38–40 | 136–224 | **225** |
| assinatura | rodapé de marca | Inter Regular 54 | 14 | **20** |

### 13.4 Twitter — tudo Inter 39px, linhas curtas tipo tweet

| Caixa | Papel | Fonte / tam. | Observado | **Limite** |
|---|---|---|---|---|
| `Nome` | nome de exibição | Inter Medium 43 | 18 | **22** |
| `@handle` | perfil | Inter Medium 39 | 14 | **20** |
| linha-afirmação | frase curta/punch | Inter Medium/Bold 39 | 23–75 | **80** |
| linha-corpo | frase longa | Inter Medium/Bold 39 | 103–110 | **115** |
| assinatura | rodapé de marca | Inter Regular 75 | 14 | **20** |

*No Twitter, cada slide é uma sequência de linhas curtas (até ~24 linhas/post). Alterne
Medium (afirmação) e Bold (ênfase). Mantenha cada linha como uma frase fechada.*

### 13.5 Regra geral de copy

- **Headline:** quanto mais curto, maior a fonte — prefira 1 ideia por título.
- **Corpo:** ~1 parágrafo-tese (negrito) + 1 de apoio por slide; respeite os limites acima.
- Se o texto exceder o limite, **encurte o copy** antes de reduzir a fonte abaixo da escala (Seção 7).
