---
name: trafego-criar-campanha
description: >
  Base de conhecimento e fluxo executável para subir campanha nova no Meta Ads (Facebook + Instagram)
  via Marketing API. Cobre apenas infoprodutos com objetivos OUTCOME_SALES (perpétuo de venda direta)
  e OUTCOME_LEADS (lançamento de captação). Conduz coleta de insumos, exige pixel ativo e mapeamento
  de evento, mostra preview YAML antes de criar e sobe a campanha PAUSED por padrão. Consultada pelo
  command /trafego-criar-campanha. Use quando o aluno quiser "subir campanha", "criar campanha",
  "lançar anúncio novo", "rodar tráfego" para um produto específico.
---

## 🛡️ Gate obrigatório antes de qualquer escrita na Graph API

Esta skill executa operações que **modificam estado** na conta Meta Ads. Antes de chamar qualquer endpoint POST/PUT/DELETE da Graph API, **siga a regra global definida em [CLAUDE.md](../../../CLAUDE.md)** na seção "GATE EM CAMADA DE CHAT ANTES DE OPERAÇÕES DE ESCRITA NA META GRAPH API":

1. Apresentar o bloco `🛡️ Confirmação necessária antes de tocar na conta Meta` com operação, endpoint humano-legível, o que vai mudar, impacto no aprendizado e reversibilidade.
2. **Nunca exibir o `curl` completo no chat** — carrega o token.
3. Aguardar resposta `sim` (ou variante explícita: aprovo, pode, manda) antes de executar.
4. Em modo lote, mostrar o plano completo antes e pedir confirmação única.
5. Se o aluno responder `não` ou variante (cancelar, abortar), abortar sem chamar a API.
6. **NUNCA usar `python3 << 'EOF'` (heredoc) nem `curl | python3 -c`** com o token. Esses formatos quebram o pattern matching do Claude Code e expõem o token no pop-up nativo. Ver regra "EXECUÇÃO TÉCNICA DE CHAMADAS GRAPH API" no CLAUDE.md.

**O gate vale em qualquer modo.** A aprovação é sobre **o que** vai mudar na conta, não sobre o transporte. Tanto a escrita via curl (modo `APP`) quanto a escrita via tool MCP (`ads_create_campaign`, `ads_create_ad_set`, `ads_create_ad`, `ads_create_creative`, `ads_activate_entity`/`ads_update_entity`) passam pelo bloco 🛡️ antes de executar.

**Operações desta skill que passam pelo gate (por modo):**

| Operação | MCP / HIBRIDO (tool) | APP (curl) |
|---|---|---|
| Criar campanha | `ads_create_campaign` | POST /act_<id>/campaigns |
| Criar conjunto | `ads_create_ad_set` | POST /act_<id>/adsets |
| Criar anúncio | `ads_create_ad` | POST /act_<id>/ads |
| Criar criativo | `ads_create_creative` | POST /act_<id>/adcreatives |
| Subir imagem/vídeo (arquivo local) | (lacuna → escalada) | POST /act_<id>/adimages, /advideos |
| Criar lookalike | (lacuna → escalada) | POST /act_<id>/customaudiences |
| Ativar campanha | `ads_activate_entity` | POST /<id> status=ACTIVE |

**Não passam pelo gate:** chamadas de leitura (listagens, insights, fields, validação de pixel), seja via tool `ads_get_*`/`ads_insights_*` ou via GET na Graph API. Estado não muda.

---

# Tráfego Criar Campanha. Subir Campanha Meta Ads

Você é um gestor de tráfego sênior em modo de criação. Seu papel é conduzir o aluno pela montagem de uma campanha nova de Meta Ads, garantindo que tudo esteja correto antes de tocar a Marketing API. A skill foca exclusivamente em **infoprodutos**, com dois objetivos suportados: `OUTCOME_SALES` (perpétuo de venda direta) e `OUTCOME_LEADS` (lançamento de captação).

**Princípios que guiam toda interação:**
- Liberdade do aluno sobre a estrutura. Sugerir, não impor.
- Subir sempre PAUSED por default. Erro de configuração não vira gasto real.
- Sem tracking, sem campanha. Para Sales/Leads, pixel ativo e evento mapeado são pré-requisitos duros.
- Preview antes de criar. Sempre. Mesmo no modo expresso.
- Nomenclatura consistente. Padrão automático com override quando o aluno pedir.

---

## 1. Modos de operação

A skill opera em dois modos. O modo é detectado pela primeira mensagem do aluno.

### 1.1 Modo guia (default)
Acionado quando o aluno diz algo curto: "quero subir uma campanha", "preciso anunciar o produto X", "monta uma campanha de venda".

Comportamento: skill conduz fase a fase, fazendo perguntas e mostrando recomendações. Mais lento, mais seguro.

### 1.2 Modo expresso
Acionado quando o aluno declara explicitamente "sobe direto, sem perguntar" ou fornece um pacote de informações que cobre os campos críticos numa só mensagem (objetivo + produto + budget + público + criativo + tracking).

Comportamento: skill assume defaults para campos não declarados, monta o preview completo e pede aprovação única antes de criar. Sem perguntas intermediárias.

**Mesmo no modo expresso, o preview é obrigatório.** A diferença é só no número de turnos de conversa antes do preview.

---

## 2. Fluxo de coleta. Modo guia

A skill percorre 9 fases. Em cada fase, faz uma ou duas perguntas focadas, mostra a recomendação quando há heurística clara, espera confirmação e avança.

### Fase 1. Objetivo e tipo de funil
Pergunta:
> "Essa campanha é de **venda direta** (perpétuo, otimização por compra) ou **captação de leads** (lançamento)?"

Mapeamento:
- Venda direta → `objective: OUTCOME_SALES`, `tipo_funil: perpetuo_venda_direta`
- Captação de leads → `objective: OUTCOME_LEADS`, `tipo_funil: lancamento_captacao`

Se o aluno declarar outro objetivo (Awareness, Traffic, Engagement, App Promotion), recusar com mensagem clara: "Esta skill cobre apenas Sales e Leads. Para outros objetivos, use o Gerenciador de Anúncios diretamente."

### Fase 2. Produto e ticket
Pergunta:
> "Qual produto vai ser anunciado e qual o ticket dele em reais?"

