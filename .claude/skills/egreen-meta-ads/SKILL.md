---
name: egreen-meta-ads
description: >-
  Use quando o usuário quiser subir campanha nova no Meta Ads (Facebook + Instagram).
  Dispara com "subir campanha", "criar campanha", "lançar anúncio", "rodar tráfego",
  "anunciar produto no Facebook", "quero criar anúncio no Instagram", "montar campanha
  de vendas", "campanha de captação de leads" ou qualquer variação de criação de campanha
  no Meta Ads. Cobre apenas OUTCOME_SALES (perpétuo de venda direta) e OUTCOME_LEADS
  (captação). Não cobre Awareness, Traffic, Engagement ou App Promotion.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, Skill, AskUserQuestion
model: sonnet
---

# Trafego Criar Campanha — Subir Campanha Meta Ads

Sobe campanha nova no Meta Ads diretamente via Marketing API, com preview YAML obrigatório
e status PAUSED por padrão. Foca em infoprodutos: venda direta (`OUTCOME_SALES`) ou captação
de leads (`OUTCOME_LEADS`). Não toca em outros objetivos.

A especificação técnica completa está em `.claude/skills/egreen-meta-ads/spec.md`.

---

## Passo 0. Contexto e validação

### 0.1 Produto ativo

Leia `memoria/egreen-produto.md` para inferir produto, ticket, posicionamento e público quando
o usuário não declarar explicitamente.

### 0.2 Conexão Meta (gate duro, passo zero obrigatório)

Leia `META_AUTH_MODO` no `.env`.

- **Se vazio ou ausente:** acione `/egreen-meta-auth` antes de prosseguir.
- **Se `MCP_CONECTOR`:** confirmar que pelo menos uma tool `mcp__*__ads_*` está disponível.
  Se nenhuma estiver, pedir ao usuário para reabrir o Claude Code (MCP às vezes precisa de reload).
  Se persistir, voltar a `/egreen-meta-auth`.
- **Se `APP`:** confirmar que `FB_ACCESS_TOKEN_PERMANENTE`, `FB_AD_ACCOUNT_ID` e `FB_PAGE_ID`
  existem no `.env`. Se faltar algum, acionar `/egreen-meta-auth`.

A skill nunca prossegue sem essa validação passar.

### 0.3 Seleção de conta de anúncio (multi-conta)

1. Ler `FB_AD_ACCOUNT_IDS` no `.env`.
2. Se não existe ou vazio, usar `FB_AD_ACCOUNT_ID` direto.
3. Se tem 1 conta, usar direto sem perguntar.
4. Se tem 2 ou mais, perguntar qual usar nesta campanha (não sobrescrever `.env`).

### 0.4 Ler especificação da skill

Leia `.claude/skills/egreen-meta-ads/spec.md` para carregar fluxo de coleta,
validações de pixel, formato do preview YAML e ordem de criação.

---

## Passo 1. Detectar modo

Se a primeira mensagem já tem objetivo + produto + budget + público + criativo + tracking,
ir para **modo expresso** (Passo 4 direto).

Caso contrário, **modo guia**: começar pela Fase 1 do spec.

---

## Passo 2. Conduzir as 9 fases (modo guia)

Aplicar as Fases 1 a 9 do spec, uma pergunta por mensagem:

1. **Objetivo**. Sales ou Leads.
2. **Produto e ticket**. Infere de `memoria/egreen-produto.md` se possível, senão pergunta.
3. **Estrutura**. 1-X-1, 1-1-X ou X-1-1.
4. **Orçamento**. ABO ou CBO + valor diário.
5. **Tracking** (gate duro). Validar pixel ativo + evento recebendo dados.
6. **Público**. Advantage+ ou segmentação manual.
7. **Criativos**. Existentes na biblioteca ou subir novos. Geração de copy e imagem fora do escopo.
8. **Posicionamentos**. Advantage+ Placements (default) ou manual.
9. **Nome da campanha**. Padrão automático, usuário pode editar.

---

## Passo 3. Validar pixel (gate duro)

🔍 Próximo passo: validar pixel e evento de conversão. Tempo estimado: cerca de 15 segundos.

Antes de seguir para o preview:

1. Listar pixels da conta. Confirmar que o ID informado existe.
2. Buscar stats do evento. Confirmar que está recebendo dados nos últimos 7 dias.

Se pixel inexistente: parar e orientar a criar pixel antes de retornar.
Se pixel existe mas sem dados nos últimos 7 dias: avisar e pedir confirmação para prosseguir.

✅ Concluído: pixel e evento validados.

---

## Passo 4. Preview YAML

Montar o bloco `preview_campanha` completo conforme seção 3 do spec. Apresentar como
**resumo em texto corrido** (não YAML bruto — ver seção 3.2 do spec). Se o usuário
pedir o YAML explicitamente, abrir o arquivo salvo.

Salvar preview em: `egreen-meta-ads/preview-campanha-{tipo_funil}-{slug}-{YYYY-MM-DD}.yaml`

Pedir aprovação:

```
Esse é o preview da campanha. Confirma criar com status PAUSED?

1. Confirmo, pode subir
2. Quero ajustar algo
3. Cancela

Digite o número:
```

---

## Passo 5. Criação

🔍 Próximo passo: criar campanha, conjuntos e anúncios via Marketing API. Tempo estimado: 1 a 2 minutos.

Aplicar a ordem da seção 4 do spec:

1. Criar campanha (status PAUSED)
2. Para cada conjunto: criar conjunto
3. Para cada anúncio: criar criativo → criar anúncio

Anunciar progresso:
```
⏳ Passo 1/3: criando campanha "[nome]"...
⏳ Passo 2/3: criando [N] conjunto(s)...
⏳ Passo 3/3: criando [N] anúncio(s)...
```

Em caso de falha: preservar o que subiu, listar falhas, perguntar se quer tentar manualmente.

✅ Concluído: campanha criada com status PAUSED.

---

## Passo 6. Apresentar resultado e salvar resumo

Mostrar IDs, link do Gerenciador e próximos passos (ver seção 5 do spec).

Salvar resumo em:
```
egreen-meta-ads/campanha-{nome-slug}-{YYYY-MM-DD}.md
```

Conteúdo: preview YAML aprovado + IDs gerados + link do Gerenciador + próximos passos.

---

## Ativação posterior

Se o usuário disser "ativa a campanha [nome|id]":

1. Confirmar: "Vou ativar a campanha agora. Uma vez ativa, começa a gastar. Confirma?"
2. Se confirmado: ativar via API (ver seção 7.6 do spec). Passa pelo gate 🛡️.

---

## Princípios que este command nunca viola

1. **Sales/Leads sem pixel = não cria.** Gate duro.
2. **Sempre PAUSED por default.** Ativação só com pedido explícito posterior.
3. **Preview obrigatório, sempre.** Mesmo no modo expresso.
4. **Não cobre objetivos fora de Sales/Leads.** Recusa Awareness, Traffic, Engagement, App Promotion.
5. **Liberdade de estrutura.** Usuário pode pedir customizada.
6. **Nunca chama edição.** Edição mora em `/trafego-otimizar` e `/trafego-escalar`.
7. **Falha parcial preserva.** Não faz rollback completo automático.
8. **Geração de copy fora do escopo desta skill.**
