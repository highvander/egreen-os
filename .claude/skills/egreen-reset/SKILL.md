---
name: egreen-reset
description: >-
  Use quando o usuário quiser apagar o projeto atual e começar do zero. Dispara com
  "resetar produto", "limpar memória", "começar novo produto", "apagar projeto atual",
  "reset", "recomeçar do zero" ou qualquer variação de reinicialização do projeto.
  Sempre oferece backup antes de qualquer exclusão.
allowed-tools: Read, Write, Edit, Glob, Bash, Skill, AskUserQuestion
model: sonnet
---

# Reset Produto — Limpar Projeto e Recomeçar

Apaga os arquivos de memória do projeto atual e restaura o estado inicial do EGreen OS,
com opção de backup completo antes de qualquer exclusão. O backup cobre memória E todos
os outputs gerados. O reset apaga apenas a memória (gate) — outputs não são deletados.

---

## Passo 0. Identificar o projeto atual

Leia `memoria/egreen-produto.md` e `memoria/egreen-nicho.md` para extrair o nome do projeto.

- Se `egreen-produto.md` tiver `status: vazio`, usar o nicho como identificador.
- Se ambos estiverem vazios, avisar que não há projeto ativo e encerrar.

Nome do projeto para exibição: derivar do campo **Nome** de `egreen-produto.md` ou do
campo **Nicho** de `egreen-nicho.md`, no formato legível (ex: "Curso de Genealogia Amadora").

---

## Passo 1. Pergunta de backup

```
Antes de continuar, gostaria de fazer backup do projeto atual?

Projeto detectado: {nome do projeto}

O backup vai salvar (se existirem):
  Memória:
    - memoria/egreen-nicho.md
    - memoria/egreen-produto.md
    - memoria/egreen-funil.md
    - memoria/egreen-design.md

  Outputs gerados:
    - egreen-nicho/
    - egreen-pesquisa/
    - egreen-produto/
    - egreen-concepcao/
    - egreen-funil/
    - egreen-copy/
    - egreen-landing/
    - egreen-mandala/
    - egreen-carrossel/
    - egreen-editorial/
    - egreen-slides/
    - egreen-meta-ads/
    - egreen-google-ads/
    - egreen-analise/

1. Sim — copiar tudo para backup antes de resetar
2. Não — já fiz o backup manualmente, pode continuar
```

---

## Passo 1A. Backup automático

Se o usuário escolher **1**:

1. Definir pasta raiz do backup com timestamp e slug:
   ```
   backup/YYYY-MM-DD-HH-MM/{slug-do-projeto}/
   ```
   Slug: nome do projeto em minúsculas, sem acentos, espaços viram hífen.
   Ex: `backup/2026-06-01-14-30/curso-genealogia-amadora/`

2. Copiar arquivos de memória (exceto `formatos.md` — referência permanente do OS):
   ```
   memoria/egreen-nicho.md     → backup/.../memoria/egreen-nicho.md
   memoria/egreen-produto.md   → backup/.../memoria/egreen-produto.md
   memoria/egreen-funil.md     → backup/.../memoria/egreen-funil.md
   memoria/egreen-design.md    → backup/.../memoria/egreen-design.md  (se existir)
   ```

3. Copiar cada pasta de output que existir, mantendo estrutura:
   ```
   egreen-nicho/              → backup/.../egreen-nicho/
   egreen-pesquisa/   → backup/.../egreen-pesquisa/
   egreen-produto/            → backup/.../egreen-produto/
   egreen-concepcao/          → backup/.../egreen-concepcao/
   egreen-funil/              → backup/.../egreen-funil/
   egreen-copy/               → backup/.../egreen-copy/
   egreen-landing/            → backup/.../egreen-landing/
   egreen-mandala/            → backup/.../egreen-mandala/
   egreen-carrossel/          → backup/.../egreen-carrossel/
   egreen-editorial/          → backup/.../egreen-editorial/
   egreen-slides/       → backup/.../egreen-slides/
   egreen-meta-ads/       → backup/.../egreen-meta-ads/
   egreen-google-ads/     → backup/.../egreen-google-ads/
   egreen-analise/            → backup/.../egreen-analise/
   ```
   Usar `cp -r` (Bash) para cada pasta. Pular silenciosamente as que não existirem.