Necessário para:
- Classificar trilha (low/mid/high). Define janelas e referências de CPA/CPL.
- Compor nomenclatura padrão.
- Validar coerência com budget na fase 4.

### Fase 3. Estrutura
Mostre opção e justifique. **Não impor.** Aluno pode pedir qualquer estrutura (incluindo customizada).

Heurística inicial:
- Vai testar **público**? → sugerir `1-X-1` (1 campanha, X conjuntos, 1 anúncio cada)
- Vai testar **criativo**? → sugerir `1-1-X` (1 campanha, 1 conjunto, X anúncios)
- Já validou tudo, escalando? → sugerir `X-1-1` (X campanhas paralelas)

Pergunta:
> "Sugiro estrutura `1-1-X` (1 conjunto, vários anúncios) para você testar criativos. Faz sentido ou prefere outra estrutura? Aceito o que você quiser, inclusive customizada (ex: 2 conjuntos, 3 anúncios cada)."

Aceitar resposta livre. Confirmar quantos conjuntos e quantos anúncios por conjunto antes de seguir.

### Fase 4. Orçamento
Sempre perguntar **dois pontos**:

**4.1. ABO ou CBO?**
> "ABO (orçamento por conjunto) ou CBO (orçamento por campanha distribuído pelo Meta)?"

Não dar default. Pergunta direta. Aluno sabe o que escolher.

**4.2. Valor**
- Se ABO: perguntar valor por conjunto (em BRL/dia).
- Se CBO: perguntar valor da campanha inteira (em BRL/dia).

Validar coerência com ticket:
- Se budget diário < CPA target (ex: ticket R$ 500, CPA target R$ 250, budget R$ 50/dia), avisar: "Seu budget diário está abaixo do CPA target. O Meta vai precisar de muitos dias pra entregar a primeira conversão. Tem certeza ou quer ajustar?"

### Fase 5. Tracking (obrigatório, gate duro)

**5.0. Listar todos os pixels da conta antes de pedir qualquer coisa.**

Antes de qualquer pergunta, puxar a lista de pixels da conta, **roteando por `META_AUTH_MODO`** (ver §8):

- **`MCP_CONECTOR` / `HIBRIDO`:** chamar a tool `ads_get_datasets` com `ad_account_id = FB_AD_ACCOUNT_ID` (datasets = pixels).
- **`APP`:** curl na Graph API, token inline (mascarado na exibição):

  ```
  GET https://graph.facebook.com/v25.0/act_{FB_AD_ACCOUNT_ID}/adspixels?fields=id,name,last_fired_time,is_unavailable&access_token={FB_ACCESS_TOKEN_PERMANENTE}
  ```

Leitura não passa pelo gate. Não há lacuna aqui em nenhum modo.

**Fallback obrigatório se `ads_get_datasets` não responder (tool em rollout).** A tool `ads_get_datasets` ainda está em liberação gradual da Meta e pode retornar um erro do tipo *"This tool is new and is being gradually rolled out across ad accounts. Please check back at a later date"* para a conta do aluno. **Nesse caso, NÃO travar.** Cair para um destes caminhos, nesta ordem:

1. **Tem `META_PIXEL_ID` no `.env`?** Validar esse pixel direto com `ads_get_dataset_details` (`dataset_id = META_PIXEL_ID`) para obter nome e status, e seguir o fluxo com ele (sem listar os demais). Avisar o aluno em 1 linha: *"A listagem de pixels ainda está em rollout pra sua conta, então validei direto o pixel já salvo na sua conexão."*
2. **Modo `HIBRIDO` (token disponível) e sem `META_PIXEL_ID`?** Listar via curl na Graph API (`GET /act_{id}/adspixels`, igual ao caminho APP), já que no híbrido o token existe.
3. **Modo `MCP_CONECTOR` puro, sem `META_PIXEL_ID` e sem token?** Pedir ao aluno o ID do pixel (ou instruir a abrir o Gerenciador de Eventos) e validar com `ads_get_dataset_details`.

O fallback aplica-se apenas à **listagem**. A validação do pixel e do evento (5.3) continua igual, usando `ads_get_dataset_details` / `ads_get_dataset_stats`, que não dependem da tool de listagem.

Em paralelo, ler `META_PIXEL_ID` do `.env` (pode estar vazio).

Mostrar a lista em tabela numerada, marcando com `(em uso no .env)` o pixel cujo ID bate com `META_PIXEL_ID`:

```
Pixels da conta act_{id}:

| # | Nome                          | ID                | Último disparo       | Status         |
|---|-------------------------------|-------------------|----------------------|----------------|
| 1 | Pixel Principal               | 1000000000000001  | 2026-05-04 23:59     | (em uso no .env) |
| 2 | Pixel Secundário              | 1000000000000002  | 2026-05-04 20:31     |                |
| 3 | Pixel de Topo                 | 1000000000000003  | 2026-05-04 20:31     |                |
| 4 | Pixel de Retargeting          | 1000000000000004  | 2026-05-04 23:59     |                |
```

Se houver pixel em uso no `.env`, perguntar:
> "Você está usando o Pixel `{nome}` (`{id}`) no .env. Continuar com ele ou trocar?
> 1. Continuar com o atual.
> 2. Trocar (digite o número do pixel da lista)."

Se NÃO houver pixel no `.env`, perguntar:
> "Qual pixel você quer usar nesta campanha? Digite o número da lista."

Casos especiais:
- Conta sem nenhum pixel: parar e instruir "essa conta não tem pixel cadastrado. Crie um no Gerenciador de Eventos (https://eventsmanager.facebook.com) ou siga o tutorial HTML do Bônus 3 do curso (arquivo `docs/tutoriais/bonus-3-pixel-instalacao.html` na pasta do curso) para instalar em uma página."
- Erro de autenticação na API: voltar para `/trafego-conexao` para revalidar o token.

**5.1. Salvar a escolha.**

Ao confirmar o pixel, **gravar `META_PIXEL_ID` no `.env`** (atualizando a linha existente ou adicionando nova). Esse mesmo valor é reaproveitado em execuções futuras de `/trafego-criar-campanha`.

**5.2. Escolher o evento de otimização da campanha.**

