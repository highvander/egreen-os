---
name: trafego-conexao
description: >
  Especificação técnica completa do fluxo de conexão com o Meta Ads (Facebook + Instagram).
  Cobre os dois modos escolhíveis (MCP do Claude Desktop e App via Facebook Developers) e o
  modo interno HIBRIDO (MCP principal + App de reserva), gravado automaticamente quando o
  aluno no MCP precisa cobrir uma das 4 lacunas do conector.
  No caminho APP, conduz o processo inteiro: criar o aplicativo no developers.facebook.com,
  gerar token permanente via Usuário do Sistema, descobrir via API as contas de anúncios que
  o token enxerga (sem pedir ID manualmente ao aluno), validar com 3 testes na Graph API e
  salvar tudo no .env. Skill consultada pelo command /trafego-conexao.
---

# Tráfego Conexão. Especificação Técnica Completa

Esta skill conecta o projeto com o Meta Ads. O command `/trafego-conexao` é o orquestrador; esta skill carrega a especificação técnica completa de cada passo. Os modos suportados são:

- **`MCP_CONECTOR`**. Conector oficial Claude + Meta. Login via OAuth direto na conta Claude. Sem token permanente, sem App no Facebook Developers, sem instalar nada na máquina. **Recomendado.** Cobre a grande maioria das operações do curso.
- **`APP`**. App via Facebook Developers. Token permanente gerado pelo Usuário do Sistema, salvo no `.env`. Caminho técnico tradicional, portável entre máquinas e planos. Faz **tudo** o que a Marketing API permite.
- **`HIBRIDO`** (modo interno, não aparece no menu). MCP como principal, App como **reserva**. Só existe quando o aluno começou no MCP e depois precisou configurar o App pra cobrir uma operação que o MCP ainda não faz (ver "Lacunas do MCP" e "Protocolo de escalada" abaixo). Nesse modo, as skills usam o MCP em tudo e só caem no token nas operações de lacuna.

### Lacunas do MCP (operações sem ferramenta no conector)

O MCP cobre a maioria das operações, mas **4 operações de escrita ainda não têm ferramenta** e só funcionam no modo `APP`/`HIBRIDO` (token), ou opcionalmente de forma manual no Gerenciador:

1. **Upload de vídeo** de criativo.
2. **Upload de imagem** de criativo a partir de arquivo local.
3. **Busca de interesse** por nome (descobrir o ID de segmentação).
4. **Criar público semelhante (lookalike)**.

> **Tratamento uniforme.** As 4 lacunas seguem **o mesmo protocolo de escalada**, sem distinção. Ao bater em qualquer uma delas no modo MCP, a skill oferece escalar pro App (modo híbrido). O caminho manual no Gerenciador é uma **opção adicional**, oferecida quando faz sentido, nunca a única saída.

Quem usa só o MCP e nunca encosta nessas 4 operações **nunca precisa configurar o App**.

### Protocolo de escalada (MCP → HIBRIDO), regra dura compartilhada

Toda skill do curso segue esta regra ao operar no modo `MCP_CONECTOR`:

1. **Nunca assumir que o token existe.** No modo MCP puro, `FB_ACCESS_TOKEN_PERMANENTE` pode não estar configurado. Jamais montar um `curl` com token nesse modo sem antes confirmar que ele existe.
2. **Ao bater em qualquer uma das 4 lacunas**, parar e oferecer ao aluno (sem distinção entre as lacunas):
   - **(a) Ativar o modo App** (caminho principal, faz a operação pelo chat). Instruir: *"essa operação o MCP ainda não faz. Pra executá-la por aqui, você precisa ativar o modo App (token permanente), o que leva alguns minutos. Quer configurar agora? Rode /trafego-conexao."*
   - **(b) Caminho manual** no Gerenciador da Meta (opção adicional, quando aplicável: criar o lookalike na interface, postar o vídeo na página pra obter o `video_id`, hospedar a imagem numa URL pública). Útil pra quem não quer configurar o App.
3. Se o aluno escolher (a) e configurar o App **com o MCP já ativo**, a `/trafego-conexao` salva `META_AUTH_MODO=HIBRIDO` (não `APP`), preservando o MCP como principal.
4. A partir daí, a skill repete a operação usando o token (fallback) e segue usando o MCP no resto. **No modo `HIBRIDO`, a lacuna já roda direto pelo token, sem reperguntar.**

---

## 0. Pré-requisito do aluno (antes de tudo)

Antes de tentar conectar, o aluno **precisa ter** os 5 itens abaixo prontos no Meta. Sem esses 5 itens, nenhum caminho desta skill funciona.

1. **Business Manager** (Portfólio Empresarial) criado em business.facebook.com
2. **Página do Facebook** (Fanpage) vinculada ao Business Manager
3. **Conta de Anúncios** ativa dentro do Business Manager (com moeda e fuso configurados)
4. **Forma de pagamento** cadastrada na Conta de Anúncios
5. **Pixel** (Conjunto de Dados) criado no Gerenciador de Eventos

Se o aluno chegar nesta skill sem ter algum desses itens, **a skill deve parar** e instruir:

```
Antes de conectar com o Meta, você precisa ter 5 coisas
prontas no seu Business Manager:

1. Business Manager criado
2. Página do Facebook vinculada
3. Conta de Anúncios ativa
4. Forma de pagamento cadastrada
5. Pixel criado

Abra o Bônus 2 do curso (Setup inicial do Meta). Ele tem
o passo a passo completo para criar os 5 itens, mais a
explicação da hierarquia (Business Manager > Conta de
Anúncios > Campanha > Conjunto > Anúncio).

📂 Caminho do arquivo (clique duas vezes no Finder ou Explorer
   para abrir no navegador):
   docs/tutoriais/bonus-2-setup-meta.html

Quando terminar o Bônus 2, volte aqui e rode
/trafego-conexao de novo.
```

