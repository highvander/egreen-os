---
name: reset-produto
description: >-
  Use quando o usuário quiser apagar o projeto atual e começar do zero. Dispara com
  "resetar produto", "limpar memória", "começar novo produto", "apagar projeto atual",
  "reset", "recomeçar do zero" ou qualquer variação de reinicialização do projeto.
  Sempre oferece backup antes de qualquer exclusão.
allowed-tools: Read, Write, Edit, Glob, Bash, Skill, AskUserQuestion
model: sonnet
---

# Reset Produto — Limpar Projeto e Recomeçar

Apaga os arquivos de memória do projeto atual e restaura o estado inicial do VTSD OS,
com opção de backup completo antes de qualquer exclusão. O backup cobre memória E todos
os outputs gerados. O reset apaga apenas a memória (gate) — outputs não são deletados.

---

## Passo 0. Identificar o projeto atual

Leia `memoria/produto.md` e `memoria/nicho.md` para extrair o nome do projeto.

- Se `produto.md` tiver `status: vazio`, usar o nicho como identificador.
- Se ambos estiverem vazios, avisar que não há projeto ativo e encerrar.

Nome do projeto para exibição: derivar do campo **Nome** de `produto.md` ou do
campo **Nicho** de `nicho.md`, no formato legível (ex: "Curso de Genealogia Amadora").

---

## Passo 1. Pergunta de backup

```
Antes de continuar, gostaria de fazer backup do projeto atual?

Projeto detectado: {nome do projeto}

O backup vai salvar (se existirem):
  Memória:
    - memoria/nicho.md
    - memoria/produto.md
    - memoria/funil.md
    - memoria/design.md

  Outputs gerados:
    - 01-nicho/
    - 02-pesquisa-mercado/
    - 03-produto/
    - 04-concepcao/
    - 05-funil/
    - 06-copy/
    - 06-landing/
    - 06-mandala/
    - 07-carrossel/
    - 07-editorial/
    - 07-apresentacao/
    - 08-trafego-meta/
    - 08-trafego-google/
    - 09-analise/

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
   memoria/nicho.md     → backup/.../memoria/nicho.md
   memoria/produto.md   → backup/.../memoria/produto.md
   memoria/funil.md     → backup/.../memoria/funil.md
   memoria/design.md    → backup/.../memoria/design.md  (se existir)
   ```

3. Copiar cada pasta de output que existir, mantendo estrutura:
   ```
   01-nicho/              → backup/.../01-nicho/
   02-pesquisa-mercado/   → backup/.../02-pesquisa-mercado/
   03-produto/            → backup/.../03-produto/
   04-concepcao/          → backup/.../04-concepcao/
   05-funil/              → backup/.../05-funil/
   06-copy/               → backup/.../06-copy/
   06-landing/            → backup/.../06-landing/
   06-mandala/            → backup/.../06-mandala/
   07-carrossel/          → backup/.../07-carrossel/
   07-editorial/          → backup/.../07-editorial/
   07-apresentacao/       → backup/.../07-apresentacao/
   08-trafego-meta/       → backup/.../08-trafego-meta/
   08-trafego-google/     → backup/.../08-trafego-google/
   09-analise/            → backup/.../09-analise/
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

**`memoria/nicho.md`**
```markdown
---
status: vazio
preenchido_por: /instalar
---

<!-- Este arquivo é preenchido automaticamente pela skill /instalar -->
<!-- Não edite manualmente -->
```

**`memoria/produto.md`**
```markdown
---
status: vazio
preenchido_por: /instalar
---

<!-- Este arquivo é preenchido automaticamente pela skill /instalar -->
<!-- Não edite manualmente -->
```

**`memoria/funil.md`**
```markdown
---
status: vazio
preenchido_por: /instalar (via /funil)
---

<!-- Este arquivo é preenchido automaticamente pela skill /instalar ao invocar /funil -->
<!-- Não edite manualmente -->
```

Se existir `memoria/design.md`, apagar o conteúdo e restaurar placeholder:
```markdown
---
status: vazio
preenchido_por: /design
---

<!-- Este arquivo é preenchido automaticamente pela skill /design -->
<!-- Não edite manualmente -->
```

---

## Passo 3. Confirmação e próximo passo

```
✓ Reset concluído.

Memória apagada:
  ✓ memoria/nicho.md — restaurado
  ✓ memoria/produto.md — restaurado
  ✓ memoria/funil.md — restaurado
  [✓ memoria/design.md — restaurado]  (se existia)

Outputs anteriores preservados nas pastas originais.
[Backup salvo em: backup/{YYYY-MM-DD-HH-MM}/{slug}/]  (se backup foi feito)

Quer configurar um novo produto agora?

1. Sim — iniciar /instalar
2. Não — encerrar
```

- Opção **1**: invocar skill `/instalar`.
- Opção **2**: encerrar.

---

## Regras

1. **Nunca apagar `memoria/formatos.md`** — é referência permanente do OS, não do projeto
2. **Nunca apagar pastas de output** — reset limpa só a memória; outputs ficam nas pastas originais
3. **Nunca pular o aviso de confirmação** — mesmo que o usuário peça reset direto
4. **Backup cobre memória + outputs** — usar `cp -r` para cada pasta; pular silenciosamente as inexistentes
5. **Backup preserva estrutura de pastas** — espelha a raiz do projeto dentro de `backup/{timestamp}/{slug}/`
