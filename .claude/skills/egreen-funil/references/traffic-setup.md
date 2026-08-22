# Setup de Tráfego Pago — Meta Ads

## Filosofia: Conservador e Paciente

- Estrutura 1-1-1 antes de 1-1-5
- 7–10 dias sem mexer antes de julgar
- UGC amador/nativo em vez de produção profissional
- Escala lenta: +20–30%/semana quando positivo (não por dia na fase 1-2)

---

## Fase 1 — Validação (Dias 1–14)

**Estrutura:** 1 campanha ABO → 1 conjunto Advantage+ → 1 criativo UGC

**Budget:** $30–50/dia

**Público:** Advantage+ audience (sem interesse manual)
- Com pixel zerado, audiência aberta performa melhor
- O algoritmo tem mais espaço para aprender quem converte

**Criativo UGC amador:**
- Vídeo vertical 9:16, 15–30 segundos
- Hook nos primeiros 3 segundos com dor específica
- Tom de conversa — câmera de celular, sem fundo clean
- Sem música de fundo, sem legendas animadas elaboradas
- Mistura-se ao feed orgânico → mais confiança

**Regra absoluta dos 7–10 dias:**
- NÃO pausar, NÃO mudar orçamento, NÃO trocar criativo
- **Única exceção:** CTR < 0.5% nos primeiros 3 dias → trocar só o hook (não o produto, não o preço, não a landing page)

**Gate para avançar para Fase 2:**
- ROAS ≥ 1.0
- CPM estável
- Mínimo 1 venda confirmada
- 7+ dias rodando

---

## Fase 2 — Otimização (Dias 15–30)

**Expandir para 1-1-5 (5 ângulos diferentes):**
1. Dor física (sintoma específico do avatar)
2. Invisibilidade médica ("seu médico disse que é normal?")
3. Identidade ("ainda sou eu?")
4. Prova social (número de pessoas com o mesmo resultado)
5. Mecanismo/curiosidade ("o hormônio que ninguém te explicou")

**Retargeting (campanha separada):**
- NUNCA no mesmo conjunto do tráfego frio
- Budget: 20% do total
- Público: visitantes dos últimos 7 dias
- Criativo diferente: foca em objeções de quem já viu mas não comprou

**Escala dos vencedores:**
- +20–30% por semana (não por dia)
- Apenas nos criativos com ROAS ≥ 1.5 sustentado
- Escalar mais de 50% de uma vez reinicia o aprendizado

**Gate para avançar para Fase 3:**
- ROAS ≥ 1.5 sustentado por 2+ semanas
- 1 criativo vencedor claro identificado
- CAC estável

---

## Fase 3 — Escala (Mês 2–3)

**Meta (escala principal):**
- Migrar de ABO para CBO nos vencedores
- +20–30%/semana no criativo campeão
- Budget alvo: $80–150/dia

**TikTok (teste separado):**
- Entra apenas nesta fase — nunca na fase 1 ou 2
- Budget fixo e separado do Meta (não canibaliza)
- Mesmo criativo UGC que já provou converter no Meta
- Avaliar em 14 dias: ROAS < 0.8 → pausar; > 1.0 → escalar

**Backend (LTV):**
- Ativar membership com conteúdo novo mensal
- Estruturar high ticket $297 para compradores engajados

---

## Pixel e Atribuição

**Setup obrigatório ANTES do primeiro anúncio:**

1. Meta Pixel instalado na landing page (ViewContent + InitiateCheckout)
2. Conversions API (CAPI) via Hotmart nativo — contorna bloqueio iOS
3. UTMs em todos os criativos: `utm_source=meta&utm_medium=paid_social&utm_campaign=f1&utm_content=[nome-criativo]`
4. UTMs em todos os links do Brevo: `utm_source=brevo&utm_medium=email&utm_campaign=pre_compra&utm_content=e03`

**Event Match Quality (EMQ):**
- Meta score de 0–10 para qualidade dos eventos CAPI
- Alvo: ≥ 6.0 — abaixo disso o CPM sobe
- Para aumentar: enviar email hasheado SHA-256 no user_data

**Métricas de controle diário:**

| Métrica | OK | Alerta | Ação |
|---|---|---|---|
| CTR | > 0.8% | < 0.5% por 3 dias | Trocar hook |
| CPM | < $25 | > $30 | Revisar copy — possível flag compliance |
| Taxa conv. LP | > 1.5% | < 0.8% | Testar nova headline |
| ROAS | > 1.0x | < 0.7x por 7 dias | Não escalar · revisar oferta |
| Chargeback | < 0.5% | > 0.9% | Revisar suporte imediatamente |

---

## Criativo UGC — Roteiro Padrão

```
[0–3s] HOOK — dor específica em 1 frase
"Se você tem [idade]+ e [sintoma específico], isso é para você."

[3–18s] STORY — jornada identificável
"Há [X meses] eu [pior momento]. [Médico/solução anterior] disse [frustração].
Descobri que [insight novo]. Comecei a [ação] e em [X dias] [resultado específico]."

[18–28s] OFFER — solução + CTA
"Criei um [produto] com exatamente o que funcionou. Link na bio / abaixo.
[Garantia de 30 dias]. Você não tem nada a perder."
```

**Regra:** o roteiro é gerado pelo Claude Code a partir do briefing.json do ciclo — não criar manualmente.