Não tentar ensinar a configurar Business Manager, Página, Conta de Anúncios ou Pixel pelo chat. O Bônus 2 cobre isso com prints e passo a passo por etapa.

A skill pode oferecer uma pergunta de checagem rápida quando o aluno não tiver certeza:

```
Você já tem os 5 itens prontos no Meta?

1. Sim, pode continuar
2. Não sei / falta algo

Digite o número:
```

- Opção 1: seguir para o Passo 1.
- Opção 2: mostrar a mensagem acima sobre o Bônus 2 e encerrar.

---

## 1. Passo 0. Verificar estado atual

Leia o arquivo `.env` na raiz do projeto.

**Caso 1. Linha `META_AUTH_MODO` já existe com valor `MCP_CONECTOR`, `APP` ou `HIBRIDO`:**

Pergunte (traduzir o valor pra linguagem do aluno: `MCP_CONECTOR` = "MCP", `APP` = "App", `HIBRIDO` = "MCP com App de reserva"):

```
Já existe uma conexão configurada com o Meta Ads.

Modo ativo: {valor traduzido}

O que você quer fazer?

1. Manter como está
2. Trocar de modo
3. Validar a conexão atual

Digite o número:
```

- Opção 1: encerrar com mensagem de confirmação ("Conexão atual mantida. Modo ativo: {valor}.").
- Opção 2: seguir para o Passo 1 e refazer a configuração. As variáveis do modo anterior (ex: `FB_ACCESS_TOKEN_PERMANENTE`, `FB_AD_ACCOUNT_ID`) ficam no `.env` por segurança, caso o aluno queira voltar para o modo anterior depois.
- Opção 3: pular direto para a Validação (seção 5) usando o modo registrado no `.env`. No `HIBRIDO`, validar os dois (MCP e token), conforme 5.4.

> **Observação sobre o `HIBRIDO`.** Ele não aparece como opção no Passo 1. Só é gravado automaticamente pelo protocolo de escalada (quando um aluno no MCP configura o App pra cobrir uma lacuna). Se o aluno no `HIBRIDO` escolher "Trocar de modo", ele pode ir pro MCP puro ou pro App puro normalmente.

**Caso 2. Linha `META_AUTH_MODO` existe mas o valor é inválido** (qualquer coisa que não seja `MCP_CONECTOR`, `APP` nem `HIBRIDO`):

Avisar o aluno:

```
Encontrei a variável META_AUTH_MODO no .env, mas o valor "{valor}" não é
reconhecido (esperado MCP_CONECTOR ou APP). Vou tratar como se a conexão
não estivesse configurada.
```

Em seguida, ir direto para o Passo 1.

**Caso 3. Linha `META_AUTH_MODO` não existe ou está vazia:** ir direto para o Passo 1, sem aviso.

---

## 2. Passo 1. Escolher modo de conexão

Pergunte exatamente neste formato:

```
Como você quer conectar com o Meta Ads?

1. MCP da Meta via Claude (recomendado)
   Adiciona o servidor MCP oficial da Meta como conector personalizado
   no seu Claude (ainda não está na lista oficial, mas leva 1 minuto
   para registrar) e autoriza via OAuth do Facebook. Sem instalar
   nada na máquina, sem token permanente, sem App no Facebook
   Developers. A conexão fica vinculada à sua conta Anthropic.
   Funciona em qualquer máquina onde você estiver logado na mesma
   conta.

2. App via Facebook Developers
   Cria um App no developers.facebook.com, gera um token permanente
   via Usuário do Sistema e salva no .env. Caminho técnico
   tradicional. Funciona em qualquer plano do Claude. O token fica
   na sua máquina, então é portável e não depende da Anthropic.

Digite o número:
```

- Opção 1: seguir para a seção **3. Caminho A. MCP do Claude Desktop**.
- Opção 2: seguir para a seção **4. Caminho B. App via Facebook Developer**.

---

## 3. Caminho A. MCP do Claude Desktop

> **Atenção.** O MCP da Meta ainda não está na lista oficial de conectores do Claude, então precisa ser adicionado como **MCP personalizado**. É rápido, só leva 1 minuto.

### 3.1 Adicionar o conector personalizado

Instrua o aluno na seguinte ordem, esperando confirmação ao final:

```
Para adicionar o MCP da Meta na sua conta Claude:

1. Abra o aplicativo do Claude Desktop (não vale o site
   https://claude.com/settings/connectors, esse caminho não
   tem mais a opção de adicionar MCP personalizado).

2. Clique em "Customize" (Personalizar) e depois em
   "Connectors" (Conectores).

3. Dentro de Conectores, clique no símbolo de "+" e escolha
   "Adicionar conector personalizado" (Add custom connector).

4. Preencha os campos do conector personalizado:
   - URL do servidor: https://mcp.facebook.com/ads
   - Nome da conexão: Meta Ads
     (pode usar outro nome se quiser, mas "Meta Ads" deixa fácil
     de identificar depois)

5. Clique em "Adicionar" / "Salvar" para registrar o MCP.

6. Vai abrir uma aba do Facebook pedindo autorização. Faça assim:
   - Entre com a conta de admin do Business Manager que tem a
     conta de anúncios que você quer usar
   - Selecione a Página do Facebook e o perfil do Instagram que
     quer autorizar
   - Confirme as permissões pedidas

7. Quando voltar ao Claude e o status do MCP "Meta Ads" estiver
   "Conectado", me avisa aqui ("conectei", "feito" ou similar) que
   continuo a validação.
```