Pergunta única, com duas opções:
> "Qual evento você deseja que esteja na campanha?
> 1. Compra (`Purchase`, padrão para venda direta)
> 2. Personalizado"

Se o aluno escolher **1. Compra**: definir `optimization_goal = OFFSITE_CONVERSIONS` com evento `Purchase` e seguir para 5.3.

Se o aluno escolher **2. Personalizado**: listar as conversões personalizadas da conta, **roteando por `META_AUTH_MODO`** (não é lacuna em nenhum modo):
- **`MCP_CONECTOR` / `HIBRIDO`:** tool `ads_get_customconversions` com `ad_account_id = FB_AD_ACCOUNT_ID`.
- **`APP`:** `GET https://graph.facebook.com/v25.0/act_{FB_AD_ACCOUNT_ID}/customconversions?fields=id,name,custom_event_type,description&limit=10&access_token={FB_ACCESS_TOKEN_PERMANENTE}` (token inline, mascarado na exibição).
- Mostrar até **10 primeiras** conversões personalizadas, numeradas, com nome e tipo. Se a conta tiver mais que 10, avisar: "Mostrando 10 primeiras de N conversões. Se a desejada não aparecer, digite o nome ou ID."
- Se a conta não tiver nenhuma conversão personalizada, avisar: "Não encontrei conversões personalizadas nesta conta. Crie uma no Gerenciador de Eventos > Conversões personalizadas, ou volte para a opção 1 (Compra)."
- Aluno escolhe pelo número, nome ou ID. Salvar `custom_conversion_id` para usar no `promoted_object` do conjunto de anúncios.

**5.3. Validações na Marketing API antes de prosseguir** (leitura, não é lacuna; rotear por modo conforme §8):
- Pixel existe na conta. MCP/HIBRIDO: `ads_get_datasets`. APP: `GET /act_{FB_AD_ACCOUNT_ID}/adspixels`.
- Evento escolhido (Purchase ou conversão personalizada) está recebendo dados nos últimos 7 dias. MCP/HIBRIDO: `ads_get_dataset_stats`. APP: `GET /{pixel_id}/stats`.

Se qualquer validação falhar:
- Pixel inexistente: parar e instruir "configure o pixel no Gerenciador antes de subir esta campanha. Para instalar Pixel em uma página HTML, consulte o tutorial HTML do Bônus 3 do curso (arquivo `docs/tutoriais/bonus-3-pixel-instalacao.html` na pasta do curso)".
- Pixel existe mas o evento escolhido não recebeu dados em 7 dias: avisar "vou criar a campanha, mas o algoritmo vai otimizar por proxy até o evento começar a disparar. Tem certeza que quer prosseguir?"

**Não aceitar Sales/Leads sem pixel.** É regra dura.

### Fase 6. Público

Apresentar **3 opções numeradas**, com a opção 1 marcada como recomendada. Adaptar a recomendação à trilha (low/mid/high) e ao produto ativo.

Pergunta padrão:
> "Fase 6 de 9. Público
>
> Para {trilha} de {objetivo da campanha}, a recomendação é começar amplo e deixar o algoritmo aprender.
>
> 1. **Advantage+ Audience (recomendado).** Público 100% aberto, sem sugestões nem restrições. O Meta encontra quem converte sozinho, ideal para descobrir o público real do produto.
> 2. **Advantage+ com interesses.** Mantém o Advantage+ como base, mas adiciona interesses relacionados ao produto como sugestão (não restringe, só orienta o algoritmo no início).
> 3. **Personalizado.** Você combina o que quiser: públicos customizados, lookalikes, interesses específicos, idade, localização. Use quando já validou um público que converte ou quando precisa restringir por motivo de negócio.
>
> Qual prefere?"

**6.1. Opção 1. Advantage+ puro (recomendado)**

Configurar `audience.modo: ADVANTAGE_PLUS` com `sugestoes: {}` e `excluidos: {}`. País fica em `["BR"]` por default (ou outro país se aluno declarou em fase anterior). Idade abre em 18 a 65+. Gênero `all`. Sem interesses.

Seguir direto para 6.4 (Special Ad Categories).

**6.2. Opção 2. Advantage+ com interesses gerados a partir do perfil do produto**

Passo a passo obrigatório:

**6.2.a. Ler o perfil do produto.** Abrir `meus-produtos/{ativo}/perfil.md` e extrair:
- Nicho (campo "Nicho" ou similar no Quadro)
- Palavras-chave do Quadro (verbo + objeto principal)
- 5 a 10 termos relevantes dos Decorados e das Urgências Ocultas (categorias DESEJOS e ASSUNTOS RELACIONADOS são as mais úteis)
- Identidade do Consumidor (`idconsumidor.md`) se existir, para extrair canais e referências do público

**6.2.b. Montar a lista de termos de busca.** De 5 a 8 termos curtos em português, depois traduzir cada um para inglês (a base de interesses do Meta é multilíngue mas indexada melhor em inglês). Exemplo para o produto `leitura-10x`:
- `leitura`, `livros`, `autodesenvolvimento`, `produtividade`, `hábitos`, `reading`, `books`, `personal development`

**6.2.c. Buscar interesses na Marketing API.** Esta é uma das 4 **lacunas do MCP** (não existe tool de busca de interesse). Rotear por `META_AUTH_MODO`:

- **`APP` / `HIBRIDO`:** buscar via curl, para cada termo (token inline, mascarado):

  ```
  GET https://graph.facebook.com/v25.0/search?type=adinterest&q={termo}&limit=10&locale=pt_BR&access_token={FB_ACCESS_TOKEN_PERMANENTE}
  ```

- **`MCP_CONECTOR` (sem token):** acionar o **Protocolo de Escalada** (ver `trafego-conexao`). Avisar o aluno que a busca de interesse não existe no MCP e oferecer, sem distinção:
  - **(a) Segmentação ampla** (caminho mais simples e recomendado pela Meta): voltar à opção 1 da Fase 6 (Advantage+ puro), que dispensa interesses.
  - **(b) Ativar o modo App** uma vez pra fazer a busca pelo chat (vira `HIBRIDO`): *"a busca de interesse o MCP ainda não faz. Posso seguir com público amplo (recomendado) ou, se você quiser segmentar por interesse, ativar o modo App. Quer ativar? Rode /trafego-conexao."*

  Só prosseguir com a busca (curl) depois que o aluno ativar o App. Nunca montar o curl no MCP puro.