4. Confirmar ao usuário:

```
Backup criado em:
  backup/{YYYY-MM-DD-HH-MM}/{slug}/

  Memória salva: {lista dos arquivos copiados}
  Outputs salvos: {lista das pastas copiadas}
```

5. Seguir para o Passo 2.

---

## Passo 1B. Caminho sem backup

Se o usuário escolher **2**, exibir aviso final:

```
⚠️  Esta ação não pode ser desfeita.

Todos os arquivos de memória do projeto "{nome do projeto}" serão
apagados permanentemente. Os outputs gerados (pastas 01-nicho,
02-pesquisa-mercado, etc.) não serão afetados.

Tem certeza?

1. Sim, estou consciente de que perderei todo o projeto "{nome do projeto}".
2. Não. Cancele o reset.
```

- Se escolher **2**: encerrar sem fazer nada. Mensagem: "Reset cancelado. Projeto intacto."
- Se escolher **1**: seguir para o Passo 2.

---

## Passo 2. Executar o reset

Restaurar os 3 arquivos de memória ao estado inicial (placeholder vazio):

**`memoria/egreen-nicho.md`**
```markdown
---
status: vazio
preenchido_por: /egreen-setup
---

<!-- Este arquivo é preenchido automaticamente pela skill /egreen-setup -->
<!-- Não edite manualmente -->
```

**`memoria/egreen-produto.md`**
```markdown
---
status: vazio
preenchido_por: /egreen-setup
---

<!-- Este arquivo é preenchido automaticamente pela skill /egreen-setup -->
<!-- Não edite manualmente -->
```

**`memoria/egreen-funil.md`**
```markdown
---
status: vazio
preenchido_por: /egreen-setup (via /egreen-funil)
---

<!-- Este arquivo é preenchido automaticamente pela skill /egreen-setup ao invocar /egreen-funil -->
<!-- Não edite manualmente -->
```

Se existir `memoria/egreen-design.md`, apagar o conteúdo e restaurar placeholder:
```markdown
---
status: vazio
preenchido_por: /egreen-design
---

<!-- Este arquivo é preenchido automaticamente pela skill /egreen-design -->
<!-- Não edite manualmente -->
```

---

## Passo 3. Confirmação e próximo passo

```
✓ Reset concluído.

Memória apagada:
  ✓ memoria/egreen-nicho.md — restaurado
  ✓ memoria/egreen-produto.md — restaurado
  ✓ memoria/egreen-funil.md — restaurado
  [✓ memoria/egreen-design.md — restaurado]  (se existia)

Outputs anteriores preservados nas pastas originais.
[Backup salvo em: backup/{YYYY-MM-DD-HH-MM}/{slug}/]  (se backup foi feito)

Quer configurar um novo produto agora?

1. Sim — iniciar /egreen-setup
2. Não — encerrar
```

- Opção **1**: invocar skill `/egreen-setup`.
- Opção **2**: encerrar.

---

## Regras

1. **Nunca apagar `memoria/formatos.md`** — é referência permanente do OS, não do projeto
2. **Nunca apagar pastas de output** — reset limpa só a memória; outputs ficam nas pastas originais
3. **Nunca pular o aviso de confirmação** — mesmo que o usuário peça reset direto
4. **Backup cobre memória + outputs** — usar `cp -r` para cada pasta; pular silenciosamente as inexistentes
5. **Backup preserva estrutura de pastas** — espelha a raiz do projeto dentro de `backup/{timestamp}/{slug}/`