Aguardar a resposta do aluno.

> **Atenção, conector é por conta Anthropic, não por máquina.** Se o aluno usar o Claude em outra máquina logada na mesma conta, o MCP Meta Ads segue ativo lá também. Não precisa adicionar de novo.

Quando o aluno confirmar, seguir para a seção **5. Validação Final**.

---

## 4. Caminho B. App via Facebook Developer

Conduz a criação completa do aplicativo, geração do token permanente e obtenção do ID da conta. Tudo dentro desta skill, sem chamar sub-skills externas.

### 4.0.0 Checar token existente ANTES de mostrar qualquer passo de criação (regra dura)

**Antes de exibir o passo a passo de criação do App (4.1 e 4.2), checar se já existe um token salvo.** O aluno pode já ser dono de um App configurado, com o token gravado no `.env` por uma execução anterior. Mostrar o passo a passo de criação do zero nesse caso gera retrabalho e confusão.

Checar presença sem expor o valor:

```bash
grep -q "^FB_ACCESS_TOKEN_PERMANENTE=" .env && echo "presente" || echo "ausente"
```

- **Token presente:** **pular 4.1 e 4.2 inteiras.** Avisar o aluno que já encontrou um token salvo e perguntar:

  ```
  Encontrei um token de App já salvo no seu projeto. O App já está
  configurado. O que você quer fazer?

  1. Usar o token que já tenho (recomendado, valido na hora)
  2. Gerar um token novo (vou te passar o passo a passo)

  Digite o número:
  ```

  - Opção 1: ir direto para a **Validação** (seção 5.2 para APP puro, ou 5.4 para HIBRIDO). Se passar, salvar o modo (6.2/6.4) e seguir para a saída. Não recriar nada.
  - Opção 2: seguir o passo a passo normal (4.1 em diante).

- **Token ausente:** seguir o fluxo normal a partir de 4.0 (decidir APP puro vs HIBRIDO) e depois 4.1.

> Esta checagem vale em qualquer entrada no Caminho B, inclusive quando a skill é acionada pelo **protocolo de escalada** (MCP→HIBRIDO) vindo de outra skill. Validar o que já existe sempre vem antes de criar do zero.

### 4.0 Detectar se o MCP já está ativo (define APP puro vs HIBRIDO)

Antes de iniciar a configuração do App, determinar o destino final do `META_AUTH_MODO`:

1. **O modo atual no `.env` é `MCP_CONECTOR` (ou `HIBRIDO`)**, OU o aluno chegou aqui pelo **protocolo de escalada** (veio de outra skill que bateu numa lacuna)? Então o objetivo é **manter o MCP como principal e adicionar o App como reserva**. Confirmar com o aluno:

   ```
   Você já está com o MCP ativo. Vou manter o MCP como principal e
   configurar o App apenas como reserva, pra cobrir as operações que o
   MCP ainda não faz (upload de vídeo, upload de imagem, busca de
   interesse, lookalike). No fim, o modo fica registrado como "MCP com
   App de reserva".

   1. Perfeito, manter o MCP como principal
   2. Não, quero trocar de vez pro App (abandonar o MCP)

   Digite o número:
   ```

   - Opção 1: ao final da configuração, salvar `META_AUTH_MODO=HIBRIDO` (seção 6.4).
   - Opção 2: ao final, salvar `META_AUTH_MODO=APP` (seção 6.2).

2. **O modo atual é vazio/ausente, ou o aluno escolheu o App direto no Passo 1 sem MCP ativo:** o objetivo é `APP` puro. Ao final, salvar `META_AUTH_MODO=APP` (seção 6.2).

Seguir a configuração (4.1 a 4.3) é idêntico nos dois casos. A diferença é só qual valor de `META_AUTH_MODO` será gravado no final.

### 4.1 Criar o aplicativo no Facebook Developers

Acesse developers.facebook.com e faça login com a conta de admin do negócio. Clique em "Meus Apps" > "Criar App".

**Etapa 1. Detalhes do app**
- Nome do app: use "Relatorio de Anuncios" ou qualquer nome simples
- Email de contato: já vem preenchido com o email do Facebook, pode deixar como está
- Clique em "Avançar"

**Etapa 2. Casos de uso (passo crítico)**
- A tela abre com o filtro "Em Destaque" selecionado, mostrando apenas 6 opções
- Troque o filtro para "Tudo" para ver todas as opções disponíveis
- Selecione TODOS os 7 casos de uso abaixo (marcar o checkbox de cada um):
  1. Criar e gerenciar anúncios com a API de Marketing
  2. Mensurar dados de desempenho do anúncio com a API de Marketing
  3. Capturar e gerenciar leads de anúncios com a API de Marketing
  4. Criar e gerenciar anúncios de apps com o Gerenciador de Anúncios da Meta
  5. Anuncie no seu app com o Meta Audience Network
  6. Gerenciar mensagens e conteúdo no Instagram
  7. Gerenciar tudo na sua Página
- Clique em "Avançar"

> **Atenção, marque os 7.** Os 4 primeiros (com a palavra "Marketing") liberam a Marketing API que é o que permite puxar métricas e gerar relatórios. Os 3 últimos (Audience Network, Instagram, Página) liberam endpoints adicionais que skills futuras vão precisar (postagem programada no Instagram, leitura de página, monetização). Se faltar algum, depois precisa recriar o App, então marca todos agora.

**Etapa 3. Empresa**
- Selecione o Portfolio Empresarial (Business Manager) que contém a conta de anúncios que você quer monitorar
- Se não aparecer nenhuma opção, verifique se está logado com a conta de admin do BM
- Clique em "Avançar"