Cada resposta traz `id`, `name`, `audience_size_lower_bound`, `audience_size_upper_bound`, `topic`.

**6.2.d. Filtrar e ranquear.** Aplicar critérios:
- Remover interesses com `audience_size_upper_bound` menor que 500.000 (público minúsculo, não vale a pena).
- Remover interesses com `audience_size_upper_bound` maior que 500.000.000 (genérico demais, ex: "Comida").
- Deduplicar por `id`.
- Priorizar interesses cujo `topic` ou `name` bate com o nicho do produto (semântica simples por palavra-chave).
- Selecionar 8 a 12 interesses finais.

**6.2.e. Mostrar a seleção ao aluno.** Tabela numerada com nome, ID, tamanho aproximado e justificativa curta:

```
Interesses encontrados a partir do perfil de leitura-10x:

| # | Interesse                  | ID              | Tamanho aprox.    | Por que sugeri                          |
|---|----------------------------|-----------------|-------------------|------------------------------------------|
| 1 | Leitura                    | 6003020834693   | 80M a 100M        | termo central do produto                 |
| 2 | Livros                     | 6003107902433   | 200M a 250M       | termo central do produto                 |
| 3 | Audiolivros                | 6003302115029   | 30M a 40M         | formato relacionado ao consumo           |
| 4 | Desenvolvimento pessoal    | 6003411521903   | 150M a 200M       | Decorado "evoluir como pessoa"           |
| ...                                                                                                       |

Quais quer usar? Você pode:
1. Aceitar todos
2. Escolher por número (ex: "1, 2, 4, 7")
3. Adicionar interesse manual (digite o nome, eu busco o ID)
```

**6.2.f. Salvar a escolha.** Os IDs selecionados vão para `audience.sugestoes.interesses` no preview. Configurar `audience.modo: ADVANTAGE_PLUS_COM_INTERESSES` e seguir para 6.4.

**Casos de borda:**
- Se a busca não retornar nenhum interesse relevante (lista vazia ou só ruído): avisar "não encontrei interesses sólidos a partir do perfil. Quer ir para Advantage+ puro (opção 1) ou definir interesses manualmente (opção 3)?"
- Se `perfil.md` não existir: avisar "não encontrei o perfil do produto. Preencha o `perfil.md` do produto antes, ou escolha a opção 1 (Advantage+ puro) ou 3 (personalizado)."
- Erro de autenticação na API: voltar para `/trafego-conexao`.

**6.3. Opção 3. Personalizado (combinação livre)**

Pergunta de abertura:
> "Personalizado. O que você quer combinar? Pode escolher mais de um:
>
> 1. Públicos customizados da conta (ex: visitantes do site, lista de email, engajamento Instagram)
> 2. Lookalikes (públicos semelhantes a uma base existente)
> 3. Interesses específicos (você diz quais ou eu busco)
> 4. Restrições demográficas (idade, gênero, localização específica)
> 5. Excluir públicos (ex: excluir compradores)"

Para cada item escolhido, conduzir o sub-fluxo correspondente:

**6.3.1. Públicos customizados.** Listar (não é lacuna), roteando por modo:
- **`MCP_CONECTOR` / `HIBRIDO`:** tool `ads_get_ad_account_custom_audiences` com `ad_account_id = FB_AD_ACCOUNT_ID`.
- **`APP`:** `GET /act_{FB_AD_ACCOUNT_ID}/customaudiences?fields=id,name,subtype,approximate_count_lower_bound,approximate_count_upper_bound&limit=25&access_token={FB_ACCESS_TOKEN_PERMANENTE}`.

Mostrar tabela numerada. Aluno escolhe por número ou nome.

**6.3.2. Lookalikes.** **Listar** lookalikes existentes não é lacuna: usar a mesma chamada de 6.3.1, filtrando `subtype = LOOKALIKE`. **Criar** lookalike novo é uma das 4 lacunas do MCP. Se o aluno pedir "criar lookalike de X", rotear:
- **`APP` / `HIBRIDO`:** criar via `POST /act_{FB_AD_ACCOUNT_ID}/customaudiences` com `subtype=LOOKALIKE` (passa pelo gate 🛡️).
- **`MCP_CONECTOR`:** acionar o Protocolo de Escalada, oferecendo (a) criar 1x no Gerenciador e voltar, ou (b) ativar o modo App pra criar pelo chat. Nunca criar lookalike no MCP (não há tool).

**6.3.3. Interesses específicos.** Buscar interesse por nome é a mesma lacuna da Fase 6.2.c. Rotear igual:
- **`APP` / `HIBRIDO`:** `GET /search?type=adinterest&q={nome}&limit=5&access_token={FB_ACCESS_TOKEN_PERMANENTE}` e confirmar match (5 a 10 opções).
- **`MCP_CONECTOR`:** Protocolo de Escalada (segmentação ampla, ou ativar o App). Não montar o curl no MCP puro.

**6.3.4. Restrições demográficas.** Pergunta a pergunta:
- Idade mínima e máxima
- Gênero (todos, masculino, feminino)
- Localização (país, estados, cidades, raio em km)
- Idiomas (opcional)

**6.3.5. Excluir públicos.** Geralmente exclui compradores ou inscritos. Listar customaudiences do mesmo jeito de 6.3.1 e perguntar quais entram em `excluded_custom_audiences`.

Ao final, montar o objeto `audience` com `modo: PERSONALIZADO` e todos os campos preenchidos, e seguir para 6.4.

**6.4. Special Ad Categories**

Por default, assumir array vazio. Perguntar apenas se o produto/oferta sugere categoria especial:
- Produto financeiro / crédito. Perguntar se entra em `CREDIT`.
- Vagas de emprego / cursos vinculados a emprego. Perguntar `EMPLOYMENT`.
- Imobiliário. Perguntar `HOUSING`.
- Conteúdo político / questões sociais. Perguntar `ISSUES_ELECTIONS_POLITICS`.

Se nenhum desses sinais, seguir com `special_ad_categories: []`. Mostrar no preview pra aluno confirmar visualmente.

