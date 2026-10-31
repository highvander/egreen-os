---
name: egreen-concepcao
description: >
  Concepção de produto em versão final e enxuta. Entrega Promessa, Mecanismo nomeado, Benefícios,
  Baldes Para Quem É, Identidade do Consumidor (com objeções), Urgências Ocultas, Escopo Mínimo
  Viável e Identidade do Produto (nome, Big Idea, inimigo, posicionamento). Substitui os termos da
  metodologia VTSD por uma linguagem pronta para uso externo (Quadro vira Promessa, Furadeira vira
  Mecanismo, Decorados viram Benefícios). Lê produto, nicho, formato e preço da memória do produto
  ativo (ou pergunta, se faltar). Não faz pesquisa de mercado. Não sugere preço. Aprovação
  obrigatória bloco a bloco. Salva o documento em {pasta-ativa}/egreen-concepcao/ e um resumo de
  argumentos em {pasta-ativa}/memoria/egreen-argumentos.md, lido por oferta, copy, anúncios e e-mails.
---

# Concepção de Produto Final

Esta skill executa a concepção completa de um produto digital em formato resumido e pronto para uso fora do projeto. Toda regra da metodologia continua valendo, mas os entregáveis recebem nomes mais diretos:

- **Promessa** (equivalente ao Quadro)
- **Mecanismo** (equivalente à Furadeira: o método com nome próprio)
- **Benefícios** (equivalente aos Decorados)
- **Baldes Para Quem É** (5 segmentos)
- **Identidade do Consumidor** (perfil completo + objeções com 7 quebras + objeções secundárias)
- **Urgências Ocultas** (razões reais e não óbvias para agir agora)
- **Escopo Mínimo Viável** (o que entra na v1 vendável agora, o que vira Esteira pra depois)
- **Identidade do Produto** (nome, Big Idea, inimigo, frase de posicionamento)

O **preço** é informado pelo aluno na pergunta inicial (já foi definido em outras skills) e vai direto para o documento final, sem nova sugestão.

## Regras Globais

### Idioma e estilo

- Português do Brasil com acentuação correta em 100% dos textos.
- Travessão (—) proibido. Substitua por vírgula, ponto, dois pontos ou parênteses.
- Ponto de exclamação proibido em copy. Use ponto final.
- Light Copy: argumentativa, lógica, sem promessas vagas, sem "mesmo que", sem "não é X, é Y", sem perguntas retóricas abrindo parágrafo.
- Toda promessa precisa de número, prazo ou situação específica.
- Sem lero-lero: palavras genéricas que soam bem mas não dizem nada ("jornada de autoconhecimento", "padrão interno", "caminhos terapêuticos") são proibidas. Troque por dado concreto ou cena real.

### Aprovação obrigatória bloco a bloco

Cada bloco do fluxo termina com:

```
1. Aprovar e seguir
2. Quero ajustar
```

Não avance sem o "1". Se o aluno escolher "2", pergunte exatamente o que ajustar e regere apenas aquele bloco.

### Postura de consultor

Você gera e sugere com base nos dados que o aluno passou na Etapa 1, nunca pergunta tudo. Faça apenas as perguntas que dependem do conhecimento exclusivo dele. Tudo que pode ser deduzido do contexto inicial é gerado por você e levado para aprovação.

### Anúncio de próximo passo

Antes de cada operação longa, avise em uma linha:

```
🔍 Próximo passo: {ação no infinitivo}. Tempo estimado: {X minutos}.
```

Ao concluir:

```
✅ Concluído: {entregável}.
```

### Proibições absolutas

- **Não fazer pesquisa de mercado.** Não usar WebSearch, WebFetch, navegação ou qualquer ferramenta de busca. A pesquisa foi feita por outra skill antes desta.
- **Não sugerir preço.** O preço foi definido em outra skill e chega pronto na Etapa 1.

---

## Passo 0. Gate e memória

Aplique REGRA 1 e REGRA 2 do `CLAUDE.md` e leia:

```
memoria/produto-ativo.md                       → pasta ativa
memoria/formatos.md                            → escopo típico de cada formato
{pasta-ativa}/memoria/egreen-produto.md        → produto, formato, preço
{pasta-ativa}/memoria/egreen-nicho.md          → nicho, público, dores
{pasta-ativa}/memoria/brand-voice.md           → (se existir) tom dos textos
{pasta-ativa}/egreen-pesquisa/                 → (se existir) concorrentes e paliativos já mapeados
```

Se os 4 dados da Etapa 1 (produto, nicho, formato, preço) já estiverem na memória, mostre-os em um resumo de 4 linhas e peça confirmação em vez de perguntar do zero. Se não houver produto ativo (uso avulso, fora do OS), siga normalmente pela Etapa 1.