**Etapa 4. Requisitos**
- Nenhuma ação necessária nessa tela
- Clique em "Avançar"

**Etapa 5. Visão geral**
- Revise as informações do app
- Clique em "Criar Aplicativo"

**Após criar: adicionar política de privacidade e publicar**

1. No menu lateral do app, clique em "Configurações do App" > "Básico"
2. No campo "URL da Política de Privacidade", cole a URL da página de política de privacidade do negócio
3. A URL precisa ser real e acessível (não aceita placeholder). Se não tiver uma página de política pronta, pode usar o link da página de política do site existente, ou criar uma página simples no Notion, Google Sites ou similar
4. Clique em "Salvar alterações"
5. No menu lateral, clique em "Publicar"
6. Clique no botão "Publicar"

O app precisa estar publicado para que o token funcione corretamente.

### 4.2 Gerar token permanente via Usuário do Sistema

Token via Usuário do Sistema. Não expira. Não precisa renovar.

**Passo 4.2.1. Criar o Usuário do Sistema**

- Acesse business.facebook.com/latest/settings
- No menu lateral, em "Usuários", clique em "Usuários do sistema"
- No canto superior direito, clique em "Adicionar"
- Na tela que abrir:
  - Nomeie o usuário: use "relatorio-ads" (sem espaço, tudo minúsculo). O Facebook não aceita espaço nem maiúscula nesse campo
  - Em "System user role", selecione "Admin"
  - Clique em "Adicionar"

**Passo 4.2.2. Atribuir ativos ao Usuário do Sistema**

Com o usuário do sistema criado e selecionado, clique em "Atribuir Ativos". Uma tela vai abrir com menu lateral. Faça as atribuições abaixo na ordem:

**Contas de anúncio (a tela já abre aqui):**
- A tela abre diretamente em "Contas de anúncio"
- Selecione todas as contas que deseja monitorar
- Ative "Controle total" em cada uma
- Clique em "Atribuir ativos"

**Apps:**
- No menu lateral, clique em "Apps"
- Selecione o app criado ("Relatorio de Anuncios" ou o nome que usou)
- Ative "Controle total"
- Clique em "Atribuir ativos"

**Páginas (obrigatório se for criar ou analisar criativos):**
- No menu lateral, clique em "Páginas"
- Selecione a página do Facebook conectada à conta de anúncios
- Ative "Criar conteúdo" e "Anúncios"
- Clique em "Atribuir ativos"

**Contas do Instagram (se houver perfil comercial vinculado):**
- No menu lateral, clique em "Contas do Instagram"
- Selecione o perfil do Instagram vinculado à página
- Ative "Anúncios"
- Clique em "Atribuir ativos"

**Conjuntos de dados (Pixel e Conversions API):**
- No menu lateral, clique em "Conjuntos de dados" (antigo "Fontes de dados" ou "Pixels")
- Selecione o conjunto de dados do negócio (o Pixel principal vinculado à conta de anúncios)
- Ative "Gerenciar conjunto de dados" (controle total) ou no mínimo "Visualizar conjunto de dados" + "Enviar eventos"
- Clique em "Atribuir ativos"

> **Atenção, esses três últimos passos são os mais esquecidos da configuração.** Sem a Página atribuída, o token funciona em testes simples como `GET /me`, mas dá erro de permissão na hora de subir criativo, disparar relatório que cruza dados de página, ou puxar insights de Reels. Sem o Conjunto de dados, qualquer chamada que envolva eventos do Pixel ou Conversions API (envio de eventos server-side, leitura de qualidade de eventos, deduplicação) volta erro 200 de permissão. Se o anunciante não usa Instagram, o passo do Instagram pode ser pulado, mas Páginas e Conjuntos de dados são obrigatórios.

**Passo 4.2.3. Gerar o token**

- Ao lado do nome do usuário do sistema, clique em "Gerar token"
- Uma tela com 4 etapas vai abrir:

**Etapa 1. Selecionar app**
- Selecione o app criado ("Relatorio de Anuncios")
- Clique em "Avançar"

**Etapa 2. Definir expiração**
- Selecione "Nunca" (não selecione "60 dias" para evitar manutenção futura)
- Clique em "Avançar"

> **O que "Nunca" significa de verdade.** O token não expira por tempo, mas pode ser revogado pela Meta em alguns cenários: troca da senha do admin que criou o usuário do sistema, troca do segredo do app, mudanças nas permissões do Business Manager, ou inatividade prolongada (raro). Recomendação de higiene: gerar um token novo a cada 6 meses, mesmo sem aviso de erro. Se um teste de validação retornar erro 190 lá na frente, o caminho é repetir este passo, não recriar o usuário do sistema nem o app.

**Etapa 3. Atribuir permissões**

Marque TODOS os escopos que aparecerem na tela (selecionar tudo). O Facebook só mostra os escopos que são compatíveis com os casos de uso que foram selecionados na criação do App, então não tem risco de marcar algo que não deveria. Liberar tudo evita ter que voltar aqui depois para regerar o token quando uma skill nova precisar de um escopo que não foi marcado da primeira vez.

Para referência, os escopos principais que as skills do curso usam são:

| Escopo | Para que serve |
|---|---|
| `ads_management` | Criar e gerenciar campanhas, conjuntos e anúncios |
| `ads_read` | Ler dados de anúncios e métricas |
| `business_management` | Acesso ao Business Manager e ativos |
| `read_insights` | Buscar relatórios e insights de desempenho |
| `pages_read_engagement` | Dados de engajamento de páginas vinculadas |
| `pages_show_list` | Listar páginas vinculadas ao negócio |
| `catalog_management` | Gerenciar catálogos de produtos |
| `instagram_basic` | Ler dados básicos do perfil Instagram vinculado |
| `instagram_content_publish` | Publicar conteúdo no Instagram via API |

