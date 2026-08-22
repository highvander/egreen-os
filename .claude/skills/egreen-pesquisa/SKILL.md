---
name: egreen-pesquisa
description: >-
  Faz pesquisa de mercado profunda e estruturada de um nicho de infoproduto, em 9 eixos (tamanho de mercado, concorrentes, faixa de preço, público-alvo, objeções reais, assuntos quentes, YouTube Top 10, biblioteca de anúncios e riscos regulatórios), com busca real na web. Entrega o relatório em markdown e, quando chamada diretamente pelo usuário, oferece também uma página HTML visual no estilo shadcn (fundo branco, sem serifa, sem emoji, com gráficos SVG inline em todos os 9 eixos) como segunda etapa opcional. Use quando o usuário pedir pesquisa de mercado de um nicho, ou quando as skills ideias-de-produto ou produto-concepcao precisarem da pesquisa antes de gerar ideias, identidades, preço ou argumentos.
---

# Pesquisa de Mercado. 9 Eixos com Busca Real

Skill autossuficiente. Pesquisa um nicho de infoproduto a fundo e entrega um
relatório estruturado de 9 eixos. Pode rodar sozinha ou ser acionada por outra
skill de concepção de produto.

> **Idioma:** responda sempre em português do Brasil, com acentuação correta.
> **Travessão proibido** em qualquer texto gerado. Use vírgula, ponto ou dois
> pontos.
> **Emoji proibido** em qualquer texto gerado, em markdown ou em HTML.
> **Serifa proibida** no HTML. Só fontes sans-serif geométricas.

---

## OBRIGATÓRIO. Buscas reais, eixo por eixo

Esta skill só tem valor se fizer buscas reais na ferramenta de busca da web. É
proibido escrever qualquer eixo a partir só do seu conhecimento interno.

Anuncie ao usuário antes de começar:

```
Vou pesquisar o mercado de {nicho} agora. Leva alguns minutos.
```

### Plano de buscas obrigatório

Você DEVE executar, no mínimo, as 13 buscas abaixo, uma a uma. Adapte os termos
ao nicho do produto, substituindo `{nicho}`. Não pule nenhuma. Os eixos 5, 6,
8 e 9 são os mais esquecidos e têm busca própria e obrigatória aqui.

1. Eixo 1. `{nicho} mercado Brasil tamanho crescimento dados`
2. Eixo 2. `curso {nicho} online concorrentes`
3. Eixo 2. `{nicho} infoproduto Hotmart Kiwify`
4. Eixo 3. `{nicho} curso online quanto custa preço`
5. Eixo 4. `{nicho} público perfil idade quem busca`
6. Eixo 5. `{nicho} reclame aqui reclamação curso`
7. Eixo 5. `{nicho} curso não funcionou opinião negativa`
8. Eixo 6. `{nicho} assuntos em alta tendências 2025`
9. Eixo 7. `{nicho} youtube vídeos mais vistos canal`
10. Eixo 7. `{nicho} youtube tutorial iniciante mais assistido`
11. Eixo 8. `biblioteca de anúncios Meta {nicho}` ou `{nicho} anúncios Facebook Instagram`
12. Eixo 9. `{nicho} regras anúncio promessa proibida`
13. Eixo 9. `{nicho} polêmica processo crítica`

Se um eixo vier fraco depois da busca, faça uma busca extra com outros termos.

### Aprofundar abrindo as páginas reais (obrigatório)

A busca só traz título e trecho. Para ter dado real, você DEVE abrir as páginas
com a ferramenta de abrir páginas da web (WebFetch ou equivalente):

- **Concorrentes (eixos 2 e 3).** Para cada concorrente, abra a página de
  vendas real e pegue o preço real, os entregáveis e os bônus. Só escreva
  "preço não divulgado" se a página realmente não mostrar o preço. É proibido
  escrever "preço estimado" sem ter aberto a página antes.
- **Reclame Aqui (eixo 5).** Abra o reclameaqui.com.br e procure pelos nomes
  dos concorrentes e por termos do nicho. Leia as reclamações reais. Se o nicho
  tiver pouca ou nenhuma reclamação lá, isso também é um achado: registre no
  relatório de forma explícita e diga de onde vieram as objeções no lugar
  (comentários de YouTube, fóruns, blogs).