---

## Fluxo Completo (9 etapas)

1. Pergunta inicial
2. Promessa
3. Mecanismo (Etapa 2B)
4. Benefícios
5. Baldes Para Quem É
6. Identidade do Consumidor
7. Urgências Ocultas (Etapa 5B)
8. Escopo Mínimo Viável
9. Identidade do Produto (Etapa 7)

### Etapa 1. Pergunta inicial sobre o produto

Se o Passo 0 já trouxe os 4 dados da memória, apenas confirme. Caso contrário, faça uma única pergunta aberta capturando os 4 dados que o aluno já tem definidos de etapas anteriores (produto, nicho, formato e preço):

```
Vamos começar a concepção. Me passa 4 informações que você já definiu:

1. Qual é o produto (o que é, o que o comprador recebe na prática)
2. Qual o nicho ou tema
3. Qual o formato (curso, mentoria, e-book, planilha, agente GPT, desafio, etc.)
4. Qual o preço

(ex: "Curso online para mães de bebês ensinarem o filho a dormir sozinho
em 14 dias. Nicho: maternidade e sono infantil. Formato: 12 aulas gravadas
+ planilha de sono + grupo de suporte. Preço: R$ 297.")
```

Aguarde a resposta. **Não avance até ter os 4 dados.** Se faltar algum, pergunte de novo apenas o que faltou em uma linha:

```
Recebi quase tudo. Faltou: {item faltante}. Me passa rapidinho?
```

Guarde os 4 dados em memória para usar em todos os blocos seguintes (Promessa, Benefícios, Baldes, Identidade do Consumidor). O preço informado aqui vai direto para o documento final, sem nova sugestão.

### Etapa 2. Promessa (5 opções)

> Esta é a peça mais importante. Aplique exatamente as regras de **Quadro** da metodologia, apenas trocando o nome para **Promessa**.

#### Definição

A Promessa é a transformação principal do produto. É o **resultado final** que a pessoa CONQUISTA ou SE TORNA após usar o produto. É a chegada, nunca o caminho.

**Teste rápido:** a pessoa pode dizer "isso aconteceu na minha vida" ao final do produto? Se sim, é Promessa. Se não, é processo, descarte.

#### Regras obrigatórias (aplique antes de apresentar)

- Até 10 palavras.
- Verbo no infinitivo (Falar, Fechar, Zerar, Conseguir, Vender, Sair, Ganhar).
- Um único resultado.
- Atrativa, clara, específica e tangível.
- **Sem palavras de caminho:** proibido "através", "com", "usando", "aplicando", "por meio de". A Promessa descreve o destino, não o meio.
- **Sem conjunção "e":** se aparecer "e", há dois resultados. Escolha o mais importante.
- **Sem imperativo:** não começar com "Descubra", "Aprenda", "Transforme". Use infinitivo.
- Verbos fracos como "Descobrir", "Aprender", "Entender" são aceitáveis mas inferiores. Prefira sempre verbos de resultado concreto (Faturar, Fechar, Zerar, Conseguir, Vender, Sair de, Receber).

#### Exemplos de Promessa válida

- Falar inglês em 90 dias
- Fechar R$10 mil por mês como social media
- Vender bolo caseiro todos os dias
- Zerar dívidas em até 90 dias sem renda extra
- Cobrar o que vale sem sentir que está exagerando
- Conseguir os primeiros 3 clientes freelancer em 30 dias
- Fazer o bebê dormir a noite toda em 14 dias

#### Exemplos do que NÃO é Promessa (processo, descarte)

- "Identificar a crença que te trava" → processo, não chegada
- "Descobrir por que você sabota seus resultados" → investigação, não resultado
- "Aprender como funciona X" → caminho, não transformação
- "Reconectar com sua essência através de práticas terapêuticas" → lero-lero
- "Sair do vermelho e ter mais qualidade de vida" → dois resultados (use "e" proibido)

#### Pergunta condicional para nicho abstrato

Antes de gerar as 5 opções, avalie se a resposta da Etapa 1 tem sinais de abstração: autoconfiança, autoconhecimento, mentalidade, espiritualidade, inteligência emocional, bem-estar, desenvolvimento pessoal, autoestima, propósito, equilíbrio, relacionamentos, cura, despertar, superação, ansiedade.

Se detectar um desses sinais, faça esta pergunta antes de gerar (sem comentar a detecção):

```
Qual área da vida isso impacta mais na prática?
(ex: profissional, financeira, relacionamentos, saúde, vida social)
```

Use a resposta para ancorar a Promessa em algo externo e mensurável. Exemplo: "autoconfiança" + "profissional" → "Falar com segurança em reuniões e ser reconhecido no trabalho".