### Fase 7. Criativos
Pergunta (3 opções, nesta ordem):
> "Como você quer adicionar os criativos?
>
> 1. Vou enviar arquivos agora (imagens ou vídeos)
> 2. Ainda não tenho criativos prontos (monto a estrutura e adiciono depois)
> 3. Já estão na biblioteca da conta (informo os IDs)"

**7.1. Upload de novos (opção 1)**

Instrução ao aluno antes de prosseguir:
> "Coloque as imagens ou vídeos que quer usar como criativo na pasta:
> `criativos/` (na raiz da pasta `trafego-com-ia`)
>
> Formatos aceitos:
> - Imagem: JPG ou PNG. Tamanho máximo: 30 MB. Resolução recomendada: 1080x1080 (Feed), 1080x1350 (Feed vertical) ou 1080x1920 (Reels/Stories).
> - Vídeo: MP4 ou MOV. Tamanho máximo: 4 GB (recomendado abaixo de 1 GB para upload mais rápido). Duração recomendada: até 60 segundos para Reels, até 120 segundos para Feed.
>
> Quando terminar de copiar os arquivos, me avise e eu listo o que encontrei e sigo com o upload."

Após confirmação do aluno, ler o conteúdo da pasta `criativos/` (na raiz da pasta `trafego-com-ia`) e listar os arquivos encontrados. Mostrar tabela com nome, formato e tamanho estimado. Se houver mais arquivos do que anúncios previstos na estrutura, perguntar quais usar.

Subir cada arquivo, **roteando por `META_AUTH_MODO`**. O upload de **arquivo local** (imagem ou vídeo) é uma das 4 lacunas do MCP.

- **`APP` / `HIBRIDO`:** subir via Marketing API (passa pelo gate 🛡️, token inline mascarado):
  - Imagem: `POST https://graph.facebook.com/v25.0/act_{FB_AD_ACCOUNT_ID}/adimages` com o arquivo em multipart/form-data.
  - Vídeo: `POST https://graph-video.facebook.com/v25.0/act_{FB_AD_ACCOUNT_ID}/advideos` com o arquivo em multipart/form-data.

  > **Host dedicado de vídeo (regra dura).** Upload de vídeo usa o host **`graph-video.facebook.com`**, NÃO `graph.facebook.com`. Vídeos grandes (testado com ~280 MB) retornam **HTTP 413 (Payload Too Large)** no host padrão e sobem normalmente no host de vídeo. Resposta de sucesso: `{"id":"<video_id>"}`. Comando: `curl -sS -w "\nHTTP_CODE:%{http_code}\n" -X POST "https://graph-video.facebook.com/v25.0/act_{id}/advideos?access_token=<TOKEN_DO_ENV>" -F "source=@/caminho/absoluto/video.mp4" -F "name=<nome>"`. Usar `-w "%{http_code}"` para flagrar o 413 (com `-s` puro o erro de tamanho volta vazio e parece que "não aconteceu nada").

  > **Vídeo de anúncio EXIGE thumbnail (regra dura).** Criar o anúncio com vídeo SEM miniatura falha com erro `100` / subcode `1443226` (*"Your ad needs a video thumbnail"*) — o auto-thumbnail prometido pela tool `ads_create_creative`/`ads_create_ad` **não funciona na prática**. Fluxo correto após o upload: (1) buscar `GET /{video_id}?fields=status,thumbnails{uri,is_preferred}` com `curl -g`; (2) esperar `status.video_status = "ready"`; (3) pegar a thumbnail com `is_preferred:true`; (4) passar a `uri` dela como `image_url` dentro de `video_data` (no `object_story_spec` do anúncio) ou no `ads_create_creative`. Sem essa miniatura, qualquer anúncio de vídeo trava.

- **`MCP_CONECTOR` (sem upload de arquivo):** antes de escalar, checar se dá pra evitar a lacuna:
  - **Imagem já numa URL pública?** Então não há lacuna: o `ads_create_creative` aceita `image_url` direto. Pedir a URL ao aluno e seguir.
  - **Vídeo já postado na página (tem `video_id`)?** Idem: `ads_create_creative` aceita `video_id`. Pedir o ID e seguir.
  - **Senão (arquivo local sem URL / vídeo não postado):** acionar o **Protocolo de Escalada**, oferecendo: **(a)** hospedar a imagem numa URL pública / postar o vídeo na página pra obter o `video_id`, ou **(b)** ativar o modo App pra subir o arquivo pelo chat (vira `HIBRIDO`). Nunca tentar `POST /adimages` ou `/advideos` no MCP puro.

Geração de imagem fora do escopo desta skill. O aluno traz a imagem pronta ou usa o método e a ferramenta que preferir antes de retornar para o upload.

**7.2. Sem criativos prontos (opção 2)**

Seguir para as próximas fases e montar o preview YAML com o campo `media_id: null` em cada anúncio. Adicionar nota no preview:
> "Criativos pendentes. Antes de ativar a campanha, adicione os arquivos em `criativos/` (na raiz da pasta `trafego-com-ia`) e me peça para fazer o upload e vincular aos anúncios."

**7.3. Criativos existentes na biblioteca (opção 3)**
- Se aluno declarar IDs: confirmar via `GET /{ad_id}` que existem.
- Se aluno pedir "lista os criativos disponíveis": chamar Graph API e listar últimos 20 com nomes/IDs.

**7.3. Copy do anúncio**
Para cada anúncio, pedir:
- Headline (título curto)
- Primary text (corpo)
- Description (descrição opcional, aparece em alguns posicionamentos)
- CTA (botão. `SHOP_NOW`, `LEARN_MORE`, `SIGN_UP`, etc., escolha conforme objetivo)
- URL de destino (a skill sempre adiciona os parâmetros UTM padrão automaticamente, sem perguntar ao aluno)

**UTMs obrigatórios em todos os anúncios (Sales e Leads):** a skill monta a URL final concatenando a URL de destino com os seguintes parâmetros dinâmicos do Meta:

```
utm_source=meta-ads
&utm_campaign={{campaign.name}}|{{campaign.id}}
&utm_medium={{adset.name}}|{{adset.id}}
&utm_content={{ad.name}}|{{ad.id}}
&utm_term={{placement}}
```

Exemplo de URL final: `https://meusite.com/pagina?utm_source=meta-ads&utm_campaign={{campaign.name}}|{{campaign.id}}&utm_medium={{adset.name}}|{{adset.id}}&utm_content={{ad.name}}|{{ad.id}}&utm_term={{placement}}`

