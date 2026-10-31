# Análise do GPT "[FLUXO] Gerador de Oferta" (VTSD) + spec do `/egreen-oferta`

> Data: 2026-10-31. Rodei dois testes com produtos fictícios no ChatGPT (conta do usuário):
> - **T1:** curso simples "Horta na Varanda", R$ 97 (fluxo completo até a oferta final)
> - **T2:** mentoria em grupo "Agenda Cheia Particular", R$ 1.997, 3 meses (até a etapa de entregáveis)
>
> Este documento registra só a estrutura e a lógica observadas. Nenhum prompt ou texto do curso foi copiado.

---

## 1. Como o GPT funciona

### Fluxo observado (igual nos dois testes)

| Etapa | O que faz | Formato |
|---|---|---|
| 0. Senha | Pede a senha de acesso do curso antes de começar | Gate |
| 1. Coleta | Pede **5 insumos de uma vez** e não avança enquanto faltar algum | Lista numerada |
| 2. Entregáveis | Gera sugestões em **9 categorias fixas** com base nas fases do método e pede pro usuário escolher | Widget de seleção (checkbox) |
| 3. Bônus | Pergunta se já existe bônus; se não, cria **3 bônus, cada um ligado a uma objeção** | Card por bônus |
| 4. Garantia | Recomenda 7 dias incondicional; pergunta prazo da garantia + tempo de acesso | Pergunta |
| 5. Preço e pagamento | Confirma preço; pergunta Pix, cartão, parcelas, boleto | Pergunta |
| 6. Consolidação | Oferta final em 8 seções e encerra com "próxima etapa" (sugere que ele é encadeado com outros GPTs) | Documento |

Obs.: as etapas 3, 4 e 5 vieram na mesma mensagem, uma logo depois da outra, sem aprovar o bônus antes.

### Insumos da etapa 1

1. **Quadro**: transformação principal
2. **Furadeira**: método passo a passo
3. **Identidade do Consumidor**: idade/perfil, dores, desejos, hábitos
4. **Objeções**: medos, dúvidas, crenças
5. **Decorados** em **5 categorias**: Financeiro, Tempo, Autoestima, Reputação, Crescimento

→ Confirma que o GPT Oferta **depende** dos GPTs anteriores (Quadro, Furadeira, Consumidor, Objeções, Decorados). É o fim da cadeia de criação de produto.

### As 9 categorias de entregáveis

1. Treinamentos/aulas gravadas (1 aula por fase do método + 1 de fechamento, **cada aula com uma metáfora**)
2. Aulas ao vivo/mentorias
3. Modelos/templates
4. Checklists/guias rápidos
5. Scripts/prompts
6. Ferramentas customizadas (calculadoras, calendário, diário)
7. Suporte/comunidade
8. Portfólio/casos reais
9. Desafios/missões (1 missão por fase, com nome gamificado)

Cada categoria termina com uma frase de valor ("São atalhos que eliminam a dúvida…").
O volume escala com o ticket: T1 (R$ 97) teve 5 aulas e encontros ao vivo opcionais; T2 (R$ 1.997) teve 8 aulas, encontro semanal, 8 templates, 6 scripts, 6 ferramentas.

### Bônus
- 3 bônus, cada um **criado para matar uma objeção específica** ("Objeção eliminada: …")
- Cada um com nome, o que inclui e **valor percebido sugerido**
- Soma dos valores com ressalva "não são preços comprovados"

### Consolidação final (8 seções)
Quadro → Furadeira → Entregáveis → Bônus → Ancoragem de valor (Decorados reescritos + tabela de bônus) → Garantia → Valor e pagamento → Resumo + parágrafo "o grande valor de…"

---

## 2. O que é bom (levar pro EGreen)

- **Bônus = objeção eliminada.** Melhor ideia do GPT. Cada bônus precisa nomear qual objeção derruba.
- **9 categorias de entregáveis** como checklist mental: força a pensar além de "aulas gravadas".
- **Entregáveis derivados das fases do método** (aula por fase, missão por fase): coerência entre Furadeira e oferta.
- **Seleção pelo usuário** antes de seguir: evita oferta inchada.
- **Ressalvas honestas** (metas não garantidas, valores de bônus não comprovados): alinhado com a diretiva anti-escassez falsa do VTSD.
- **Escala por ticket**: o volume de entregáveis acompanha o preço.

## 3. O que é fraco (onde o EGreen pode ser melhor)