Se o nicho já é objetivo e tangível (finanças, idiomas, emagrecimento, vendas), pule essa pergunta sem mencionar.

#### Apresentação das 5 opções

Gere 5 opções aplicando todas as regras acima. Teste cada uma internamente antes de mostrar:
- A pessoa pode dizer "isso aconteceu na minha vida"?
- Tem verbo no infinitivo no início?
- Não tem "e", "através", "com", "usando"?
- Tem prazo, número ou situação concreta?

Apresente assim:

```
Aqui estão 5 opções de Promessa para o seu produto:

1. {Opção 1}
2. {Opção 2}
3. {Opção 3}
4. {Opção 4}
5. {Opção 5}

Escolha o número da que mais conecta. Pode também digitar uma versão sua.

1. Aprovar e seguir
2. Quero ajustar
```

Salve a Promessa escolhida.

### Etapa 2B. Mecanismo (substitui Furadeira)

#### O que é

O Mecanismo é o **caminho** que leva à Promessa: o método, em fases, que o produto ensina ou executa. A Promessa é o quadro na parede; o Mecanismo é a furadeira. Ninguém compra a furadeira pela furadeira, mas é ela que torna a Promessa crível.

Um Mecanismo com **nome próprio** parece único, defensável e difícil de copiar. Nomear cria realidade.

#### Pergunta obrigatória (conhecimento exclusivo do aluno)

```
Como você leva a pessoa do zero até a Promessa?
Me conta as etapas na ordem, do jeito que você faria na prática.
(pode ser solto, eu organizo)
```

Se o aluno não tiver método definido, proponha um com base no produto e formato e deixe claro que é sugestão para ele validar.

#### Regras de geração

- 3 a 6 fases, em ordem, cada uma com: nome curto da fase (verbo de ação), o que a pessoa faz, resultado parcial ao fim da fase.
- O resultado parcial de cada fase é um degrau visível rumo à Promessa (a pessoa sente progresso).
- Fases concretas: ferramenta, ação, entregável. Sem lero-lero ("despertar", "ressignificar").
- 5 opções de nome para o Mecanismo, misturando estilos: descritivo ("Método Varanda Produtiva"), número + resultado ("Os 4 Passos da Colheita Contínua"), metáfora, sigla com sentido, nome do autor + método.
- Para cada nome, uma linha dizendo por que conecta com esse público.

#### Apresentação

```
Mecanismo em {N} fases:

Fase 1. {Nome}: {o que faz} → {resultado parcial}
Fase 2. {Nome}: {o que faz} → {resultado parcial}
...

Opções de nome para o método:
1. {Nome 1}: {por que funciona}
...
5. {Nome 5}: {por que funciona}

Escolha o número do nome (ou digite o seu) e diga se as fases estão certas.

1. Aprovar e seguir
2. Quero ajustar
```

Salve o Mecanismo aprovado (nome + fases). Ele é a base do Escopo Mínimo Viável (Etapa 6), do currículo (`egreen-curriculo`) e da oferta (`egreen-oferta`).

### Etapa 3. Benefícios (substitui Decorados)

> Mesma lógica dos Decorados da metodologia. Apenas o nome muda.

#### O que são

Benefícios são os 50 resultados diretos e indiretos que decorrem da Promessa. Não são features do produto. São consequências reais na vida do comprador depois que a transformação acontece.

#### Estrutura obrigatória

5 categorias com exatamente 10 itens em cada, totalizando 50 Benefícios.

1. **Financeiro** (10 itens). O que muda no dinheiro: faturamento, economia, novas fontes de receita, dívidas zeradas, custos cortados.
2. **Tempo** (10 itens). O que muda na agenda: tempo livre, fim de retrabalho, processos mais rápidos, ritual fixo, fim da procrastinação.
3. **Autoestima** (10 itens). O que muda por dentro: orgulho, confiança, fim da culpa, segurança em decisões, identidade nova.
4. **Reputação** (10 itens). O que os outros veem: reconhecimento, autoridade no nicho, indicações, fila de espera, status profissional.
5. **Crescimento** (10 itens). O que destrava daqui pra frente: novas habilidades adjacentes, network, repertório, próximos passos viabilizados.

#### Regras de geração

- Cada Benefício é uma frase curta, específica, em terceira pessoa ou imperativo de resultado.
- Não repita o mesmo Benefício em categorias diferentes só trocando palavras.
- Use o contexto do produto, nicho e formato (Etapa 1) para tornar os Benefícios concretos.
- Conecte cada Benefício à Promessa (se ela for "Falar inglês em 90 dias", o financeiro pode ser "Aceitar vaga remota com salário em dólar" e não "Ganhar dinheiro").
- Light Copy: sem exclamação, sem travessão, sem lero-lero.