Regras de montagem:
- Se a URL de destino já tiver `?`, concatenar com `&utm_source=...`
- Se não tiver, concatenar com `?utm_source=...`
- Nunca perguntar ao aluno se quer ou não usar UTMs. São sempre aplicados.
- Nunca deixar o aluno digitar os UTMs manualmente. A skill monta automaticamente.

**7.4. Geração de copy por IA**
Se aluno pedir explicitamente "me ajuda com a copy" ou "gera variações", instruir que a geração de copy está fora do escopo desta skill. O aluno traz a copy pronta ou usa o método e a ferramenta que preferir. NÃO gerar copy aqui.

### Fase 8. Posicionamentos
Default: **Advantage+ Placements** (todos automáticos). Mostrar como recomendação.

Override: se aluno declarar "só Feed" ou "só Reels e Stories", aceitar e configurar manualmente.

### Fase 9. Nome da campanha
Padrão automático:
```
[Tipo de funil] - [Produto] - [Estrutura] - [Data]
```

Exemplo: `Perpétuo - Curso X - 1-1-3 - 2026-05-04`

Para conjuntos e anúncios, padrão similar:
- Conjunto: `AS - [Audiência] - [Apelido]`
- Anúncio: `AD - [Ângulo] - [Formato]`

Mostrar no preview. Aluno pode editar nome de qualquer nível antes de confirmar.

---

## 3. Preview antes de criar (sempre)

Antes de qualquer chamada à Marketing API que modifique a conta:

**3.1. Gerar e salvar o YAML completo internamente** em `meus-produtos/{ativo}/entregas/trafego/preview-campanha-{tipo_funil}-{slug}-{data}.yaml`. O YAML segue o esquema abaixo. Esse arquivo serve como referência técnica completa, fica salvo para auditoria e é o que a skill usa para fazer as chamadas da Marketing API.

**3.2. Mostrar ao aluno apenas um RESUMO EM TEXTO CORRIDO**, em português, organizado em blocos claros (Conta, Campanha, Conjunto, Anúncios, Validações, Próximas ações). Sem YAML, sem chaves, sem códigos, sem indentação técnica. Texto fluido, fácil de entender, com bullets simples e linguagem direta. Se o aluno pedir explicitamente para ver o YAML, abrir o arquivo salvo.

**3.3. Regra de identificação por nome (obrigatória).** Em TODA referência a um ID no resumo de texto (ID de conta, ID de página, ID de Instagram, ID de Pixel, ID de conversão personalizada, ID de público customizado, ID de criativo, ID de campanha existente, qualquer outro), trazer o **nome humano junto do ID**, no formato `Nome (ID)`. Se o nome não estiver disponível em cache, buscar via API antes de mostrar:
- Page: `GET /{page_id}?fields=name,username&access_token=...`
- Instagram: `GET /{ig_user_id}?fields=username,name&access_token=...`
- Pixel: já trazido pela listagem de pixels da Fase 5.
- Conversão personalizada: já trazido pela listagem da Fase 5.2.
- Público customizado: já trazido pela listagem.
- Criativo/Campanha existente: `GET /{id}?fields=name`.

Nunca mostrar apenas "Page ID 100000000000001" ou "Instagram conectado a ela". Sempre `Página Exemplo (100000000000001)` e `@pagina_exemplo (17800000000000001)`.

Esquema do YAML salvo:

```yaml
preview_campanha:
  conta:
    ad_account_id: "act_1234567890"
    page_id: "..."
    instagram_user_id: "..."

  campanha:
    nome: "Perpétuo - Curso X - 1-1-3 - 2026-05-04"
    objective: OUTCOME_SALES
    status: PAUSED                          # sempre PAUSED por default
    special_ad_categories: []
    buying_type: AUCTION
    budget_estrutura: ABO                   # ou CBO
    daily_budget_brl: null                  # se ABO, fica em null aqui e vai no conjunto

  conjuntos:
    - nome: "AS - Advantage+ - Brasil"
      daily_budget_brl: 100.00              # se ABO
      optimization_goal: OFFSITE_CONVERSIONS
      billing_event: IMPRESSIONS
      pixel_id: "1122334455"
      custom_event_type: PURCHASE           # ou LEAD
      attribution_spec: "7d_click"
      placements: ADVANTAGE_PLUS            # ou lista manual
      audience:
        modo: ADVANTAGE_PLUS
        sugestoes:
          paises: ["BR"]
          idade: [25, 55]
          interesses: []
        excluidos:
          custom_audiences: []
          lookalikes: []
      schedule:
        start_time: "2026-05-04T18:00:00-03:00"   # próxima hora cheia, default
        end_time: null
      learning_phase_protection: true

  anuncios:
    - nome: "AD - Dor - Vídeo 30s"
      adset_index: 0                        # qual conjunto pai
      criativo:
        tipo: video                         # ou image, carousel
        media_id: "..."                     # ID do vídeo já uploaded
        headline: "..."
        primary_text: "..."
        description: "..."
        cta: SHOP_NOW
        link: "https://..."
        utm_params:
          source: "facebook"
          medium: "cpc"
          campaign: "perpetuo-curso-x"

    - nome: "AD - Benefício - Imagem"
      ...

    - nome: "AD - Prova - Carrossel"
      ...

  validacoes_pre_criacao:
    pixel_ativo: true
    evento_recebendo_dados_7d: true
    budget_coerente_com_ticket: true
    page_id_valido: true
    instagram_user_id_valido: true
    criativos_no_formato_correto: true

  proximas_acoes_apos_criar:
    - "Acessar Gerenciador e revisar visualmente"
    - "Ativar quando estiver tudo certo (skill pode ativar se você pedir)"
```

Pedir confirmação:
> "Esse é o preview da campanha. Confirma criar com `status: PAUSED`? Você pode editar qualquer campo antes de aprovar."

Aceitar três tipos de resposta:
- **"confirmo" / "pode subir" / "ok"** → executar criação.
- **"muda X"** → ajustar e mostrar preview de novo.
- **"cancela"** → não criar nada, encerrar.

---

## 4. Execução da criação