Não precisa identificar um por um. É só marcar a opção "Selecionar tudo" no topo da lista (se existir) ou marcar todos os checkboxes manualmente.

- Clique em "Gerar token"

**Etapa 4. Concluir**
- O token vai aparecer na tela
- Copie o token e guarde em um lugar seguro (ele não aparece novamente)
- Clique em "Concluir"

### 4.3 Descobrir o ID da conta de anúncios via API

**Não pedir o ID da conta manualmente ao aluno.** Com o token permanente já salvo no `.env` como `FB_ACCESS_TOKEN_PERMANENTE`, a skill descobre sozinha quais contas o token enxerga e oferece a lista pro aluno escolher. Pedir o ID manual é fricção desnecessária e contraria o princípio de auto-descoberta do curso.

🔍 Próximo passo: listar as contas de anúncios que seu token enxerga. Tempo estimado: cerca de 10 segundos.

Chamar a Graph API:

```
curl -s "https://graph.facebook.com/v25.0/me/adaccounts?fields=id,account_id,name,currency,timezone_name,account_status&limit=50&access_token=<TOKEN_DO_ENV>"
```

Onde `<TOKEN_DO_ENV>` é substituído pelo valor de `FB_ACCESS_TOKEN_PERMANENTE` lido inline do `.env` no momento da execução. Nunca exibir o token no chat — usar `$(grep ^FB_ACCESS_TOKEN_PERMANENTE= .env | cut -d= -f2-)` dentro do próprio curl.

**Tratamento do retorno:**

- **1 conta apenas:** salvar automaticamente como `FB_AD_ACCOUNT_ID` (só os dígitos, sem o prefixo `act_`) e seguir. Avisar em 1 linha: `✅ Conta identificada: {name} (act_{account_id}), em {currency}, fuso {timezone_name}. Salva no .env como conta padrão.`

- **2 ou mais contas:** mostrar tabela numerada com Nome, ID, Moeda, Fuso e Status, e perguntar qual usar como padrão:

  ```
  Contas de anúncios que seu token enxerga:

  | # | Nome              | ID                   | Moeda | Fuso              | Status |
  |---|-------------------|----------------------|-------|-------------------|--------|
  | 1 | Conta Principal    | act_1234567890123456 | BRL   | America/Sao_Paulo | ativa  |
  | 2 | Outra Conta       | act_9876543210987654 | BRL   | America/Sao_Paulo | ativa  |

  Qual conta você quer usar como padrão? Digite o número.
  ```

  Salvar o `account_id` da escolha (só os dígitos, sem `act_`) como `FB_AD_ACCOUNT_ID`. Salvar também a lista completa como `FB_AD_ACCOUNT_IDS` separada por vírgula sem espaço — útil pra skills futuras que cruzam várias contas.

- **Lista vazia:** o usuário do sistema não recebeu nenhuma conta de anúncios atribuída. Voltar ao Passo 4.2.2 e instruir o aluno a atribuir pelo menos uma Conta de anúncio com "Controle total" ao usuário do sistema. Não pedir ID manual como fallback.

- **Erro `190` (token inválido) ou `200` (sem permissão):** o token pode ter sido copiado errado ou faltam escopos. Voltar ao Passo 4.2.3 e regerar o token.

**Regra dura:** a descoberta via API é o caminho único. Se o token vê a conta, o ID está disponível. Se não vê, a correção é atribuir o ativo ao usuário do sistema, não digitar o ID manualmente. **A skill nunca pede ao aluno pra colar `FB_AD_ACCOUNT_ID`.**

---

## 5. Validação Final

### 5.1 Modo MCP_CONECTOR

🔍 Próximo passo: validar o MCP da Meta. Tempo estimado: cerca de 15 segundos.

Identifique a tool de listagem de contas de anúncio disponibilizada pelo MCP da Meta. **Não dependa do prefixo do nome.** O prefixo varia conforme o ambiente: pode ser `mcp__Meta_Ads__...`, mas também pode ser um identificador longo (UUID), por exemplo `mcp__a1b2c3d4-0000-0000-0000-000000000000__ads_get_ad_accounts`. O que é **estável é o sufixo** `ads_get_ad_accounts`. Estratégia de busca, em ordem:

1. **Procurar pelo sufixo, não pelo prefixo.** Localize qualquer tool cujo nome termine em `ads_get_ad_accounts` (ou, de forma mais ampla, qualquer tool com o trecho `__ads_` no nome). Em alguns ambientes as tools do MCP ficam "adormecidas" (deferred) e só aparecem depois de uma busca por nome; nesse caso, faça a busca pelo sufixo `ads_get_ad_accounts` para trazer a tool antes de chamá-la.
2. **Se a busca não for conclusiva**, perguntar ao aluno: *"Qual nome você deu ao MCP da Meta? Vou usar pra localizar a tool certa."*
3. Chamar a tool `ads_get_ad_accounts` encontrada (sem parâmetros obrigatórios; ela retorna as contas que o conector enxerga).