Avise antes de gerar:

```
🔍 Próximo passo: gerar 50 Benefícios em 5 categorias. Tempo estimado: 2 a 3 minutos.
```

#### Apresentação

Mostre os 50 Benefícios organizados pelos 5 H3 e peça aprovação:

```
1. Aprovar e seguir
2. Quero ajustar uma categoria específica
```

Se escolher 2, pergunte qual categoria e regere apenas aquela.

### Etapa 4. Baldes Para Quem É (5 segmentos)

#### O que são

Os Baldes Para Quem É são 5 perfis distintos de potencial comprador. Cada balde é um recorte diferente do mesmo público, organizado por:

- Profissão ou ocupação
- Momento de vida
- Dor dominante
- Nível de consciência
- Objetivo imediato

**Regra crítica:** os 5 baldes precisam ser RECORTES DISTINTOS. Não são variações do mesmo perfil mudando só o nome. Cada balde fala com uma persona diferente que tem motivações específicas.

#### Estrutura obrigatória por balde

```
### Balde {N}: {Nome descritivo do segmento}

**Descrição:** {1 parágrafo descrevendo quem é essa pessoa, situação de vida,
contexto, o que sente em relação ao problema que a Promessa resolve.}

**Como se comunicar:**
- {orientação de tom ou ângulo}
- {orientação de tom ou ângulo}
- {orientação de tom ou ângulo}
```

#### Regras de geração

- Use o produto, nicho, formato e a Promessa como base.
- Cada balde precisa ter uma dor dominante diferente.
- O nome do balde é descritivo, não um nome próprio (ex: "Mãe de primeira viagem cansada", "Empreendedora que já tentou tudo", "Recém-formada sem clientes").
- Não invente baldes ricos demais ou pobres demais que o produto não atende.

Avise antes de gerar:

```
🔍 Próximo passo: gerar 5 Baldes Para Quem É com descrição e tom de comunicação.
Tempo estimado: 2 a 3 minutos.
```

#### Aprovação

```
1. Aprovar e seguir
2. Quero ajustar um balde específico
```

### Etapa 5. Identidade do Consumidor (documento completo)

#### O que vai dentro

Documento único com 7 blocos:

1. Para Quem É (frase de posicionamento + exclusões)
2. Perfil Demográfico (idade, gênero, profissão, renda, estado civil, localização, nível de consciência, canais de informação)
3. Paliativos (concorrentes que resolvem parcialmente)
4. Objeções de Compra (5 objeções com 7 argumentos de quebra cada, 2 parágrafos por argumento)
5. Sonho (frase em primeira pessoa, cena do futuro)
6. Frases que Essa Pessoa Diria (6 a 10 frases reais)
7. Como se Comunicar (tom, palavras que conectam, palavras que afastam)

#### Estrutura completa (siga o template à risca)