- **YouTube (eixo 7).** Abra ou inspecione os vídeos do Top 10 para pegar
  título exato, canal, visualizações e comentários reais.

Abra no mínimo 5 páginas reais por pesquisa. Se a ferramenta de abrir páginas
não existir no ambiente, registre no relatório que os dados vieram da busca e
não da página aberta.

### Trava antes de escrever o relatório

Antes de montar o relatório, confira: cada um dos 9 eixos teve busca real
própria? Você abriu as páginas de vendas dos concorrentes para pegar o preço
real? Você investigou o Reclame Aqui de verdade, abrindo o site e procurando o
nicho? Os eixos 8 (biblioteca de anúncios) e 9 (riscos) tiveram busca dedicada?
Se algo faltou, faça agora. Só escreva o relatório depois disso.

### Sem busca na web no ambiente

Se o ambiente onde você roda não tiver ferramenta de busca na web, avise o
usuário em uma linha que a pesquisa será baseada em conhecimento geral, sem
dados atualizados, e só então prossiga.

---

## Os 9 eixos

Pesquise e organize cada um. Se um eixo vier vazio, tente uma segunda busca com
termos diferentes antes de marcar "sem dados".

1. **Tamanho e saúde do mercado.** Estimativa de tamanho no Brasil, tendência
   de crescimento, sazonalidade. Fontes: SEBRAE, IBGE, Google Trends,
   relatórios setoriais, associações do nicho.
2. **Concorrentes (mínimo 10).** Diretos, indiretos e referências
   aspiracionais. Para cada um: nome, link real da página, promessa principal,
   entregáveis, bônus, preço, diferencial aparente. Marque quais são top of
   mind e quais são aspiracionais. Monte uma tabela. Proibido usar URL de busca
   como link (google.com/search, youtube.com/results). Se não achou o link
   real, escreva "link indisponível".
3. **Faixa de preço.** Menor preço, maior preço e faixa mais comum. Relação
   entre preço e formato (e-book, mini-curso, curso completo, mentoria, grupo).
   Ofertas e parcelamentos típicos do nicho. Cases de preço fora da curva e por
   quê. Ao final, sugira uma faixa de preço para um produto novo no nicho, com
   raciocínio baseado nos dados.
4. **Público-alvo real.** Demografia (idade, gênero, classe, região),
   comportamento (onde consome, como compra), situações de vida típicas que
   levam à busca, e o nível de consciência dominante (escala de Schwartz:
   inconsciente do problema, consciente do problema, consciente da solução,
   consciente do produto, totalmente consciente).
5. **Objeções reais (mínimo 10).** Investigue o Reclame Aqui de verdade,
   abrindo o site e procurando os nomes dos concorrentes e termos do nicho, e
   também fóruns e comentários. No relatório, deixe explícito o que a busca no
   Reclame Aqui encontrou. Se o nicho tiver pouca presença lá, diga isso e
   aponte de onde vieram as objeções. Cada objeção precisa de evidência de
   fonte. Traduza cada padrão de queixa em uma objeção antecipável.
6. **Assuntos quentes e ângulos virais.** Termos de busca em alta, conteúdos
   virais recentes, ganchos que estão performando em conteúdo e anúncio.
7. **YouTube Top 10.** Os 10 vídeos mais relevantes do nicho. Priorize vídeos
   ligados ao tema do produto, no máximo 2 por canal, descarte clickbait sem
   relação real. Para cada um: título exato, canal e número de inscritos,
   link, visualizações aproximadas com a data da consulta, data de publicação,
   3 a 5 comentários mais curtidos, a thumbnail descrita (cores dominantes,
   expressão facial, texto em destaque, elementos visuais, composição), o
   ângulo do título e a lacuna que o vídeo não cobre. Ao final, sintetize os
   padrões observados nos 10: thumb dominante, gancho de título dominante, dor
   ou desejo dominante nos comentários, lacunas de conteúdo do mercado.
8. **Biblioteca de anúncios.** Anúncios ativos há mais de 30 dias no nicho
   (alta chance de estarem funcionando) e anúncios com muitas variações (sinal
   de otimização). Padrões de headline, gancho, oferta e CTA que se repetem. Se
   o acesso direto não for possível, use pesquisa web para identificar
   criativos conhecidos do nicho.