- **Se retornar uma lista de contas de anúncios:** conexão validada. Antes de seguir para a seção 6, **selecionar e salvar a conta padrão** conforme a seção 5.1.1 abaixo.
- **Se nenhuma tool com prefixo MCP relacionada ao Meta estiver disponível** (erro "tool not found" ou similar): o conector ainda não está ativo na conta. Avisar o aluno:

  ```
  Não consegui acessar nenhuma tool do MCP da Meta. Confirme:

  - Você está logado no Claude com a mesma conta onde adicionou o
    MCP personalizado?
  - No app do Claude Desktop, em Customize > Connectors, o MCP que você
    adicionou (ex: "Meta Ads") aparece como "Conectado" (verde)?
  - Você precisa reiniciar o Claude Desktop para o MCP recém-adicionado
    aparecer? (saia do app e abra de novo)

  Quando estiver tudo certo, me avisa que tento de novo.
  ```

  Aguardar e tentar de novo. Se o aluno desistir, oferecer trocar para o modo `APP` (voltar ao Passo 1).

- **Se a tool retornar erro de permissão:** o MCP está conectado mas o aluno não autorizou nenhuma conta de anúncios na hora do OAuth. Pedir para refazer o passo 6 da seção 3.1 no Facebook (o passo de seleção da Página e do perfil do Instagram).

### 5.1.1 Selecionar e salvar a conta padrão (modo MCP)

> **Regra dura.** As tools MCP de escrita (`ads_create_campaign`, `ads_create_ad_set`, `ads_create_ad`, `ads_create_custom_audience`, etc.) **exigem o parâmetro `ad_account_id`**. Por isso o modo MCP também precisa salvar a conta padrão no `.env`, exatamente como o caminho APP faz em 4.3. Sem isso, a skill seguinte (`/trafego-criar-campanha`) não sabe em qual conta operar.

A própria chamada de validação (`ads_get_ad_accounts`) já devolve a lista de contas. Use esse retorno, **não faça uma segunda chamada**. Para cada conta, leia (quando disponível) os campos `name`, `account_id`, `currency`, `timezone_name` e `is_ads_mcp_enabled`.

**Caso A. O conector enxerga 1 conta apenas.** Salvar automaticamente como `FB_AD_ACCOUNT_ID` (só os dígitos, sem o prefixo `act_`). Avisar em 1 linha:

```
✅ Conta identificada: {name} (act_{account_id}), em {currency}. Salva no .env como conta padrão.
```

**Caso B. O conector enxerga 2 ou mais contas.** Mostrar tabela numerada e perguntar a padrão. **Marcar na coluna "MCP" se a conta está habilitada para o conector** (`is_ads_mcp_enabled`): contas com `false` ainda não funcionam no MCP (rollout gradual da Meta) e não devem ser escolhidas como padrão.

```
Contas que o conector MCP enxerga:

| # | Nome           | ID                   | Moeda | MCP        |
|---|----------------|----------------------|-------|------------|
| 1 | Conta Principal | act_1234567890123456 | BRL   | habilitada |
| 2 | Conta Secundária  | act_9876543210987654  | BRL   | ainda não  |

Qual conta você quer usar como padrão? Digite o número.
(Evite contas marcadas como "ainda não" — elas não funcionam no MCP por enquanto.)
```

Se o aluno escolher uma conta marcada como "ainda não" (`is_ads_mcp_enabled:false`), avisar que ela ainda não funciona no MCP e pedir para escolher outra (ou trocar para o modo `APP`, que não tem essa limitação).

Salvar o `account_id` da escolha (só os dígitos, sem `act_`) como `FB_AD_ACCOUNT_ID`. Salvar também a lista completa das contas habilitadas como `FB_AD_ACCOUNT_IDS`, separada por vírgula sem espaço. Em seguida, seguir para a seção 6.

### 5.2 Modo APP

🔍 Próximo passo: validar o token permanente com 3 testes na Graph API. Tempo estimado: cerca de 20 segundos.

Leia `FB_ACCESS_TOKEN_PERMANENTE` e `FB_AD_ACCOUNT_ID` do `.env`. Rode os 3 testes abaixo.

> ### ⚙️ Como executar (regra dura para a skill)
>
> **Cada teste é uma chamada `Bash` independente.** Substituir `TOKEN` pelo valor literal **inline na URL** do `curl`. NÃO empacotar os 3 testes num script multi-linha com `TOKEN="..."` no início. Esse formato (script bash com variável shell) **não casa** com os padrões autorizados e dispara o pop-up nativo de permissão, que exibe o token completo na tela.
>
> Formato CORRETO (3 chamadas Bash independentes, cada uma um único `curl` com token inline):
>
> ```
> curl -s "https://graph.facebook.com/v25.0/me?access_token=<TOKEN_DO_ENV>"
> ```
> ```
> curl -s "https://graph.facebook.com/v25.0/me/adaccounts?access_token=<TOKEN_DO_ENV>"
> ```
> ```
> curl -s "https://graph.facebook.com/v25.0/act_<id>/campaigns?limit=1&access_token=<TOKEN_DO_ENV>"
> ```
>
> Após cada chamada, mostrar a resposta resumida ao aluno (sucesso/erro). Não ecoar a URL completa com o token na resposta. Descrever em linguagem natural: "Teste 1 passou: token responde como `relatorio-ads` em /me".

**Teste 1. Token está válido**

```bash
curl "https://graph.facebook.com/v25.0/me?access_token=TOKEN"
```

Esperado: `{"id":"...","name":"relatorio-ads"}` (ou o nome que deu ao usuário do sistema). Se vier erro, o token foi copiado errado ou já está revogado.

**Teste 2. Usuário do sistema enxerga a conta de anúncios**

```bash
curl "https://graph.facebook.com/v25.0/me/adaccounts?access_token=TOKEN"
```

Esperado: lista contendo `act_<seu_ad_account_id>`. Se vier vazio ou sem a conta esperada, a atribuição da conta no Passo 4.2.2 não foi feita corretamente, refaça aquele passo.

**Teste 3. Permissão de leitura na conta funciona de verdade**