```markdown
# Identidade do Consumidor: {Nome fictício brasileiro comum}

## Para Quem É

"Este produto é para {perfil específico}, que {problema ou situação atual},
e quer {transformação desejada baseada na Promessa}."

Não é para:
- {exclusão 1}
- {exclusão 2}
- {exclusão 3}
- {exclusão 4}

## Perfil Demográfico

- **Idade:** {faixa baseada no nicho e formato}
- **Gênero:** {predominante ou ambos}
- **Profissão:** {ocupação típica}
- **Renda:** {faixa coerente com o preço informado na Etapa 1}
- **Estado civil:** {predominante}
- **Localização:** {região ou Brasil todo}
- **Nível de consciência:** {inconsciente do problema / consciente do problema /
  consciente da solução / consciente do produto / totalmente consciente}
- **Onde busca informação:** {canais concretos com tipo de conteúdo}

## Paliativos

- {Nome do concorrente ou solução} → {o que oferece e por que não entrega
  o resultado completo da Promessa}
- {mínimo 4, máximo 8}

## Objeções de Compra (Framework dos 7 Argumentos)

### Objeção 1: {texto da objeção real do nicho}

**1. Argumento Incontestável**

{Parágrafo 1: dado concreto, estatística ou fato irrefutável com fonte.}

{Parágrafo 2: aplicação do dado à realidade desse consumidor.}

**2. Argumento Lógico (causa e efeito)**

{Parágrafo 1: raciocínio com números e relação causa-consequência.}

{Parágrafo 2: virada lógica que reposiciona a pergunta.}

**3. Argumento por Analogia**

{Parágrafo 1: comparação visual e cotidiana. NUNCA cite celebridades.
Use situações reais que esse público vive.}

{Parágrafo 2: extensão da analogia conectando ao contexto de compra.}

**4. Argumento por Exemplificação**

{Parágrafo 1: caso real com nome fictício brasileiro, situação inicial,
decisão tomada.}

{Parágrafo 2: desfecho concreto com número ou prazo e moral para o leitor.}

**5. Argumento de Valor**

{Parágrafo 1: comparação do investimento com retorno tangível.
Use o preço real do produto informado na Etapa 1.}

{Parágrafo 2: retorno intangível e diferencial percebido ao longo do tempo.}

**6. Argumento de Consequência**

{Parágrafo 1: cenário de adiar a decisão. O que acontece em 6 meses,
1 ano sem resolver.}

{Parágrafo 2: cenário de decidir agora. O que muda no mesmo prazo.}

**7. Argumento de Contradição**

{Parágrafo 1: onde a objeção contradiz outras escolhas ou prioridades
da própria pessoa.}

{Parágrafo 2: conclusão que reposiciona a prioridade sem atacar
o consumidor.}

### Objeção 2: {texto}
{mesma estrutura}

### Objeção 3: {texto}
{mesma estrutura}

### Objeção 4: {texto}
{mesma estrutura}

### Objeção 5: {texto}
{mesma estrutura}

## Objeções Secundárias

Objeções menores que não merecem os 7 argumentos, mas não podem ficar sem resposta
(praticidade, logística, medo pontual). De 3 a 6 itens:

- "{objeção}" → {resposta em 1 ou 2 frases, concreta}

## Sonho

"{Frase longa em primeira pessoa, entre aspas, descrevendo a cena do futuro
desejado depois da Promessa cumprida. Específica, sensorial, com nome de
pessoa, lugar ou situação real. Não genérica.}"

## Frases que Essa Pessoa Diria

1. "{frase de dor, situação concreta}"
2. "{frase de desejo, o que sonha alcançar}"
3. "{frase de objeção, dúvida real antes de comprar}"
4. "{frase de frustração com tentativas anteriores}"
5. "{frase que demonstra o nível de consciência}"
6. "{frase que apareceria em comentário do YouTube ou DM do Instagram}"
7. "{frase opcional}"
8. "{frase opcional}"

## Como se Comunicar

- **Tom de voz recomendado:** {específico, ex: direto e prático sem ser
  frio, ou acolhedor sem ser condescendente}
- **Palavras que conectam:** {8 a 12 palavras ou expressões que esse
  público usa e responde bem}
- **Palavras que afastam:** {6 a 10 palavras ou abordagens que geram
  resistência}
```

#### Regras de geração

- Use TUDO o que foi coletado até aqui: produto, nicho, formato, preço, Promessa, Benefícios, Baldes.
- Nome fictício brasileiro comum (Mariana, João, Carolina, Pedro, Aline, Lucas, etc.).
- Cada objeção precisa ser real (deduzida do perfil, preço e nicho).
- Cada argumento precisa ter 2 parágrafos completos, nunca 1 frase.
- Total: 5 objeções × 7 argumentos × 2 parágrafos = 70 parágrafos só no bloco de objeções.
- Light Copy em tudo: sem travessão, sem exclamação, sem pergunta retórica abrindo parágrafo, sem lero-lero.

Avise:

```
🔍 Próximo passo: gerar Identidade do Consumidor completa (perfil, paliativos,
5 objeções com 7 argumentos cada, sonho, frases, comunicação).
Tempo estimado: 3 a 5 minutos.
```

#### Aprovação

```
1. Aprovar e seguir para o documento final
2. Quero ajustar uma seção específica
```

Se escolher 2, pergunte qual seção (perfil, paliativos, alguma objeção, sonho, frases, comunicação) e regere apenas aquela.

### Etapa 5B. Urgências Ocultas

#### O que são

Razões **reais e não óbvias** para a pessoa resolver o problema agora, e não "um dia". A urgência óbvia ("quanto antes melhor") não move ninguém. A oculta revela um custo que a pessoa está pagando sem perceber.

É a resposta ética à pergunta "por que agora?": ancorada no custo real da inação, nunca em escassez falsa, contador fictício ou "últimas vagas" inventadas.

#### Tipos de urgência oculta (use como lente, não precisa cobrir todos)

1. **Custo que acumula:** dinheiro, tempo ou saúde que se perde todo mês enquanto nada muda.
2. **Efeito composto:** quanto mais tarde começa, menor o resultado acumulado (hábitos, carreira, investimento, idade).
3. **Janela que fecha:** sazonalidade, fase da vida, momento de mercado, idade do filho, prazo externo real.
4. **Problema que piora sozinho:** o quadro se agrava ou fica mais caro de resolver com o tempo.
5. **Custo de oportunidade:** o que a pessoa deixa de ganhar ou viver enquanto adia.
6. **Custo social ou emocional:** desgaste em relações, autoimagem, exemplo para os filhos, reputação.
7. **Gatilho de evento:** um acontecimento próximo e real que torna o problema mais visível (início de ano, volta às aulas, verão, data comemorativa, mudança de lei).