9. **Riscos regulatórios.** Regras específicas do nicho (saúde, finanças),
   palavras e promessas que dão problema em anúncio, histórico de polêmicas.

---

## Regras de rigor

- Nunca invente dado nem fonte. Se não achou, escreva "sem dados disponíveis".
- Todo número tem origem em uma busca real. Os concorrentes do eixo 2 levam o
  link real da página.
- Resuma com palavras próprias, sem copiar trecho de fonte externa.
- Sem travessão, sem ponto de exclamação e sem emoji no relatório.

---

## Estrutura do relatório

Monte o relatório nesta ordem:

```markdown
# Pesquisa de Mercado. {Nicho}

**Data:** {data}
**Nicho:** {nicho}

## 1. Tamanho e saúde do mercado
{estimativa, tendência, sazonalidade, com fontes}

## 2. Concorrentes
| # | Nome | Link | Promessa | Entregáveis | Bônus | Preço | Diferencial |
|---|------|------|----------|-------------|-------|-------|-------------|
{mínimo 10 linhas}

## 3. Faixa de preço praticada
{menor, maior, faixa comum, relação preço x formato, sugestão de preço}

## 4. Público-alvo real
{demografia, comportamento, situações de vida, nível de consciência Schwartz}

## 5. Objeções reais
{Comece com uma linha sobre o que a investigação no Reclame Aqui encontrou.
Depois liste no mínimo 10 objeções, cada uma com a evidência de origem}

## 6. Assuntos quentes
{termos em alta, conteúdos virais, ganchos}

## 7. YouTube Top 10
{os 10 vídeos com os campos pedidos, mais os padrões observados}

## 8. Biblioteca de anúncios
{padrões de headline, oferta e CTA}

## 9. Riscos regulatórios
{regras do nicho, palavras a evitar, polêmicas}

## Oportunidades e lacuna de posicionamento
{o que o mercado não faz e um produto novo pode ocupar}

## Cuidados e riscos
{o que evitar}

## Confiança geral da pesquisa
{Alta, Média ou Baixa, com a justificativa: quantidade e qualidade das fontes
cruzadas, quantos eixos vieram com dado real}
```

---

## Como entregar

A entrega depende de como você foi acionada.

### Caso 1. Acionada por outra skill (ideias-de-produto ou produto-concepcao)

Produza o relatório completo em markdown dos 9 eixos e devolva o controle para
a skill que chamou. Ela vai usar o relatório para gerar as ideias, as
identidades e a Seção de Pesquisa do documento do produto. **Não gere HTML
neste caso** e não encerre a conversa.

### Caso 2. Acionada diretamente pelo usuário (fluxo de 2 etapas)

**Etapa 1. Entregar o markdown.** Apresente um resumo conversacional dos
achados (números e insights principais, não o relatório inteiro), salve o
relatório completo em `pesquisa-mercado-{nicho}.md` e disponibilize no chat
para o usuário baixar.

**Etapa 2. Oferecer o HTML.** Logo depois de entregar o markdown, faça esta
pergunta:

```
Pesquisa concluída. Posso gerar também uma página HTML visual com esse
relatório, com gráficos em todos os 9 eixos?

1. Sim, gerar o HTML
2. Não, só o markdown está ótimo

Digite o número:
```

Se o usuário responder 1, siga para a seção "Geração do HTML" abaixo. Se 2,
encerre confirmando que o markdown está pronto.

A separação em 2 etapas é proposital: gerar o HTML com os gráficos é uma
operação pesada que pode estourar o contexto se feita junto da pesquisa.
Quebrar em duas mensagens dá fôlego ao Claude Chat e deixa o usuário pular o
HTML quando não precisar do visual.

---

## Geração do HTML

Quando o usuário pedir o HTML:

1. Carregue `references/template-relatorio.html`.
2. Preencha cada placeholder `{{NOME}}` com os dados da pesquisa que você
   acabou de fazer. Os placeholders e o formato esperado de cada um estão
   documentados como comentários HTML dentro do próprio template.
3. **Não altere o CSS nem a estrutura do template.** Só troque os
   placeholders e gere os SVGs nos slots de gráficos. Mantenha as 9 seções,
   os 4 stats da capa, a tabela de concorrentes, os cards do YouTube, a
   síntese de oportunidades e o bloco de confiança da pesquisa.