```bash
curl "https://graph.facebook.com/v25.0/act_SEU_AD_ACCOUNT_ID/campaigns?limit=1&access_token=TOKEN"
```

Esperado: um objeto `data` com 1 campanha (se a conta tiver), ou `data: []` (se a conta for nova). Em ambos os casos, sem mensagem de erro.

Os três passaram? Token validado, seguir para a seção 6.

### 5.3 Mapa de erros comuns (modo APP)

| Código | Causa provável | Solução |
|---|---|---|
| `190 — Invalid OAuth access token` | Token errado, copiado parcialmente, ou já revogado | Voltar a 4.2.3 e gerar de novo. Tokens da Meta têm 200+ caracteres, conferir se copiou o token inteiro |
| `200 — Permissions error` | Token válido, mas o usuário do sistema não tem o ativo atribuído | Voltar a 4.2.2 e confirmar as permissões certas em cada bloco |
| `100 — Invalid parameter` | Prefixo `act_` no lugar errado | No `.env`, salvar só os números. Na URL do curl, prefixar com `act_` |
| `10 — Application does not have permission` | App sem o caso de uso "Marketing API" ou usuário do sistema sem o app atribuído | Voltar a 4.1 (confirmar caso de uso) e a 4.2.2 (confirmar app com Controle total) |
| `4 — Application request limit reached` | Rate limit do app | Aguardar 1 hora. Se persistir, publicar o app (precisa da política de privacidade configurada) |
| `17 — User request limit reached` | Muitas chamadas em pouco tempo com esse token | Aguardar e implementar pausa entre chamadas. Não regerar o token |
| `appsecret_proof` exigido | App Secret Proof ativado nas Configurações Avançadas | Para teste manual, desativar temporariamente em Configurações > Avançado, fazer os testes, religar |

### 5.4 Modo HIBRIDO

🔍 Próximo passo: validar os dois caminhos do modo híbrido. Tempo estimado: cerca de 30 segundos.

No `HIBRIDO`, os dois precisam funcionar: o MCP (principal) e o token (reserva). Validar nesta ordem:

1. **MCP**, conforme 5.1 (chamar `ads_get_ad_accounts` e confirmar que retorna contas).
2. **Token**, conforme 5.2 (os 3 testes na Graph API).

- Se **os dois** passarem: modo híbrido validado, seguir para 6.4.
- Se **só o MCP** passar e o token falhar: avisar que a reserva (App) não está funcionando e oferecer regerar o token (4.2.3). O MCP segue utilizável pro dia a dia, mas as 4 lacunas ficam indisponíveis até a reserva voltar.
- Se **só o token** passar e o MCP falhar: o conector caiu. Como o token faz tudo, oferecer rebaixar pra `APP` puro (a operação não fica bloqueada), ou reconectar o MCP (seção 3) pra manter o híbrido.

---

## 6. Salvamento no `.env`

Após validação passar, salvar as variáveis abaixo no `.env` usando `Edit` cirúrgico (atualizar a linha existente ou adicionar nova). Não sobrescrever outras variáveis.

### 6.1 Modo MCP_CONECTOR

```
META_AUTH_MODO=MCP_CONECTOR
FB_AD_ACCOUNT_ID={id_da_conta_default}
FB_AD_ACCOUNT_IDS={id_1},{id_2},{id_3}
```

- `META_AUTH_MODO=MCP_CONECTOR` registra o modo.
- `FB_AD_ACCOUNT_ID` e `FB_AD_ACCOUNT_IDS` vêm da seleção feita em 5.1.1 (apenas dígitos, sem o prefixo `act_`; lista separada por vírgula sem espaço). São obrigatórios porque as tools MCP de escrita exigem `ad_account_id`.
- O modo MCP **não salva token**: a autenticação fica na conta Anthropic, a skill nunca vê o token.

### 6.2 Modo APP

```
META_AUTH_MODO=APP
FB_ACCESS_TOKEN_PERMANENTE={token}
FB_AD_ACCOUNT_ID={id}
```

### 6.3 Multi-conta (modo APP)

Logo após salvar o token e antes da confirmação final, **sempre listar todas as contas que o token enxerga**, sem perguntar:

```bash
curl -s "https://graph.facebook.com/v25.0/me/adaccounts?fields=id,account_id,name,account_status,currency&limit=100&access_token=TOKEN"
```

**Mapeamento de status (`account_status`):**

| Valor | Significado |
|---|---|
| 1 | Ativa |
| 2 | Desabilitada |
| 3 | Sem conformidade |
| 7 | Pendente de risco |
| 9 | Em revisão |
| 100 | Pendente de fechamento |
| 101 | Fechada |
| 201 | Outro motivo de inatividade |

**Caso A. Token retorna 1 conta.** Salvar direto, sem perguntar. Avisar o aluno: "Conta única detectada: {nome} ({id}). Salva como padrão."

**Caso B. Token retorna 2 ou mais contas.** Mostrar tabela com `#`, `Nome`, `ID`, `Moeda`, `Status` e perguntar:

```
Quais contas quer salvar no projeto? Digite os números separados por
vírgula (ex: 1,3,5) ou "todas" para salvar todas.
```

Depois:

```
Qual delas é a padrão? Será usada nas chamadas automáticas quando nenhuma
for especificada. Digite o número:
```

Salvar:

```
FB_AD_ACCOUNT_ID={id_da_conta_default}
FB_AD_ACCOUNT_IDS={id_1},{id_2},{id_3}
```

Regras de formato:
- Apenas números, sem o prefixo `act_`.
- `FB_AD_ACCOUNT_IDS` separado por vírgula sem espaço.
- O `FB_AD_ACCOUNT_ID` (padrão) precisa aparecer também dentro de `FB_AD_ACCOUNT_IDS`.