#### Regras de geração

- Gere **7 Urgências Ocultas**, cada uma com:
  - **Nome curto** da urgência
  - **A urgência** em 1 frase, específica para esse consumidor
  - **Por que é oculta:** o que a pessoa não está percebendo hoje
  - **Custo de esperar:** número, prazo ou cena concreta (ex: "6 meses adiando = R$ 480 a mais em feira")
  - **Onde usar:** headline, anúncio, e-mail, stories, VSL ou fechamento da oferta
- Use preço, Benefícios Financeiro e Tempo, Sonho e Objeções como base para os números.
- Proibido: escassez falsa, ameaça, catastrofismo, culpa pesada. Light Copy.
- Se uma urgência depender de dado que você não tem (estatística do nicho), marque `{confirmar dado}` em vez de inventar número.

Avise antes de gerar:

```
🔍 Próximo passo: gerar 7 Urgências Ocultas com custo de esperar. Tempo estimado: 1 a 2 minutos.
```

#### Aprovação

```
1. Aprovar e seguir
2. Quero ajustar uma urgência específica
```

### Etapa 6. Escopo Mínimo Viável

> Independente do nicho, formato ou preço, todo produto passa por aqui antes do currículo (`egreen-curriculo`), da experiência (`egreen-experiencia`) ou do ebook (`egreen-ebook`) serem desenhados. É o freio contra produzir demais antes de validar.

#### O que é

O menor conjunto de entregáveis que já cumpre a Promessa inteira, vendável e usável por alguém desde já, sem esperar o resto ser produzido. Não é uma versão incompleta do produto. É o produto completo, na forma mais direta de entregar.

Tudo que não é indispensável para a Promessa acontecer vira **Esteira**: bônus, próximo produto, upsell, aprofundamento futuro.

**Teste obrigatório por item:** "se eu tirar isso, a Promessa ainda acontece?" Se a resposta é sim, o item é Esteira, não Essencial.

#### Regras de geração

- Liste de 3 a 6 **Entregáveis Essenciais** (o que precisa existir: módulo, aula, ritual, ferramenta, template, sessão).
- Liste de 2 a 5 itens de **Esteira** (o que fica para depois da venda validar o produto).
- Cada Entregável Essencial precisa sustentar pelo menos 3 dos 50 Benefícios (Etapa 3). Se um Entregável não sustenta nenhum Benefício, é decoração, corte ou mova para Esteira.
- Toda fase do Mecanismo (Etapa 2B) precisa estar coberta por pelo menos um Entregável Essencial. Fase sem entregável = Promessa quebrada no meio.
- Use o formato definido na Etapa 1 (curso, desafio, ebook, mentoria, etc.) para nomear os Entregáveis em termos concretos daquele formato, não genéricos.

Avise antes de gerar:

```
🔍 Próximo passo: gerar o Escopo Mínimo Viável (Essenciais + Esteira). Tempo estimado: 1 a 2 minutos.
```

#### Apresentação

```
Escopo Mínimo Viável:

Essenciais (entram na v1, sem eles a Promessa não acontece):
1. {entregável essencial}
2. {entregável essencial}
...

Esteira (fica para depois, não impede a Promessa):
1. {item de esteira}
2. {item de esteira}
...

1. Aprovar e seguir para o documento final
2. Quero ajustar
```

Se escolher 2, pergunte o que ajustar (mover item entre Essencial/Esteira, adicionar, remover) e regere apenas o necessário.

### Etapa 7. Identidade do Produto

#### O que é

A síntese de tudo: como o produto se chama, qual ideia nova ele carrega e contra o que ele luta. É o que torna o produto reconhecível e diferente dos Paliativos (Etapa 5).

#### Regras de geração

1. **Nome do produto:** 5 opções. Curtas (até 4 palavras), fáceis de falar em voz alta, ligadas à Promessa ou ao Mecanismo. Se o aluno já tem nome definido, mostre-o como opção 1 e gere 4 alternativas.
2. **Big Idea:** 1 frase com a ideia central nova que muda a forma como o público vê o problema. Ela explica por que as tentativas anteriores falharam e por que o Mecanismo funciona. Ex: "Horta de apartamento não morre por falta de cuidado, morre por falta de luz certa."
3. **Inimigo:** o que o produto combate. Um comportamento, crença, prática do mercado ou paliativo (nunca uma pessoa ou marca nomeada). 1 frase + por que ele prejudica o consumidor.
4. **Frase de posicionamento:** "O único {categoria} que {diferencial ligado ao Mecanismo} para {público do Para Quem É}."
5. **Subtítulo do produto:** Promessa + Mecanismo em até 15 palavras (ex: "Colha seus temperos em 60 dias com o Método Varanda Produtiva").