| Problema | Evidência | Melhoria no `/egreen-oferta` |
|---|---|---|
| Sem ancoragem de verdade | Só somou bônus (R$ 111). Não valorizou entregáveis principais nem fez "valor total vs preço" | Stack completo: valor de cada item, total, preço, razão de valor (ex.: 10x) |
| Não avalia viabilidade | Ofereceu mentoria ao vivo mensal num curso de R$ 97 sem alertar custo de entrega | Checagem de **custo de entrega × ticket** (horas do expert/mês, escala de alunos) |
| Objeções não cobertas ficam soltas | T1 tinha 6 objeções; bônus cobriram 3; "vai sujar", "condomínio", "mais barato no mercado" ficaram sem resposta | **Matriz objeção → onde é respondida** (entregável, bônus, garantia, FAQ, copy). Nenhuma objeção órfã |
| Garantia genérica | Só ofereceu 7 dias incondicional | Opções de garantia: incondicional, condicional por ação, dupla, de resultado. Escolha justificada pelo ticket e pela objeção principal |
| Preço não é discutido | Aceitou o preço dado sem questionar | Sanity check de preço (valor da transformação, concorrência, formato em `memoria/formatos.md`). Sugere, não impõe |
| Método sem nome | Furadeira ficou "método em 4 etapas" | Nomear o mecanismo (VTSD: "nomear cria realidade") |
| Sem urgência legítima | Nenhuma | Campo opcional: urgência real (bônus de fundador, turma com vagas reais, preço de lançamento com data). Proíbe escassez falsa |
| Sem order bump / upsell | Oferta isolada | Gancho opcional pro `/egreen-posvenda` (order bump e upsell derivados da oferta) |
| Etapas 3–5 de uma vez | Bônus nem foi aprovado antes da garantia | Aprovação bloco a bloco (padrão do EGreen) |
| Pede tudo de novo | Usuário redigita Quadro, Furadeira etc. | Lê da memória/concepção do produto ativo; só pergunta o que falta |
| Imagens aleatórias da web | Cards com fotos de sites aleatórios | Não usar |

---

## 4. Spec do `/egreen-oferta`

**Posição no pipeline:** depois de `/egreen-concepcao` (e de `/egreen-curriculo` ou `/egreen-experiencia` quando houver), antes de `/egreen-copy`, `/egreen-landing`, `/egreen-vsl`, `/egreen-mandala`.

**Saída:** `{pasta-ativa}/egreen-oferta/YYYY-MM-DD-oferta-{produto}.md` + resumo em `{pasta-ativa}/memoria/egreen-oferta.md` (lido pela copy, landing, vsl, mandala, posvenda).

### Passo 0 — Gate e memória
- REGRA 1 e 2 do CLAUDE.md.
- Ler `egreen-produto.md`, `egreen-nicho.md`, `egreen-funil.md`, `formatos.md` e o último arquivo de `egreen-concepcao/`.
- Montar os 5 insumos (Promessa, Mecanismo, Consumidor, Objeções, Benefícios nas 5 categorias) a partir da memória. **Perguntar só o que faltar**, uma pergunta por vez.
- Se faltar Mecanismo ou Objeções (hoje a concepção não gera), coletar aqui. Ver item 2 do roadmap em `2026-10-31-avaliacao-gpts-vtsd.md`.

### Bloco 1 — Mecanismo nomeado
- 5 opções de nome para o método (Furadeira), com as fases.
- Aprovação.

### Bloco 2 — Entregáveis
- Sugestões nas 9 categorias, derivadas das fases do método (aula por fase, missão por fase).
- Recomendação de pacote enxuto conforme o ticket (low < R$ 200, mid até R$ 997, high acima disso).
- **Checagem de custo de entrega:** alerta quando um item ao vivo/individual não escala no ticket.
- Usuário escolhe. Aprovação.

### Bloco 3 — Matriz de objeções
- Tabela: objeção → resposta → onde é respondida (entregável, bônus, garantia, FAQ, copy).
- Toda objeção sem resposta vira candidata a bônus.
- Aprovação.

### Bloco 4 — Bônus
- 3 bônus (ou os que o usuário já tem), cada um com: nome, o que inclui, **objeção eliminada**, valor de referência.
- Aprovação.

### Bloco 5 — Garantia
- 3 opções (incondicional; condicional por ação; de resultado/dupla) com prós e contras para o ticket.
- Tempo de acesso.
- Aprovação.

### Bloco 6 — Preço, stack e pagamento
- Sanity check do preço (valor da transformação a partir dos benefícios financeiros, faixa do formato, concorrência se houver pesquisa em `egreen-pesquisa/`).
- **Stack de valor:** cada entregável + bônus com valor de referência, total, preço, razão de valor.
- Condições: Pix, cartão/parcelas, boleto.
- Urgência **só se for real** (data, vagas, bônus de fundador). Bloquear contador falso.
- Ressalvas: valores de referência não são preço comprovado; metas não são resultado garantido.
- Aprovação.

### Bloco 7 — Consolidação
- Documento final: Promessa → Mecanismo → Entregáveis → Bônus → Stack → Garantia → Preço/pagamento → Resumo de 1 parágrafo (Big Idea da oferta).
- Sugestão de order bump e upsell derivados → próximo passo `/egreen-posvenda`.
- Salvar (REGRA 3) e oferecer próximo passo: `/egreen-copy`.

### Integrações a ajustar depois
- `egreen-copy`: Blocos Entregáveis, Bônus, Stack, Garantia e FAQ passam a ler `memoria/egreen-oferta.md`.
- `egreen-lancamento`: inserir `/egreen-oferta` entre concepção e copy (gate de aprovação da oferta).
- `CLAUDE.md` e README: tabela do pipeline e mapa de pastas.