### 6.4 Modo HIBRIDO

Gravado **apenas** pelo protocolo de escalada (aluno no MCP que configurou o App como reserva, escolhendo a opção 1 em 4.0). Salvar:

```
META_AUTH_MODO=HIBRIDO
FB_ACCESS_TOKEN_PERMANENTE={token}
FB_AD_ACCOUNT_ID={id}
FB_AD_ACCOUNT_IDS={id_1},{id_2},{id_3}
```

- `META_AUTH_MODO=HIBRIDO` diz às skills: usar MCP em tudo, token só nas 4 lacunas.
- O token e os IDs vêm da configuração do App (4.2/4.3). As mesmas regras de formato da seção 6.3 valem.
- Se o `FB_AD_ACCOUNT_ID` já tinha sido salvo pelo MCP (5.1.1), manter o valor; não sobrescrever sem necessidade.

---

## 7. Saída final

Mostrar ao aluno:

```
✅ Conexão com Meta Ads configurada.

Modo ativo: {MCP | App | MCP com App de reserva}

Variável salva no .env: META_AUTH_MODO={MCP_CONECTOR | APP | HIBRIDO}

A próxima skill do curso (/trafego-criar-campanha) vai ler essa preferência
e usar o caminho certo automaticamente. Você não precisa configurar de novo.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️  Antes de subir sua primeira campanha, confirme que o
    pixel do Facebook está instalado e disparando evento no
    seu site. A próxima skill (/trafego-criar-campanha) exige
    pixel ativo para campanhas de venda direta ou captação.

    Se você ainda não instalou o pixel na sua página, abra
    o tutorial em HTML do Bônus 3 do curso antes de prosseguir.

    📂 Caminho do arquivo (clique duas vezes no Finder ou Explorer
       para abrir no navegador):
       docs/tutoriais/bonus-3-pixel-instalacao.html

    Cobre 7 plataformas: Hotmart, Kiwify, Cartpanda, WordPress,
    Hotmart Pages, Elementor, Lovable + bloco genérico para HTML
    direto (Claude Code, Vercel, etc.).
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔭 Próximo passo recomendado: /trafego-criar-campanha
Conta conectada e pixel ativo. Suba sua primeira campanha
(venda direta ou captação de leads).
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Para trocar o modo no futuro, rode /trafego-conexao de novo.
```

> **Regra dura, não expandir esta saída.** Não acrescentar lista de "Próximas skills disponíveis" nem citar outras skills. O curso só usa `/trafego-conexao` e `/trafego-criar-campanha`. Encerra com a confirmação acima e ponto.

---

## 8. Como o command deve usar esta especificação

O command `/trafego-conexao` é o orquestrador. Ele:

1. Lê `META_AUTH_MODO` do `.env`.
2. Conduz a pergunta de modo (Passo 1 desta skill). O menu mostra só MCP e App; o `HIBRIDO` nunca aparece como opção.
3. Para o caminho escolhido, segue a seção correspondente (3 para MCP, 4 para APP). No caminho do App, o passo 4.0 decide se o destino é `APP` puro ou `HIBRIDO` (quando o MCP já está ativo ou o aluno chegou pelo protocolo de escalada).
4. Aplica a validação (seção 5): 5.1 para MCP, 5.2 para APP, 5.4 para HIBRIDO (valida os dois).
5. Salva no `.env` (seção 6): 6.1 MCP, 6.2 APP, 6.4 HIBRIDO.
6. Mostra a saída final (seção 7).

A skill é idempotente, pode ser chamada várias vezes sem efeito colateral.

---

## 9. Princípios que esta skill nunca viola

1. **Nunca salvar `META_AUTH_MODO` antes da validação passar.** Se o conector ou o token falham na hora de validar, a variável não entra no `.env`. Evita estado inconsistente em que a skill diz "conectado" mas a outra skill do curso falha.
2. **Nunca pular a pergunta de modo na primeira execução.** Mesmo que o aluno já tenha `FB_ACCESS_TOKEN_PERMANENTE` no `.env` por ter rodado o caminho técnico antes, perguntar e deixar ele escolher conscientemente.
3. **Nunca pedir token completo no chat no caminho MCP.** Token e auth ficam todos na conta Anthropic, a skill nem vê.
4. **Nunca recomendar o caminho do App sem aviso.** Sempre apresentar o conector MCP como recomendado primeiro, deixar o aluno escolher consciente.
5. **Sempre validar antes de declarar conexão pronta.** Para MCP, chamar uma tool de leitura. Para APP, rodar os 3 testes da Graph API. Para HIBRIDO, validar os dois (MCP e token), conforme 5.4.
6. **Nunca exibir o token no chat.** Mesmo em logs, mensagens de confirmação ou comandos mostrados ao aluno, o valor real do token jamais aparece. Usar `***TOKEN_MASCARADO***` ou apenas confirmar com "salvo".
7. **Nunca usar `python3 << 'EOF'` (heredoc) nem `curl | python3 -c` com o token.** Esses formatos expõem o token no pop-up nativo do Claude Code. Cada chamada `curl` é uma `Bash` independente com o token inline.
8. **No modo MCP puro, nunca assumir que o token existe.** Se uma operação exige token (uma das 4 lacunas), seguir o protocolo de escalada: parar, oferecer o caminho manual ou a ativação do App. Jamais montar um `curl` com token no modo `MCP_CONECTOR` sem antes confirmar a presença de `FB_ACCESS_TOKEN_PERMANENTE` (o que, na prática, só acontece em `HIBRIDO` ou `APP`).