Light Copy em tudo. Sem superlativos vazios ("revolucionário", "definitivo").

Avise antes de gerar:

```
🔍 Próximo passo: gerar a Identidade do Produto (nome, Big Idea, inimigo, posicionamento).
Tempo estimado: 1 minuto.
```

#### Aprovação

```
1. Aprovar e seguir para o documento final
2. Quero ajustar
```

---

## Encerramento (geração obrigatória do documento final)

Depois que a Identidade do Produto (Etapa 7) for aprovada, **gere automaticamente** o documento final consolidado. Não pergunte se o aluno quer. Não dê opção. O documento é o entregável principal da skill e precisa estar pronto para download no fim de toda execução.

### Passo 1. Avisar que vai gerar

```
🔍 Próximo passo: gerar o documento final da concepção em um único arquivo .md
para download. Tempo estimado: cerca de 30 segundos.
```

### Passo 2. Montar o arquivo

Nome do arquivo: `{YYYY-MM-DD}-concepcao-{slug-do-produto}.md` onde `{slug-do-produto}` é o nome do produto em ASCII minúsculo com hífens (ex: `2026-10-31-concepcao-curso-sono-bebe.md`).

Local de salvamento (por ordem de preferência, use o primeiro que existir e for gravável):

1. `{pasta-ativa}/egreen-concepcao/` (padrão no EGreen OS, REGRA 3 do `CLAUDE.md`)
2. Pasta de Downloads do usuário (só em uso avulso, sem produto ativo)
3. Diretório de trabalho atual

Estrutura obrigatória do arquivo:

```markdown
# Concepção de Produto: {Nome do Produto}

**Data:** {data de hoje em formato DD/MM/AAAA}
**Nicho:** {nicho informado na Etapa 1}
**Formato:** {formato informado na Etapa 1}
**Preço:** R$ {preço informado na Etapa 1}

---

## 1. Promessa

{promessa aprovada na Etapa 2}

---

## 1B. Mecanismo: {nome do método}

1. **{Fase 1}:** {o que faz} → {resultado parcial}
2. **{Fase 2}:** {o que faz} → {resultado parcial}
... (3 a 6 fases)

---

## 2. Benefícios (50)

### Financeiro
1. {benefício 1}
2. {benefício 2}
... (10 itens)

### Tempo
1. {benefício 1}
... (10 itens)

### Autoestima
1. {benefício 1}
... (10 itens)

### Reputação
1. {benefício 1}
... (10 itens)

### Crescimento
1. {benefício 1}
... (10 itens)

---

## 3. Baldes Para Quem É

### Balde 1: {Nome}
**Descrição:** {parágrafo completo}
**Como se comunicar:**
- {orientação}
- {orientação}
- {orientação}

### Balde 2: {Nome}
{mesma estrutura}

### Balde 3: {Nome}
{mesma estrutura}

### Balde 4: {Nome}
{mesma estrutura}

### Balde 5: {Nome}
{mesma estrutura}

---

## 4. Identidade do Consumidor

{copiar o documento completo da Etapa 5 na íntegra: Para Quem É, Perfil Demográfico,
Paliativos, 5 Objeções com 7 argumentos cada, Objeções Secundárias, Sonho, Frases que diria,
Como se comunicar}

---

## 4B. Urgências Ocultas

### {Nome da urgência 1}
- **Urgência:** {frase}
- **Por que é oculta:** {frase}
- **Custo de esperar:** {número, prazo ou cena}
- **Onde usar:** {canais}

... (7 urgências)

---

## 5. Escopo Mínimo Viável

### Essenciais (v1, sem eles a Promessa não acontece)
1. {entregável essencial} (cobre a Fase {N} do Mecanismo)
... (3 a 6 itens)

### Esteira (para depois da validação)
1. {item de esteira}
... (2 a 5 itens)

---

## 6. Identidade do Produto

- **Nome:** {nome aprovado}
- **Subtítulo:** {Promessa + Mecanismo}
- **Big Idea:** {frase}
- **Inimigo:** {frase + por que prejudica}
- **Posicionamento:** {O único X que Y para Z}
```

### Passo 2B. Salvar o resumo de argumentos na memória

Além do documento completo, salve (ou sobrescreva) `{pasta-ativa}/memoria/egreen-argumentos.md`. É a versão curta que as outras skills leem pela REGRA 2 (oferta, copy, landing, VSL, mandala, e-mails, stories):

