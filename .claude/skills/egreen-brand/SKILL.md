---
name: egreen-brand
description: >
  Constrói a voz de marca do infoproduto via entrevista de 11 perguntas (uma por vez).
  Gera 6 blocos aprovados sequencialmente: 4 dimensões de voz com score, arquétipo de marca,
  vocabulário autorizado/proibido, guia do/don't com exemplos, 6 amostras de copy prontas e
  Identidade do Comunicador (história de origem, crenças, inimigo, provas de autoridade e release
  do autor em 3 tamanhos).
  Salva em {pasta-ativa}/memoria/brand-voice.md. Lido automaticamente por egreen-copy,
  egreen-mandala, egreen-carrossel, egreen-editorial e egreen-emails antes de gerar texto.
  Execute após /egreen-design e antes de /egreen-copy.
---

# /egreen-brand — Voz de Marca do Infoproduto

Skill que constrói a voz de marca completa via entrevista guiada e salva `{pasta-ativa}/memoria/brand-voice.md`. Esse arquivo é lido automaticamente por todas as skills de conteúdo antes de gerar texto.

**Não analisa URLs externas. Não compara concorrentes. Não cobre identidade visual** (paleta, fontes, componentes — responsabilidade do `/egreen-design`).

---

## O que esta skill faz

1. Verifica gate de memória do OS.
2. Realiza entrevista de 11 perguntas (uma por vez), usando dados da memória existente para pré-preencher sugestões.
3. Gera 6 blocos com aprovação obrigatória um a um.
4. Salva `{pasta-ativa}/memoria/brand-voice.md`.

---

## Passo 0 — Gate de memória (REGRA 1)

Leia `memoria/produto-ativo.md` para obter `{pasta-ativa}`.

Verifique:
- `{pasta-ativa}/memoria/egreen-nicho.md`
- `{pasta-ativa}/memoria/egreen-produto.md`

Se ausentes ou com `status: vazio`: **PARE** e instrua:

> **PARE.** O OS não está configurado.
> Execute `/egreen-setup` para realizar a entrevista inicial antes de usar esta skill.

Leia todos os arquivos existentes em `{pasta-ativa}/memoria/` — use os dados para pré-preencher sugestões durante a entrevista.

---

## Passo 1 — Verificar brand-voice existente

Se `{pasta-ativa}/memoria/brand-voice.md` já existir, pergunte:

```
Voz de marca já existe para este produto.

1. Atualizar (entrevista focada nas mudanças)
2. Recriar do zero
```

Aguarde resposta antes de continuar.

Se "1" (Atualizar): releia `{pasta-ativa}/memoria/brand-voice.md` para extrair os valores atuais. Para cada uma das 11 perguntas do Passo 2, exiba o valor atual como sugestão pré-preenchida e pergunte "O que mudou? (Enter para manter)". Pule perguntas cujo valor o usuário confirmar sem alteração. Ao final, regere apenas os blocos que tiverem respostas alteradas.

Se "2" (Recriar): siga o Passo 2 normalmente, sem carregar valores anteriores.

---

## Passo 2 — Entrevista (11 perguntas, uma por vez)

Faça **uma pergunta por vez**. Aguarde a resposta antes de passar para a próxima. Se o usuário responder "não sei" ou pular, registre como indefinido e continue.

Se a informação já estiver na memória, pré-preencha uma sugestão:
> "Da memória do produto, tenho [X]. Quer usar isso ou prefere algo diferente?"

### Pergunta 1 — Nome da marca

> "Qual o **nome da marca**? Pode ser o nome do produto, o seu nome ou um nome criado. (ex: 'Raízes Vivas', 'Hugo Genealogista', 'Método Árvore')"

### Pergunta 2 — Personalidade em 3 palavras

> "Escolha **3 palavras** que descrevem a personalidade da marca. Exemplos: direto · confiável · humano · leve · rigoroso · íntimo · ousado · acolhedor · especialista · curioso."

### Pergunta 3 — Tom com o cliente

> "Como você trata o cliente nos seus textos? Escolha o mais próximo:
> 1. Como aluno (você ensina, ele aprende)
> 2. Como amigo (conversa próxima, informal)
> 3. Como profissional (respeito mútuo, linguagem técnica moderada)
> 4. Como aprendiz (você é guia, ele tem potencial inexplorado)"

Use `egreen-nicho.md` para sugerir a opção mais coerente com o público identificado.

### Pergunta 4 — O que a marca nunca diz

> "O que a marca **nunca** diria? Exemplos: 'nunca usa gírias', 'nunca faz promessas sem evidência', 'nunca usa linguagem técnica sem explicar', 'nunca soa desesperado para vender'."

### Pergunta 5 — Referência de tom