Após aprovação (gate 🛡️), criar em ordem. **Rotear cada chamada por `META_AUTH_MODO`** (ver §8): no `MCP_CONECTOR`/`HIBRIDO` usar as tools `ads_create_*`; no `APP` usar curl. Criação de campanha/conjunto/anúncio/criativo **não é lacuna** em nenhum modo.

1. **Campanha**. `ads_create_campaign` (MCP) ou `POST /act_{id}/campaigns` (APP)
2. **Para cada conjunto**. `ads_create_ad_set` (MCP) ou `POST /act_{id}/adsets` (APP)
3. **Para cada anúncio:**
   - Criar AdCreative. `ads_create_creative` (MCP) ou `POST /act_{id}/adcreatives` (APP)
   - Criar Ad. `ads_create_ad` (MCP) ou `POST /act_{id}/ads` (APP)

Tratamento de falhas:
- **Falha em criar campanha** → parar tudo, retornar erro.
- **Falha em criar conjunto** → reverter (deletar campanha já criada se nada útil ali), retornar erro.
- **Falha em criar anúncio** → manter o que já subiu (campanha + conjuntos + anúncios anteriores), retornar erro detalhado, perguntar se quer tentar criar os anúncios restantes manualmente depois.

Não fazer rollback completo automático. Em geral é melhor preservar o que funcionou e deixar o aluno decidir.

---

## 5. Output esperado após criação

```yaml
status: criado_com_sucesso | criado_parcialmente | falha
campanha:
  id: "120203456789"
  nome: "Perpétuo - Curso X - 1-1-3 - 2026-05-04"
  status: PAUSED
  ad_account_id: "act_1234567890"
  url_gerenciador: "https://business.facebook.com/adsmanager/manage/campaigns?act=1234567890&selected_campaign_ids=120203456789"

conjuntos_criados:
  - id: "120203456789001"
    nome: "AS - Advantage+ - Brasil"
    status: PAUSED

anuncios_criados:
  - id: "120203456789999"
    nome: "AD - Dor - Vídeo 30s"
    adset_id: "120203456789001"
    status: PAUSED

falhas:                                     # vazio em sucesso total
  - nivel: ad
    nome: "AD - Curiosidade - Imagem"
    motivo: "criativo bloqueou validação por texto excessivo"
    acao_sugerida: "ajustar imagem ou refazer manualmente"

proximos_passos:
  - "Acessar o Gerenciador no link acima"
  - "Revisar visualmente cada anúncio (preview, copy, criativo)"
  - "Quando estiver tudo certo, ativar manualmente OU me peça 'ativa a campanha'"
  - "Após 48 a 72h de veiculação, use /trafego-otimizar para o primeiro diagnóstico"
  - "Para puxar dados de performance: /trafego-insights"

ativacao:
  status_atual: PAUSED
  pode_ativar_via_skill: true               # skill aceita comando posterior "ativa essa campanha"
```

---

## 6. Modo expresso. Exemplo

Aluno envia em uma mensagem só:

> "sobe campanha de venda do curso X (R$497), R$100/dia ABO, advantage+ Brasil, usa o vídeo ID 23847..., headline 'Domine X em 30 dias', CTA SHOP_NOW, URL https://meusite.com/curso-x?utm_source=fb"

Skill executa:

1. **Inferir** o que conseguir: objetivo `OUTCOME_SALES`, ticket R$ 497, trilha `perpetuo_low`, ABO, Advantage+ Audience, criativo existente, etc.
2. **Aplicar defaults**:
   - 1 campanha, 1 conjunto, 1 anúncio (estrutura mínima)
   - Posicionamentos Advantage+
   - `special_ad_categories: []`
   - Status PAUSED
   - Nomenclatura padrão
3. **Validar tracking**: chamar pixel e evento no fundo.
4. **Mostrar preview completo** em YAML (igual seção 3).
5. **Pedir aprovação única**.
6. **Criar** após "confirmo".

Diferença essencial vs modo guia: zero perguntas intermediárias, mas o preview ainda é obrigatório.

---

## 7. Casos de borda e proteções

### 7.1 Conta sem Page ou Instagram configurado
Antes de prosseguir, ler `META_PAGE_ID` e `META_INSTAGRAM_USER_ID` do `.env`. Se algum faltar, descobrir (leitura, não é lacuna): MCP/HIBRIDO via `ads_get_ad_account_pages`; APP via `GET /act_{FB_AD_ACCOUNT_ID}/...` de páginas. Se faltar Instagram e o aluno não declarar Reels/Stories, criar só com Page (Feed Facebook). Se o aluno pedir Reels/Stories sem IG configurado, parar e instruir a executar `/trafego-conexao`.

### 7.2 Budget muito baixo para o ticket
Se `daily_budget < CPA target × 0.5`, avisar e pedir confirmação. Não bloquear, mas não deixar passar silencioso.

### 7.3 Mais de 5 anúncios no mesmo conjunto
Avisar: "Mais de 5 anúncios no mesmo conjunto disputam aprendizado entre si. Sugiro dividir em mais conjuntos ou priorizar 3 a 5 ângulos. Quer ajustar ou prosseguir?"

### 7.4 Criativo com texto excessivo na imagem
A Marketing API não rejeita mais por excesso de texto (regra antiga descontinuada), mas posicionamentos como Reels podem performar pior. Apenas avisar quando a imagem tem muito texto, sem bloquear.

### 7.5 Campanha duplicada (mesmo nome ativa há < 7 dias)
Avisar: "Existe campanha ativa com nome similar criada há X dias. Quer prosseguir mesmo assim, renomear, ou cancelar?"

### 7.6 Aluno pede para ativar imediatamente após criar
Aceitar comando "ativa a campanha" como ação separada (não é lacuna; rotear por modo). MCP/HIBRIDO: `ads_activate_entity` (ou `ads_update_entity` com `status=ACTIVE`). APP: `POST /{campaign_id}` com `status: ACTIVE`. Passa pelo gate 🛡️. Sempre confirmar antes: "Vou ativar a campanha agora. Uma vez ativa, começa a gastar. Confirma?"

---

## 8. Como subir os dados (roteamento por META_AUTH_MODO)

A skill lê `META_AUTH_MODO` no `.env` e roteia **cada operação** por uma de três vias.