```markdown
---
status: aprovado
fonte: {pasta-ativa}/egreen-concepcao/{arquivo do documento completo}
atualizado: {YYYY-MM-DD}
---

# Argumentos do Produto: {Nome}

## Promessa
{promessa}

## Mecanismo: {nome}
1. {Fase 1} → {resultado parcial}
...

## Identidade do Produto
- Subtítulo: {…}
- Big Idea: {…}
- Inimigo: {…}
- Posicionamento: {…}

## Objeções
| Objeção | Argumento mais forte (1 a 2 frases) |
|---|---|
| {objeção principal 1} | {síntese do melhor dos 7 argumentos} |
... (5 principais + secundárias)

## Urgências Ocultas
- **{nome}:** {urgência} · custo de esperar: {…}
... (7)

## Sonho
"{frase do sonho}"
```

Se não houver produto ativo (uso avulso), pule este passo.

### Passo 3. Confirmar e entregar o caminho

Depois de salvar, mostre EXATAMENTE este bloco (substituindo os valores reais):

```
✅ Salvo em: {pasta-ativa}/egreen-concepcao/{YYYY-MM-DD}-concepcao-{slug-do-produto}.md
✅ Memória atualizada: {pasta-ativa}/memoria/egreen-argumentos.md

Resumo do pacote entregue dentro do arquivo:

📌 PRODUTO: {nome aprovado}, {subtítulo}
📌 PROMESSA: {promessa aprovada}
📌 MECANISMO: {nome do método} em {N} fases
📌 BIG IDEA: {frase}
📌 BENEFÍCIOS: 50 itens em 5 categorias
📌 BALDES PARA QUEM É: 5 segmentos distintos
📌 IDENTIDADE DO CONSUMIDOR: {nome fictício} com 5 objeções, 35 argumentos de quebra e {N} objeções secundárias
📌 URGÊNCIAS OCULTAS: 7
📌 ESCOPO MÍNIMO VIÁVEL: {N} entregáveis essenciais na v1, {N} itens na esteira
📌 PREÇO: R$ {valor informado na Etapa 1}

Próximo passo: /egreen-curriculo ou /egreen-experiencia (conteúdo de entrega), depois /egreen-oferta
```

### Regras críticas do encerramento

- **Nunca pular esta etapa.** O fluxo só termina quando o arquivo foi gerado E o caminho foi mostrado.
- **Nunca perguntar se quer gerar.** A geração é obrigatória.
- **Sempre mostrar o caminho** onde o arquivo foi salvo.
- **Se a pasta do produto ativo não existir**, caia no próximo local da lista e avise o aluno onde salvou.
- **Se houver erro ao salvar**, mostre o conteúdo completo do documento no chat para o aluno copiar manualmente, e diga: "Não consegui salvar o arquivo. Copie o conteúdo acima e cole em um arquivo .md no seu computador."

---

## Checklist de Verificação Final

Antes de declarar o fluxo encerrado, verifique:

- [ ] A Promessa cumpre todas as regras (até 10 palavras, infinitivo, sem "e", sem palavras de caminho, sem imperativo, resultado concreto)
- [ ] O Mecanismo tem nome próprio e 3 a 6 fases, cada uma com resultado parcial
- [ ] Toda fase do Mecanismo é coberta por pelo menos um Entregável Essencial
- [ ] As 7 Urgências Ocultas têm custo de esperar concreto e nenhuma usa escassez falsa
- [ ] A Identidade do Produto tem nome, subtítulo, Big Idea, inimigo e posicionamento
- [ ] `{pasta-ativa}/memoria/egreen-argumentos.md` foi salvo (quando há produto ativo)
- [ ] Os 50 Benefícios estão divididos em 5 categorias com exatamente 10 cada
- [ ] Os 5 Baldes são recortes distintos (não variações do mesmo perfil)
- [ ] A Identidade do Consumidor tem 5 objeções com 7 argumentos de 2 parágrafos cada
- [ ] Todo Entregável Essencial do Escopo Mínimo Viável sustenta pelo menos 3 dos 50 Benefícios
- [ ] Nenhum Entregável Essencial passou no teste "se eu tirar isso, a Promessa ainda acontece?" com resposta sim
- [ ] Nenhum texto tem travessão, exclamação, lero-lero ou pergunta retórica
- [ ] O preço informado na Etapa 1 aparece no cabeçalho do documento final e foi usado como referência no Argumento de Valor das objeções
- [ ] Toda a entrega está em pt_BR com acentuação correta
- [ ] O arquivo .md foi salvo em `{pasta-ativa}/egreen-concepcao/` e o caminho foi mostrado ao aluno

Se algum item falhar, corrija antes de entregar.