4. Salve o resultado em `pesquisa-mercado-{nicho}.html` e disponibilize no
   chat para o usuário baixar.

### Regras de preenchimento

- **Light Copy.** Sem travessão, sem ponto de exclamação, sem lero-lero, sem
  emoji. Os textos dentro dos placeholders seguem as mesmas regras do
  relatório markdown.
- **Dados ausentes.** Se um eixo veio "sem dados disponíveis" da pesquisa,
  escreva isso no lugar do placeholder, não invente conteúdo.
- **Capa.** O título da capa traz o nicho em peso 700 com tracking apertado,
  formato direto sem floreios. Se o nicho for muito longo, use uma palavra
  curta auxiliar como subtítulo em `{{NICHO_SUBTITULO}}`. Caso contrário,
  deixe vazio.
- **4 stats principais da capa.** Escolha os 4 indicadores mais úteis da
  pesquisa para os cards da capa. Sugestões: tamanho do mercado em R$,
  preço médio praticado, faixa etária dominante, número de concorrentes
  mapeados, número de objeções, ticket teto do nicho. O valor deve caber em
  uma linha curta (ex: "R$ 2,3 bi", "R$ 497", "35-45", "12 críticas").
- **HTML self-contained.** O template já carrega Google Fonts via CDN. Não
  adicione bibliotecas externas, não troque a tipografia, não troque a
  paleta. O design é fixo (clean minimalista estilo shadcn, fundo branco,
  fonte Inter sem serifa, sem emoji, paleta neutra com acentos coloridos
  controlados).
- **Caracteres especiais.** Use entidades HTML quando necessário (`&amp;`,
  `&lt;`, `&gt;`, `&quot;`), especialmente dentro dos cards do YouTube e nas
  células da tabela.

---

## Gráficos obrigatórios por eixo

Cada eixo do HTML tem um slot de gráfico (placeholder `{{EIXO_X_GRAFICO_SVG}}`)
que você DEVE preencher com um SVG inline gerado a partir dos dados da
pesquisa. SVG só, sem JavaScript, sem biblioteca externa. Visual estilo
shadcn: grid suave, barras com cantos arredondados, paleta controlada,
rótulos em fonte Inter pequena e em cinza.

### Paleta de gráficos disponível

Use só essas cores nos SVGs, todas já definidas como CSS variables no template:

| Variável     | Hex      | Quando usar                                 |
|--------------|----------|---------------------------------------------|
| `--chart-1`  | #0EA5E9  | Cor principal de barras e séries primárias  |
| `--chart-2`  | #10B981  | Segunda série, positivos, crescimento       |
| `--chart-3`  | #F59E0B  | Terceira série, atenção, intermediário      |
| `--chart-4`  | #8B5CF6  | Quarta série, segmento alternativo          |
| `--chart-5`  | #EF4444  | Quinta série, riscos, valores críticos      |
| `--border`   | #E5E7EB  | Linhas de grid e separadores                |
| `--muted-fg` | #71717A  | Rótulos de eixo e legendas                  |
| `--fg`       | #0A0A0A  | Rótulos de destaque                         |

Use cores diretas no SVG (não use `var()` dentro de SVG inline porque atributos
SVG não resolvem CSS variables de forma confiável em todos os renderizadores).
Cole os hexadecimais.

### Regras gerais dos SVGs

- Toda barra tem `rx="3"` para canto arredondado suave.
- Grid em `stroke="#E5E7EB"` com `stroke-width="1"`. Linha principal sólida,
  auxiliares com `stroke-dasharray="2 3"`.
- Rótulos em `font-family="Inter, sans-serif"`, `font-size="11"`,
  `fill="#71717A"`. Valores em destaque em `fill="#0A0A0A"` e `font-weight="600"`.
- Cada SVG tem `viewBox` declarado e `preserveAspectRatio="xMidYMid meet"`.
  O CSS faz o SVG ocupar 100% da largura do card.
- Sem títulos dentro do SVG (o título e a descrição já estão no card que
  envolve, em HTML). Sem emojis e sem ícones decorativos.
- Sem animação. Sem `<style>` interno. Sem JavaScript.

### Especificação por eixo