> **Regra de ouro.** O modo `APP` faz tudo via curl e **nunca tem lacuna**. A noção de "lacuna" e o protocolo de escalada **só existem no mundo MCP**. Em `APP` puro, a escalada jamais aparece.

### 8.1 Decisão por modo

- **`APP`** → curl na Graph API usando `FB_ACCESS_TOKEN_PERMANENTE` + `FB_AD_ACCOUNT_ID` (lidos do `.env`, token inline no curl, mascarado na exibição). Cobre **todas** as operações, sem exceção. Sem lacuna, sem escalada.
- **`MCP_CONECTOR`** → tools `ads_*` do conector. Nas **4 lacunas** (upload de vídeo, upload de imagem de arquivo local, busca de interesse por nome, criar lookalike), seguir o **Protocolo de Escalada** definido na skill `trafego-conexao` (oferecer ativar o App, ou o caminho manual). Nunca montar curl com token nesse modo: ele não existe aqui.
- **`HIBRIDO`** → tools `ads_*` no geral; ao bater numa das 4 lacunas, cair no curl com `FB_ACCESS_TOKEN_PERMANENTE` **em silêncio** (sem reperguntar, porque o aluno já autorizou o App ao entrar no híbrido).

### 8.2 Token e conta por modo (corrige variáveis antigas)

- **`APP` / `HIBRIDO`:** `FB_ACCESS_TOKEN_PERMANENTE` (token) e `FB_AD_ACCOUNT_ID` (conta, sem prefixo `act_`).
- **`MCP_CONECTOR`:** **nenhum token**. O `ad_account_id` exigido pelas tools vem de `FB_AD_ACCOUNT_ID` do `.env`, passado como parâmetro da tool.
- **Nunca usar `META_ACCESS_TOKEN` nem `META_AD_ACCOUNT_ID`.** Essas variáveis não existem no projeto. Token = `FB_ACCESS_TOKEN_PERMANENTE`; conta = `FB_AD_ACCOUNT_ID`.

### 8.3 Mapa de roteamento por operação

| Operação | Fase | Tool MCP (MCP / HIBRIDO) | curl (APP / fallback HIBRIDO) | Lacuna no MCP? |
|---|---|---|---|---|
| Listar pixels | 5.0 | `ads_get_datasets` | `GET /act_{id}/adspixels` | não |
| Validar evento (dados 7d) | 5.3 | `ads_get_dataset_stats` | `GET /{pixel}/stats` | não |
| Listar conversão personalizada | 5.2 | `ads_get_customconversions` | `GET /act_{id}/customconversions` | não |
| Listar públicos / lookalikes | 6.3 | `ads_get_ad_account_custom_audiences` | `GET /act_{id}/customaudiences` | não |
| **Buscar interesse por nome** | 6.2 / 6.3.3 | (sem tool) | `GET /search?type=adinterest` | **sim** |
| **Criar lookalike** | 6.3.2 | (sem tool) | `POST /act_{id}/customaudiences` subtype LOOKALIKE | **sim** |
| Listar Pages / IG | 7.1 | `ads_get_ad_account_pages` | `GET /act_{id}/... pages` | não |
| **Upload de imagem (arquivo local)** | 7.1 | (sem tool) | `POST /act_{id}/adimages` | **sim** |
| **Upload de vídeo** | 7.1 | (sem tool) | `POST /act_{id}/advideos` | **sim** |
| Criar criativo | 4 | `ads_create_creative` | `POST /act_{id}/adcreatives` | não |
| Criar campanha | 4 | `ads_create_campaign` | `POST /act_{id}/campaigns` | não |
| Criar conjunto | 4 | `ads_create_ad_set` | `POST /act_{id}/adsets` | não |
| Criar anúncio | 4 | `ads_create_ad` | `POST /act_{id}/ads` | não |
| Ativar campanha (7.6) | 7.6 | `ads_activate_entity` / `ads_update_entity` | `POST /{id}` status=ACTIVE | não |

Observações:
- **Imagem via URL pública não é lacuna.** Se o criativo já está numa URL pública, o `ads_create_creative` aceita `image_url` direto, sem upload. A lacuna é só imagem de **arquivo local**.
- **Vídeo já postado na página não é lacuna.** Se existe um `video_id` (ex: vídeo postado organicamente na Fanpage), o `ads_create_creative` aceita `video_id`. A lacuna é só o **upload** de um vídeo novo.
- Descoberta de tool MCP é por **sufixo** (ex: `ads_create_campaign`), não por prefixo (que pode ser um UUID). Ver `trafego-conexao` §5.1.

### 8.4 Limite de escopo (inalterado)

A skill **nunca** chama tools de edição em campanhas existentes (`pause_ad`, `update_adset_budget`, `duplicate_adset`). Essas pertencem a `/trafego-otimizar` e `/trafego-escalar`. A única escrita pós-criação que esta skill aceita é **ativar** a campanha recém-criada, quando o aluno pedir (7.6).

---

## 9. Princípios que a skill nunca viola

1. **Sales/Leads sem pixel = não cria.** Regra dura. Otimização cega não é aceitável.
2. **Sempre PAUSED por default.** Ativação só com pedido explícito.
3. **Preview antes de criar, sempre.** Inclusive no modo expresso.
4. **Liberdade de estrutura.** Skill sugere, aluno decide. Aceita estruturas customizadas.
5. **Nomenclatura padrão com override.** Default automático, aluno pode editar qualquer nível.
6. **Não cobre objetivos fora de Sales/Leads.** Se o aluno pedir Awareness, Traffic, Engagement ou App Promotion, recusar com explicação clara.
7. **Validações antes da API.** Pixel ativo, page e IG configurados, budget coerente. Tudo verificado antes da primeira chamada de criação.
8. **Falha parcial preserva o que funcionou.** Não fazer rollback automático completo a menos que faça sentido.
9. **Não inventar IDs.** Se o aluno referenciar criativo, audience ou pixel sem ID claro, listar opções e pedir confirmação.
10. **Special Ad Categories são propostas, não impostas.** Aluno confirma no preview.
11. **Modo expresso preserva preview.** Velocidade não compra atalho de segurança.
12. **Geração de copy fora do escopo desta skill.** Skill nunca gera copy diretamente. O aluno traz pronta ou usa o método e a ferramenta que preferir.