> "Existe alguma marca **fora do seu nicho** cuja forma de se comunicar você admira? (ex: 'Nubank — direto e sem juridiquês', 'Nerdologia — didático e apaixonado', 'Não tenho referência')"

### Pergunta 6 — Vocabulário proibido

> "Quais palavras ou expressões **irritam você** quando vê em textos do seu nicho ou soam completamente erradas para sua marca? (ex: 'missão de vida', 'jornada', 'despertar', 'guru', 'exclusivo')"

### Pergunta 7 — Sensação-alvo

> "Que **sensação** o cliente deve ter ao ler qualquer texto da marca? Uma frase. (ex: 'Que tem alguém competente do lado dele', 'Que descobriu algo que todo mundo deveria saber', 'Que esse produto foi feito especificamente pra ele')"

### Pergunta 8 — Texto de referência

> "Tem algum texto **já escrito** que representa bem como você quer soar — um post, email, legenda, áudio transcrito? Cole aqui ou diga 'não tenho'."

Se colado: analise vocabulário, ritmo e tom. Use como âncora nos blocos gerados.

As perguntas 9 a 11 alimentam a Identidade do Comunicador (Bloco F). Se a marca não tem um rosto (empresa sem expert), pule-as e o Bloco F.

### Pergunta 9 — História de origem

> "Como você chegou até aqui? Me conta o antes (onde você estava, o que te incomodava), o momento da virada e o depois. Pode ser solto."

### Pergunta 10 — Provas de autoridade

> "Quais conquistas concretas você tem nesse tema? Números, anos de prática, alunos/clientes atendidos, resultados seus ou de clientes, formações, aparições. Só o que for verdade e você puder sustentar."

### Pergunta 11 — Crença e inimigo

> "Em que você discorda do que a maioria do seu mercado ensina ou faz? O que você combate?"

---

## Passo 3 — Resumo para aprovação

Antes de gerar qualquer bloco, exiba:

```
Resumo do que vou gerar:
- Nome da marca: [X]
- Personalidade: [3 palavras]
- Tom com o cliente: [tipo escolhido]
- Proibições: [lista]
- Referência de tom: [marca ou "nenhuma"]
- Vocabulário proibido: [lista]
- Sensação-alvo: [frase]
- Texto de referência: [analisado / não tenho]
- Origem / autoridade / crença: [resumo ou "sem rosto"]

1. Tudo certo, pode gerar
2. Quero ajustar algo
```

Aguarde "1". Se "2": pergunte o que ajustar, atualize o resumo, exiba novamente.

---

## Passo 4 — Geração bloco a bloco

Cada bloco termina com:

```
1. Aprovar e seguir
2. Quero ajustar
```

Não avance sem "1". Se "2": pergunte exatamente o que ajustar e regenere só aquele bloco.

Antes de cada bloco:
```
🔍 Próximo passo: gerar [nome do bloco]. Tempo estimado: 1 minuto.
```

### Bloco A — Dimensões de voz

4 espectros com score 1-10 derivado das respostas da entrevista. Inclua 1 linha de evidência por score (citando resposta da entrevista).

Representação visual obrigatória:

```
Formal                                    Casual
|----[X]----------------------------------|
Evidência: [frase da entrevista]

Sério                                     Leve
|--------[X]------------------------------|
Evidência: [frase da entrevista]

Técnico                                   Simples
|------------------[X]--------------------|
Evidência: [frase da entrevista]

Reservado                                 Ousado
|------------[X]--------------------------|
Evidência: [frase da entrevista]
```

### Bloco B — Arquétipo de marca

Identifique 1 primário e 1 secundário entre os 5:

| Arquétipo | Características | Voz |
|---|---|---|
| **Autoridade** | Especialista, confiável, baseado em dados | Educacional, preciso, confiante sem arrogância |
| **Inovador** | Visionário, disruptivo, à frente do nicho | Empolgante, focado no futuro |
| **Amigo** | Acolhedor, próximo, empático | Conversacional, encorajador, inclusivo |
| **Rebelde** | Ousado, contra o status quo, opiniático | Direto, provocador, memorável |
| **Guia** | Sábio, metódico, paciente | Claro, instrucional, passo a passo |

Entregue:
- **Primário:** [arquétipo] — justificativa em 2 linhas conectando às respostas da entrevista
- **Secundário:** [arquétipo] — idem (ou "nenhum" se a marca é arquetipicamente pura)

### Bloco C — Vocabulário

**Palavras autorizadas** (derivadas do nicho, personalidade e referências):
- Verbos de ação (5-8 palavras)
- Adjetivos (5-8 palavras)
- Palavras-valor (5-8 palavras)

