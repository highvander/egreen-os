---
name: egreen-afiliados
description: >
  Estrutura o programa de afiliados/parceiros do infoproduto — comissão em camadas, kit de material pronto, regras de atribuição e conflito de canal — e a copy de recrutamento/ativação de afiliado. Combina os Princípios de Influência de Robert Cialdini (reciprocidade, prova social, compromisso, escassez, autoridade) aplicados a recrutar e ativar afiliados, com a prática de mercado consolidada nas plataformas dominantes do infoproduto brasileiro (Hotmart, Eduzz, Kiwify). Use esta skill sempre que o usuário pedir "criar programa de afiliados", "como recrutar afiliados", "comissão de afiliado", "kit de divulgação pro afiliado", "carta de convite pra afiliado" — mesmo sem citar Cialdini ou as plataformas.
---

# Programa de Afiliados (Cialdini + Prática de Mercado)

Esta skill estrutura o programa de afiliados/parceiros — regras, comissão, kit — e escreve a copy de recrutamento. Não é a mesma coisa que anúncio pago (`egreen-mandala`/`egreen-meta-ads`): aqui o "comprador" é o afiliado em potencial, não o cliente final.

**Antes de estruturar, leia `references/frameworks-afiliados.md`.**

---

## Passo 0 — Carregar memória do produto ativo

```
memoria/produto-ativo.md                    → pasta ativa
{pasta-ativa}/memoria/egreen-produto.md            → produto, preço
{pasta-ativa}/memoria/egreen-funil.md              → margem disponível pra comissão
{pasta-ativa}/memoria/egreen-nicho.md              → onde encontrar afiliados potenciais (mesmo nicho, público adjacente)
```

Se existir output de `egreen-copywriting`, `egreen-mandala` ou `egreen-emails`, reaproveite como base do kit de afiliado (Fase 2) em vez de escrever do zero.

---

## FASE 0 — Intake

1. Preço e margem do produto (define teto realista de comissão)
2. O produto já tem afiliados hoje, ou é programa novo?
3. Canal de gestão do programa (Hotmart/Eduzz/Kiwify já define parte da estrutura técnica — confirmar qual)
4. Existe rede de possíveis afiliados já mapeada (parceiros, outros produtores do nicho, alunos satisfeitos) ou é preciso recrutar do zero?

---

## FASE 1 — Estrutura do programa

Defina, aplicando a prática de mercado consolidada:

1. **Comissão em camadas** — percentual padrão + percentual maior a partir de volume definido
2. **Janela de atribuição** — prazo do cookie, comunicado sem ambiguidade
3. **Regra de conflito de canal** — o que cada lado pode/não pode fazer (ex: afiliado não pode anunciar pelo nome da marca do produtor)
4. **Cadência de pagamento e suporte** — quando paga, como afiliado tira dúvida

Sinalize ao usuário se algum desses 4 pontos ficou indefinido — programa sem essas regras claras trava ativação de afiliado grande.

---

## FASE 2 — Kit de afiliado

Monte a lista do que precisa existir (reaproveitando outputs já salvos quando existirem):
- Copy de anúncio pronta (de `egreen-copywriting`/`egreen-mandala`)
- E-mails prontos pra lista do afiliado (de `egreen-emails`, adaptado pra tom de terceiro)
- Argumentos de venda / principais objeções já resolvidas (de `egreen-nicho.md`)
- Banners/criativos (referenciar `egreen-carrossel`/`egreen-editorial` se aplicável)

Se algum item não existir ainda, sinalizar como pendência antes do programa ser lançado — programa sem kit pronto tem taxa de ativação muito menor.

---

## FASE 3 — Copy de recrutamento e ativação

Aplique os princípios de Cialdini na carta/mensagem de convite:

1. **Reciprocidade** — apresentar o kit pronto antes de pedir qualquer esforço
2. **Prova social** — se houver, mostrar resultado de afiliados que já estão promovendo (com autorização)
3. **Compromisso e consistência** — pedir um primeiro compromisso pequeno e específico (ex: "compartilhar no story essa semana") em vez de um pedido vago de "divulgar"
4. **Escassez** — se fizer sentido, comissão elevada por tempo limitado ou vagas de "afiliado fundador"
5. **Autoridade** — priorizar recrutamento qualificado (poucos afiliados com autoridade real) sobre volume de afiliados pequenos

---

## Passo Final — Salvar output

```
{pasta-ativa}/egreen-afiliados/{YYYY-MM-DD-descricao-curta}.md
```

Confirmação:
```
✅ Salvo em: {pasta-ativa}/egreen-afiliados/{YYYY-MM-DD-descricao-curta}.md

Próximo passo: configurar o programa na plataforma (Hotmart/Eduzz/Kiwify) e enviar o convite aos primeiros afiliados
```

---

## Notas de estilo

- Nunca prometer comissão acima da margem real definida em `egreen-funil.md`.
- Nunca inventar resultado de afiliado pra usar como prova social — usar só o que o usuário confirmar como real e autorizado.
- Entregar em formato de tabela/lista clara (estrutura do programa) + texto pronto (carta de convite). Se o usuário pedir arquivo específico, gerar no formato apropriado; caso contrário, entregue na conversa e salve o Markdown conforme o Passo Final.
