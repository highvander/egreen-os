# Landing Page — Estrutura Detalhada

## Decisão VSL vs Copy Longa

**Fase 1 (sem depoimentos):** copy longa — gerada pelo Claude Code em horas
**Fase 2 (com 1+ depoimento):** adicionar vídeo 2–3 min no topo, testar vs copy pura

No nicho de saúde feminina 40–55 anos: vídeo nativo sem produção performa melhor que criativo polido. A audiência é mais cética com conteúdo que parece publicidade.

---

## S1 — Above the Fold

**Objetivo:** parar o scroll e comunicar em 3 segundos se o produto é para aquela pessoa.

**Fórmula da headline:**
```
[Quem] + [Resultado específico] + [Tempo] + [Sem objeção principal]
```

**Exemplo:**
> "For Women 42–55: Sleep Through the Night Again in 21 Days — Without Hormones or Expensive Doctors"

**Subheadline:** clarifica o como em 1 frase
> "The 3-step protocol that 847 women used to finally understand what's happening to their body — and stop it."

**Elementos obrigatórios:**
- Botão CTA grande, copy no imperativo descrevendo resultado
- Sem menu de navegação
- Sem links externos
- Mobile-first — testar em 375px antes de qualquer outro device

---

## S2 — Prova Social Rápida

**Sem depoimentos reais (fase 1):**
- Número de downloads do lead magnet
- "847 women on the waitlist before launch" (se verdadeiro)
- "Based on research from Mayo Clinic, Harvard Health, and NIH" — cita a ciência, não a si mesmo
- Nunca inventar números ou usar fotos de banco de imagem como clientes reais

**Com depoimentos (fase 2+):**
```
"I slept through the night for the first time in 8 months on day 4."
— Sarah M., 47, Texas

* Individual result. Most participants report improved sleep quality
  within 2–3 weeks of consistent application.
```

**Regra FTC:** depoimento com resultado específico SEMPRE com disclaimer abaixo.

---

## S3 — Problema e Dor

**Sequência Brunson:** emoção → lógica → medo/urgência

**Nesta seção:** apenas emoção — primeira pessoa do avatar.

- Começa no pior momento emocional, não no início da história
- Agita a dor sem resolver ainda
- Faz a pessoa pensar "ela está descrevendo exatamente o que sinto"
- Termina com a pergunta que o produto responde

**Nunca nesta seção:** claims médicos, soluções, preço.

---

## S4 — Mecanismo Único

**Objetivo:** lógica — explicar POR QUE outros métodos falharam e apresentar a solução como nova categoria.

- Nome o mecanismo (cria propriedade intelectual percebida)
- Explica em linguagem simples o que acontece no corpo
- Mostra que as soluções anteriores atacam o sintoma, não a causa
- Apresenta o produto como a única abordagem que ataca a causa real

**Não precisa ser cientificamente revolucionário** — precisa ser enquadrado de forma que faça sentido para o avatar.

---

## S5 — Value Stack (Hormozi)

**Formato visual obrigatório:**

```
✓ [Nome do Produto Principal]          — Valor $97
✓ Bônus 1: [Nome]                      — Valor $47
✓ Bônus 2: [Nome]                      — Valor $37
✓ Bônus 3: [Nome]                      — Valor $27
────────────────────────────────────────────────────
  Total Value                           $208
  Seu preço hoje                         $27
```

**Regras:**
- Valores declarados precisam ser defensáveis — seria vendido sozinho por esse preço?
- Nunca inflar valores absurdamente — destrói credibilidade
- Cada bônus remove uma objeção específica e nomeada
- O preço $27 deve parecer irracional não comprar após ver o stack

---

## S6 — CTA + Garantia + Checkout

**Garantia:**
```
30-Day Money-Back Guarantee
If you are not completely satisfied for any reason, contact us within
30 days and we will issue a full refund — no questions asked.
```

**Copy do botão principal:** resultado, não ação
- ✓ "Yes, I Want to Sleep Through the Night"
- ✗ "Add to Cart" / "Buy Now" / "Purchase"

**Botão secundário** (abaixo da garantia):
- "Start Reading in 60 Seconds"

**Checkout:**
- Embed na própria página (não redirect) — converte 15–25% mais
- Checkbox de aceite dos ToS antes de confirmar
- Hotmart: embed via iframe ou botão direto sem sair da página

**Disclaimer médico** (footer obrigatório em produtos de saúde):
```
This product is for informational and educational purposes only.
It is not intended to diagnose, treat, cure, or prevent any disease
or medical condition. Results may vary. Always consult your
healthcare provider before making changes to your health regimen.
```

---

## Checklist Técnico Pré-Lançamento

- [ ] Página carrega em < 3 segundos no mobile (PageSpeed > 80)
- [ ] Sem menu de navegação nem links que tiram o visitante da página
- [ ] Meta Pixel disparando ViewContent ao carregar
- [ ] InitiateCheckout disparando ao clicar em comprar
- [ ] Checkout testado com compra real de $1
- [ ] Email de confirmação chegando em < 2 minutos após compra
- [ ] Disclaimer médico visível no footer
- [ ] ToS + Privacy Policy linkados no footer
- [ ] Checkbox de aceite ativo no checkout