**Palavras proibidas** (da entrevista + inferidas do arquétipo):
| Palavra/expressão | Por quê evitar |
|---|---|
| [palavra] | [motivo específico, não genérico] |

**Frases-assinatura** — padrões linguísticos recorrentes da marca (ex: "começa frases com verbo no imperativo", "usa dado antes de afirmação", "parágrafo curto, máx 3 linhas").

### Bloco D — Guia de escrita

**Nossa voz É / Nossa voz NÃO É** (4-5 pares):

| Nossa voz É | Nossa voz NÃO É |
|---|---|
| [ex: Confiante] | [ex: Arrogante] |

**Do's** (6-8 regras com exemplo concreto em português):
- **DO:** [regra específica] → `"[exemplo de frase no tom certo]"`

**Don'ts** (6-8 anti-padrões com exemplo):
- **DON'T:** [regra específica] → Errado: `"[exemplo fora do tom]"`

### Bloco E — 6 amostras de copy

Todas escritas usando vocabulário autorizado, evitando proibidos, seguindo arquétipo e dimensões.

1. **Headline de página de vendas** — até 10 palavras, afirmação direta, sem nome do produto
2. **Parágrafo de abertura do produto** — 3-4 linhas, apresenta problema antes de mencionar o produto
3. **Post Instagram** — legenda completa, sem hashtags, gancho na primeira linha
4. **Assunto de email** — até 8 palavras, curiosidade ou especificidade, sem clickbait
5. **CTA** — texto do botão (3-5 palavras) + frase de apoio abaixo (até 10 palavras)
6. **Mensagem de boas-vindas ao comprador** — 2-3 linhas, tom pós-compra, sem promessa de entrega técnica

### Bloco F — Identidade do Comunicador e Release

Pule se a marca não tem rosto (perguntas 9 a 11 puladas).

1. **História de origem** (5 a 7 linhas): antes → virada → depois, com cena concreta. Sem drama inventado.
2. **3 crenças** que a marca defende (1 frase cada, específicas, discutíveis).
3. **Inimigo:** o comportamento, prática ou crença do mercado que o comunicador combate (nunca pessoa ou marca nomeada).
4. **Provas de autoridade:** lista só com o que foi informado na Pergunta 10. Nada inventado ou arredondado para cima.
5. **Release do autor em 3 tamanhos:**
   - **Curto** (bio de Instagram, até 150 caracteres)
   - **Médio** (3 a 4 linhas, para página de captura, evento, convite de live)
   - **Longo** (2 a 3 parágrafos, para o bloco de Autoridade da página de vendas, imprensa e podcast), em terceira pessoa, com a conquista mais forte na primeira frase

Se existir `{pasta-ativa}/memoria/egreen-argumentos.md`, alinhe o inimigo e as crenças com o Inimigo e a Big Idea do produto.

---

## Passo 5 — Salvar e confirmar (REGRA 3)

Após aprovação do Bloco F (ou do Bloco E, se a marca não tem rosto), salvar automaticamente:

**Caminho:** `{pasta-ativa}/memoria/brand-voice.md`

**Conteúdo do arquivo:**

```markdown
---
status: ativo
produto: {nome-da-marca}
atualizado_em: {YYYY-MM-DD}
---

# Voz de Marca — {nome}

## Dimensões de Voz
[barras visuais com score e evidência]

## Arquétipo
**Primário:** {arquétipo} — {justificativa}
**Secundário:** {arquétipo} — {justificativa}

## Vocabulário

### Palavras autorizadas
**Verbos:** ...
**Adjetivos:** ...
**Palavras-valor:** ...

### Palavras proibidas
| Palavra/expressão | Por quê evitar |
|---|---|

### Frases-assinatura
- ...

## Guia de Escrita

### Nossa voz É / Nossa voz NÃO É
| Nossa voz É | Nossa voz NÃO É |
|---|---|

### Do's
- **DO:** [regra] → `"[exemplo]"`

### Don'ts
- **DON'T:** [regra específica] → Errado: `"[exemplo fora do tom]"`

## Amostras de Copy
**Headline:** ...
**Abertura do produto:** ...
**Post Instagram:** ...
**Assunto de email:** ...
**CTA:** [botão] — [frase de apoio]
**Boas-vindas:** ...

## Identidade do Comunicador
**História de origem:** ...
**Crenças:** 1. ... 2. ... 3. ...
**Inimigo:** ...
**Provas de autoridade:** ...

### Release do autor
**Curto:** ...
**Médio:** ...
**Longo:** ...
```

Exibir confirmação obrigatória:

```
✅ Salvo em: {pasta-ativa}/memoria/brand-voice.md

Próximo passo: /egreen-produto — pesquisa de mercado e 50 ideias de produto
(ou /egreen-copy se o produto já está definido)
```