**Eixo 1, Tamanho e saúde do mercado.** Gráfico de barras verticais com 4 a 6
barras mostrando a evolução do mercado por ano (ex: 2022, 2023, 2024, 2025,
2026 estimado). Última barra com fill mais suave (opacidade .5) para indicar
projeção. Eixo Y opcional implícito. Rótulos abaixo das barras com o ano,
rótulos acima das barras com o valor (R$ X bi). Se o nicho não tiver série
temporal, faça barras comparativas (Brasil vs LatAm vs Mundo, ou segmentos do
mercado).

**Eixo 2, Concorrentes.** Gráfico de barras horizontais com os 5 a 8 maiores
concorrentes ordenados por preço (mais caro no topo). Concorrentes sem preço
divulgado vão para uma seção separada do gráfico como "Preço não divulgado"
em barras cinza claras (fill #E5E7EB). Use `--chart-1` para os que têm preço
real.

**Eixo 3, Faixa de preço.** Gráfico de range bars (barras com início e fim)
mostrando a faixa de preço de cada formato (Ebook, Mini curso, Curso completo,
Curso premium, Mentoria). Cada formato vira uma linha do gráfico com a barra
indo do min ao max e um marcador (pequeno círculo) no preço típico.

**Eixo 4, Público-alvo.** Dois gráficos lado a lado dentro do mesmo card.
Primeiro: donut/anel mostrando a divisão por gênero ou por tribo de público.
Segundo: barras horizontais com a prevalência do problema por faixa etária
(ex: 13-22, 23-29, 30-39, 40-49, 50+).

**Eixo 5, Objeções.** Gráfico de barras horizontais com as 8 a 12 objeções
ordenadas por frequência observada (estimativa qualitativa de 1 a 10). Texto
curto em cada barra (até 5 palavras). Use `--chart-5` (vermelho) para as 3
objeções mais críticas, `--chart-3` (âmbar) para as intermediárias e
`--chart-1` (azul) para o resto.

**Eixo 6, Assuntos quentes.** Visualização de tags com tamanho proporcional.
Em vez de SVG complexo, use 10 a 20 tags em diferentes tamanhos de fonte (de
11px a 22px) e níveis de cinza, todas dentro do bloco `{{EIXO_6_TERMOS}}`.
A "vis" aqui é tipográfica. Não precisa SVG. Para o slot
`{{EIXO_6_GRAFICO_SVG}}` faça um gráfico de barras horizontais com os 5
termos de busca mais quentes e sua intensidade relativa (1 a 100), estimada
qualitativamente pelos achados das buscas.

**Eixo 7, YouTube Top 10.** Os cards do top 10 já são a vis primária. Para o
slot `{{EIXO_7_GRAFICO_SVG}}` faça um gráfico de barras horizontais simples
contando os formatos de conteúdo observados nos 10 vídeos (ex: rotina diária,
antes e depois, dermato responde, jornada pessoal, ranking de produtos). Cada
barra mostra quantos dos 10 caem naquele formato.

**Eixo 8, Biblioteca de anúncios.** Gráfico de barras horizontais com a
frequência de cada padrão de criativo observado (ex: depoimento em vídeo,
antes e depois, lista numerada, contagem regressiva, dermato fala). Cada barra
de 0 a 10 representando quão dominante é o padrão.

**Eixo 9, Riscos regulatórios.** Matriz de risco (grid 3x3) com os 4 a 6
riscos principais posicionados como pontos. Eixos: severidade (baixa, média,
alta) na vertical, probabilidade (baixa, média, alta) na horizontal. Pontos
maiores e em `--chart-5` para alta severidade e alta probabilidade. Pontos
menores em `--chart-3` para casos intermediários. Legenda dos pontos
numerados ao lado.

### Quando faltar dado para o gráfico

Se um eixo veio com pouco dado real, NÃO invente números para popular o
gráfico. Substitua o SVG por um bloco de texto dentro do mesmo `chart-card`:

```html
<div class="chart-empty">Sem dados suficientes para visualizar este eixo.</div>
```

A classe `chart-empty` já está no CSS do template.

---

## Lista completa de placeholders do template

Capa: `{{NICHO}}`, `{{NICHO_SUBTITULO}}`, `{{DATA}}`, `{{N_CONCORRENTES}}`,
`{{N_OBJECOES}}`, `{{CONFIANCA}}`, `{{STAT_1_VALOR}}`, `{{STAT_1_LABEL}}`,
`{{STAT_2_VALOR}}`, `{{STAT_2_LABEL}}`, `{{STAT_3_VALOR}}`, `{{STAT_3_LABEL}}`,
`{{STAT_4_VALOR}}`, `{{STAT_4_LABEL}}`.

Eixo 1: `{{EIXO_1_TEXTO}}`, `{{EIXO_1_FONTES}}`, `{{EIXO_1_GRAFICO_SVG}}`,
`{{EIXO_1_GRAFICO_TITULO}}`, `{{EIXO_1_GRAFICO_DESC}}`.

Eixo 2: `{{EIXO_2_INTRO}}`, `{{EIXO_2_LINHAS_TABELA}}`,
`{{EIXO_2_GRAFICO_SVG}}`, `{{EIXO_2_GRAFICO_TITULO}}`, `{{EIXO_2_GRAFICO_DESC}}`.

Eixo 3: `{{PRECO_MIN}}`, `{{PRECO_MAX}}`, `{{PRECO_FAIXA_COMUM}}`,
`{{PRECO_X_FORMATO}}`, `{{PRECO_OFERTAS}}`, `{{PRECO_SUGESTAO}}`,
`{{EIXO_3_GRAFICO_SVG}}`, `{{EIXO_3_GRAFICO_TITULO}}`, `{{EIXO_3_GRAFICO_DESC}}`.

Eixo 4: `{{EIXO_4_DEMOGRAFIA}}`, `{{EIXO_4_COMPORTAMENTO}}`,
`{{EIXO_4_SITUACOES}}`, `{{EIXO_4_CONSCIENCIA}}`, `{{EIXO_4_GRAFICO_SVG}}`,
`{{EIXO_4_GRAFICO_TITULO}}`, `{{EIXO_4_GRAFICO_DESC}}`.

Eixo 5: `{{EIXO_5_INTRO_RECLAME_AQUI}}`, `{{EIXO_5_LISTA_OBJECOES}}`,
`{{EIXO_5_GRAFICO_SVG}}`, `{{EIXO_5_GRAFICO_TITULO}}`, `{{EIXO_5_GRAFICO_DESC}}`.

Eixo 6: `{{EIXO_6_TERMOS}}`, `{{EIXO_6_VIRAIS}}`, `{{EIXO_6_GANCHOS}}`,
`{{EIXO_6_GRAFICO_SVG}}`, `{{EIXO_6_GRAFICO_TITULO}}`, `{{EIXO_6_GRAFICO_DESC}}`.

Eixo 7: `{{EIXO_7_CARDS_YOUTUBE}}`, `{{EIXO_7_PADRAO_THUMB}}`,
`{{EIXO_7_PADRAO_TITULO}}`, `{{EIXO_7_PADRAO_COMENTARIOS}}`,
`{{EIXO_7_LACUNAS}}`, `{{EIXO_7_GRAFICO_SVG}}`, `{{EIXO_7_GRAFICO_TITULO}}`,
`{{EIXO_7_GRAFICO_DESC}}`.

Eixo 8: `{{EIXO_8_ANUNCIOS_LONGOS}}`, `{{EIXO_8_VARIACOES}}`,
`{{EIXO_8_HEADLINES}}`, `{{EIXO_8_GANCHOS}}`, `{{EIXO_8_OFERTAS}}`,
`{{EIXO_8_CTAS}}`, `{{EIXO_8_GRAFICO_SVG}}`, `{{EIXO_8_GRAFICO_TITULO}}`,
`{{EIXO_8_GRAFICO_DESC}}`.

Eixo 9: `{{EIXO_9_REGRAS}}`, `{{EIXO_9_PALAVRAS}}`, `{{EIXO_9_POLEMICAS}}`,
`{{EIXO_9_GRAFICO_SVG}}`, `{{EIXO_9_GRAFICO_TITULO}}`, `{{EIXO_9_GRAFICO_DESC}}`.

Síntese: `{{OPORTUNIDADES_INTRO}}`, `{{OPORTUNIDADES_LISTA}}`,
`{{CUIDADOS_LISTA}}`, `{{CONFIANCA_JUSTIFICATIVA}}`.
