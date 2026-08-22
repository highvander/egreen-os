---
name: egreen-meta-auth
description: >-
  Use quando o usuário quiser conectar o projeto com o Meta Ads, configurar autenticação
  (MCP OAuth ou App via Facebook Developers), gerar token permanente, validar ou trocar
  o modo de conexão. Dispara com "conectar Meta Ads", "configurar token Facebook",
  "quero anunciar no Meta", "setup Meta Ads", "como conecto o Meta", "validar minha
  conexão Meta", ou qualquer variação de configuração de acesso ao Meta Ads.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, AskUserQuestion
model: sonnet
---

# Tráfego Conexão — Conectar Projeto com o Meta Ads

Orquestrador do fluxo de conexão. Pergunta o modo, executa o caminho escolhido e salva
a preferência em `META_AUTH_MODO` no `.env`.

A especificação técnica completa está em `.claude/skills/egreen-meta-auth/spec.md`.

Os dois modos suportados são:

- **`MCP_CONECTOR`**. Conector MCP da Meta no Claude Desktop. Login via OAuth. Recomendado.
- **`APP`**. App via Facebook Developers + token permanente salvo no `.env`. Portável entre máquinas.

---

## Pré-requisito (gate antes do Passo 0)

Confirmar que o usuário já tem os 5 itens prontos no Meta. Se faltar qualquer um, parar e
instruir a configurar antes de retornar. Não ensinar a configurar BM, Página ou Pixel pelo chat.

Itens obrigatórios:

1. Business Manager (Portfólio Empresarial) criado em business.facebook.com
2. Página do Facebook (Fanpage) vinculada ao Business Manager
3. Conta de Anúncios ativa dentro do Business Manager (com moeda e fuso configurados)
4. Forma de pagamento cadastrada na Conta de Anúncios
5. Pixel (Conjunto de Dados) criado no Gerenciador de Eventos

Se o usuário não tiver certeza, oferecer:

```
Antes de conectar com o Meta, você precisa ter 5 coisas
prontas no seu Business Manager:

1. Business Manager criado
2. Página do Facebook vinculada
3. Conta de Anúncios ativa
4. Forma de pagamento cadastrada
5. Pixel criado

Você já tem tudo isso?

1. Sim, pode continuar
2. Não sei / falta algo

Digite o número:
```

- Opção 1: seguir para o Passo 0.
- Opção 2: parar e instruir a criar os 5 itens no Meta antes de retornar.

---

## Passo 0. Verificar estado atual

Aplicar a seção **1. Passo 0** do spec.md. Resumo:

- Se `META_AUTH_MODO` já existe com valor `MCP_CONECTOR` ou `APP`: oferecer manter, trocar ou validar.
- Se existe com valor inválido: avisar e seguir para o Passo 1.
- Se não existe ou está vazio: seguir para o Passo 1 sem aviso.

---

## Passo 1. Escolher modo de conexão

Aplicar a seção **2. Passo 1** do spec.md. O usuário escolhe:

1. MCP da Meta via Claude (recomendado).
2. App via Facebook Developers.

Encaminhar para o caminho escolhido.

---

## Passo 2A. Caminho MCP

🔍 Próximo passo: adicionar o MCP da Meta como conector personalizado no Claude Desktop. Tempo estimado: cerca de 60 segundos.

Aplicar a seção **3. Caminho A** do spec.md:

- 3.1. Adicionar o conector personalizado (URL `https://mcp.facebook.com/ads`, nome "Meta Ads").
- Aguardar a confirmação "conectei" do usuário.
- Seguir para o Passo 3.

---

## Passo 2B. Caminho App

🔍 Próximo passo: criar o aplicativo no Facebook Developers e gerar o token permanente. Tempo estimado: 8 a 12 minutos.

Aplicar a seção **4. Caminho B** do spec.md em sequência:

- 4.1. Criar o aplicativo no Facebook Developers (5 etapas + política de privacidade + publicar).
- 4.2. Gerar token permanente via Usuário do Sistema (criar usuário, atribuir ativos, gerar token).
- 4.3. Descobrir o ID da conta de anúncios via API. **Nunca pedir o ID manualmente.** Com o token em mãos, listar automaticamente as contas e oferecer escolha.

Pedir ao usuário apenas **o token** nesse momento. O ID da conta é descoberto via API logo em seguida.

Seguir para o Passo 3.

---

## Passo 3. Validar conexão

🔍 Próximo passo: validar a conexão. Tempo estimado: cerca de 20 segundos.

Aplicar a seção **5. Validação Final** do spec.md, conforme o modo:

- Modo MCP: aplicar 5.1 (chamar tool de leitura do MCP).
- Modo APP: aplicar 5.2 (3 testes na Graph API) e, em caso de erro, 5.3 (mapa de erros).

Não salvar `META_AUTH_MODO` no `.env` antes da validação passar.

✅ Concluído: conexão validada.

---

## Passo 4. Salvar no `.env`

Aplicar a seção **6. Salvamento no `.env`** do spec.md, conforme o modo:

### Modo MCP

Salvar `META_AUTH_MODO=MCP_CONECTOR` e `FB_AD_ACCOUNT_ID` (da seleção 5.1.1).

### Modo APP

**OBRIGATÓRIO** seguir esta sequência:

1. **Salvar** `META_AUTH_MODO=APP` e `FB_ACCESS_TOKEN_PERMANENTE={token}` no `.env`.
2. **Listar AUTOMATICAMENTE** todas as contas que o token enxerga:

   ```bash
   curl -s "https://graph.facebook.com/v25.0/me/adaccounts?fields=id,account_id,name,account_status,currency&limit=100&access_token=TOKEN"
   ```

3. **Processar conforme seção 6.3** do spec.md:
   - **1 conta:** salvar `FB_AD_ACCOUNT_ID` direto.
   - **2+ contas:** mostrar tabela, perguntar padrão, salvar `FB_AD_ACCOUNT_ID` + `FB_AD_ACCOUNT_IDS`.
   - **0 contas / erro:** orientar a refazer atribuição de ativos (seção 4.2.2 do spec).

A skill **nunca deixa o usuário digitar o ID da conta manualmente**.

---

## Passo 5. Saída final

Aplicar a seção **7. Saída final** do spec.md. Mostrar confirmação com o modo salvo e próximo passo recomendado (`/egreen-meta-ads`).

---

## Princípios que este command nunca viola

Carregar e respeitar os princípios da seção **9** do spec.md. Em especial:

1. Nunca salvar `META_AUTH_MODO` antes da validação passar.
2. Nunca exibir o token no chat. Usar `***TOKEN_MASCARADO***` ou apenas confirmar "salvo".
3. Cada chamada `curl` à Graph API é uma `Bash` independente, com token inline. Nunca empacotar com `python3 << 'EOF'` nem `curl | python3 -c`.
