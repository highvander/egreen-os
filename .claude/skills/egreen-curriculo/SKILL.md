---
name: egreen-curriculo
description: >
  Desenha o currículo/módulos do infoproduto para os formatos Curso Simples e Curso Completo — a estrutura pedagógica real de entrega (módulos, aulas, objetivo de cada aula, prática e avaliação), não a página de vendas nem o marketing ao redor. Combina três frameworks de design instrucional amplamente reconhecidos: Backward Design de Wiggins & McTighe (definir a transformação e a evidência antes de desenhar qualquer aula), a Taxonomia de Bloom revisada (sequenciar módulos por complexidade cognitiva crescente) e os Nove Eventos de Instrução de Robert Gagné (estrutura de cada aula individual). Use esta skill sempre que o usuário pedir para "criar o currículo do curso", "montar os módulos", "estruturar as aulas", "desenhar a grade curricular", ou pedir ajuda para decidir quantas aulas/módulos o produto deve ter e em que ordem — mesmo sem citar os nomes dos frameworks. Para E-book use `egreen-ebook`; para Desafio, Comunidade ou Mentoria use `egreen-experiencia`.
---

# Currículo do Curso (Backward Design + Bloom + Gagné)

Esta skill desenha o **conteúdo de entrega real** do produto — os módulos e aulas que o aluno efetivamente recebe — para os formatos Curso Simples e Curso Completo definidos em `memoria/formatos.md`. Não é copy de venda (`egreen-copy`), não é posicionamento (`egreen-posicionamento`): é o produto em si.

**Antes de desenhar qualquer módulo, leia `references/frameworks-instrucionais.md`** — os 3 frameworks abaixo vêm de lá, com detalhe operacional completo.

---

## Passo 0 — Carregar memória do produto ativo

```
memoria/produto-ativo.md                    → pasta ativa
{pasta-ativa}/memoria/egreen-nicho.md              → avatar, nível de conhecimento do público
{pasta-ativa}/memoria/egreen-produto.md            → formato (Curso Simples ou Curso Completo), preço
{pasta-ativa}/memoria/egreen-funil.md              → oferta, bônus já definidos
memoria/formatos.md                         → faixa de volume esperada por formato
```

Se existir output de `egreen-concepcao` em `{pasta-ativa}/egreen-concepcao/`, leia o mais recente — **a Promessa e os 5 Baldes de lá são o ponto de partida do Estágio 1 do Backward Design abaixo**, não redefina do zero. Se o formato (Simples vs Completo) já estiver definido em `egreen-produto.md`/`egreen-funil.md`, pule a pergunta correspondente na Fase 0.

**Se existir Escopo Mínimo Viável em `egreen-concepcao`, ele é o teto da v1.** Os Entregáveis Essenciais de lá viram os módulos obrigatórios do currículo (mesmo no Curso Completo). Qualquer módulo além disso (aprofundamento, módulo bônus, tema adjacente) vai para uma seção separada "Módulos de Esteira" no fim do currículo, não misturado com os módulos essenciais — só produza a esteira depois que a v1 validar.

---

## FASE 0 — Intake

Complete o que não veio da memória:

1. Formato: Curso Simples (3-7 aulas) ou Curso Completo (30-60+ módulos, 30-100+ aulas)? — reaproveitar de `egreen-produto.md` se já definido
2. Nível de conhecimento prévio do público-alvo (zero, básico, intermediário) — reaproveitar de `egreen-nicho.md`
3. A transformação final prometida (reaproveitar Promessa de `egreen-concepcao`, ou perguntar se não existir)
4. Quanto tempo/recurso existe pra produzir o conteúdo (afeta quão ambicioso o currículo pode ser)
5. Formato de entrega preferido por aula: vídeo, texto, áudio, ou misto

---

## FASE 1 — Backward Design: definir antes de desenhar

Nesta ordem, sem pular:

1. **Resultado desejado** — declare em uma frase o que o aluno consegue fazer/ser ao final que não conseguia antes (deve ser consistente com a Promessa de `egreen-concepcao`, se existir).
2. **Evidência aceitável** — defina, antes de qualquer módulo, como se prova que o aluno chegou lá: projeto final, checklist de resultado, entrega concreta. Se não for possível definir isso claramente, o resultado do passo 1 ainda está vago — volte e refine antes de seguir.
3. Só agora avance para a Fase 2.

---

## FASE 2 — Sequenciar por complexidade (Bloom)

Distribua os módulos ao longo dos 6 níveis da Taxonomia de Bloom (lembrar → entender → aplicar → analisar → avaliar → criar), do mais simples ao mais complexo. Nunca comece um currículo no nível "aplicar" ou "criar" sem cobrir "lembrar/entender" antes — é a causa mais comum de aluno travado.

- **Curso Simples** (3-7 aulas): geralmente cobre até o nível 3 (aplicar) — um resultado prático rápido, sem aprofundar em análise/avaliação.
- **Curso Completo** (30-60+ módulos): cobre a escada completa até o nível 6 (criar), com módulo(s) de projeto final autônomo.

Para cada nível coberto, liste o(s) módulo(s) correspondentes com um título curto e o objetivo de aprendizagem daquele módulo.

---

## FASE 3 — Estrutura de módulos e volume

Usando `memoria/formatos.md` como referência de volume esperado:

| Formato | Módulos | Aulas |
|---|---|---|
| Curso Simples | módulos simples, pouco aninhamento | 3-7 aulas no total |
| Curso Completo | 30-60+ módulos | 30-100+ aulas |

Para cada módulo, produza: número, título, nível de Bloom correspondente, objetivo de aprendizagem, lista de aulas dentro dele.

---

## FASE 4 — Roteiro de cada aula (Gagné)

Para cada aula listada na Fase 3, aplique os Nove Eventos de Gagné (comprimindo os eventos 1-3 e 8-9 em aulas curtas de Curso Simples, mas nunca eliminando os eventos 6-7 — prática e feedback):

1. Gancho de atenção
2. Objetivo específico da aula
3. Conexão com conhecimento prévio (da aula anterior ou da vida do aluno)
4. Conteúdo (o ensino)
5. Orientação (exemplo, analogia, "como pensar sobre isso")
6. **Prática** — o que o aluno faz, não só assiste
7. **Feedback** — como o aluno sabe se acertou
8. Avaliação do objetivo da aula
9. Ponte pra próxima aula / aplicação na vida real

Sinalize explicitamente se algum item da Fase 3 ficou sem evento 6-7 definido — aula sem prática é a causa mais comum de "curso assistido mas não aplicado".

---

## FASE 5 — Entrega

Apresente o currículo completo em formato de tabela/lista hierárquica (módulo → aulas → objetivo → prática/evidência), seguido da evidência final definida na Fase 1.

---

## Passo Final — Salvar output

```
{pasta-ativa}/egreen-curriculo/{YYYY-MM-DD-descricao-curta}.md
```

Confirmação:
```
✅ Salvo em: {pasta-ativa}/egreen-curriculo/{YYYY-MM-DD-descricao-curta}.md

Próximo passo: gravar/produzir as aulas, ou usar este currículo como base de Entregáveis (Bloco 07) em /egreen-copy
```

---

## Notas de estilo

- Nunca prometer resultado de aprendizagem sem uma prática/evidência correspondente — cada módulo precisa de um "o aluno faz X", não só "o aluno assiste sobre X".
- Não infle o número de módulos/aulas artificialmente para parecer "Curso Completo" — o volume deve ser o que a transformação prometida realmente exige, sinalizando ao usuário se o formato escolhido não bate com a complexidade do resultado.
- Se o usuário pedir E-book, Desafio, Comunidade ou Mentoria, encaminhar para `egreen-ebook` ou `egreen-experiencia` em vez de forçar a estrutura de módulos/aulas aqui.
- Entregar em formato de tabela/lista clara. Se o usuário pedir arquivo específico (planilha, apresentação), gerar no formato apropriado; caso contrário, entregue na conversa e salve o Markdown conforme o Passo Final.
