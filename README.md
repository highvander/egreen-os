# VTSD OS — Agentic OS para Marketing Digital de Infoprodutos

Sistema de skills para criar e vender infoprodutos digitais. Cada etapa do
pipeline de marketing (nicho → produto → concepção → copy → tráfego) é uma
skill independente, invocada como slash command dentro do Claude Code.

---

## Como funciona

O VTSD OS usa o sistema de skills do Claude Code. Ao abrir o projeto no Claude
Code, os comandos abaixo ficam disponíveis automaticamente. Cada skill lê a
memória do produto ativo, executa sua tarefa e salva o output na pasta
correspondente — sem precisar pedir.

---

## Pré-requisito

[Claude Code](https://claude.ai/code) com acesso a um projeto local (CLI ou
extensão VS Code / JetBrains).

---

## Instalação

```bash
git clone https://github.com/highvander/vtsd-os
cd vtsd-os
```

Abra a pasta no Claude Code e rode:

```
/instalar
```

O comando `/instalar` conduz uma entrevista de 8 minutos, cria a pasta do
novo produto e desbloqueia o pipeline completo.

---

## Estrutura multi-produto

Cada produto vive em sua própria pasta isolada. Rodar `/instalar` novamente
**nunca sobrescreve** o produto anterior — cria uma pasta nova automaticamente.

```
vtsd-os/
  memoria/
    formatos.md          ← referência permanente do OS
    produto-ativo.md     ← aponta para o produto em uso
  produto-01/            ← criado pelo primeiro /instalar
    memoria/
      nicho.md
      produto.md
      funil.md
      design.md          ← gerado por /design (opcional)
    01-nicho/
    02-pesquisa-mercado/
    03-produto/
    04-concepcao/
    05-funil/
    06-copy/
    06-landing/
    06-mandala/
    07-carrossel/
    07-editorial/
    07-apresentacao/
    08-trafego-meta/
    08-trafego-google/
    09-analise/
  produto-02/            ← criado pelo segundo /instalar
    ...
  .claude/skills/        ← skills do sistema
  references/            ← referências técnicas do OS
```

Todas as pastas `produto-*/` estão no `.gitignore` — os dados de cada produto
ficam apenas na máquina local.

---

## Pipeline de Skills

| # | Comando | O que entrega |
|---|---------|---------------|
| 0 | `/instalar` | Entrevista inicial — cria pasta produto-XX/, configura memória e funil |
| 0 | `/design` | Sistema de design (paleta, tipografia, componentes visuais) |
| 1 | `/nicho` | Pesquisa e posicionamento de nicho |
| 1.5 | `/pesquisa-mercado` | Pesquisa profunda em 9 eixos com busca real na web |
| 2 | `/produto` | 50 ideias de infoproduto em 15 formatos |
| 2.5 | `/concepcao` | Promessa, 50 benefícios, 5 baldes e identidade do consumidor |
| 3 | `/funil` | Funil completo com order bump, OTO e sequência de email |
| 4 | `/copy-pagina-vendas` | Copy de página de vendas em 15 blocos (Light Copy) |
| 4 | `/landing` | Página de vendas HTML completa |
| 4 | `/mandala` | 4 tipos de anúncio argumentativo para Meta Ads |
| 5 | `/carrossel` | Carrossel de curiosidade para Instagram (7-9 slides) |
| 5 | `/editorial` | Carrossel editorial com dados e pesquisa (6 slides) |
| 5 | `/apresentacao` | Slides HTML animados para pitch ou aula |
| 6 | `/trafego-conexao` | Autenticação com Meta Ads |
| 6 | `/trafego-criar-campanha` | Sobe campanha Meta Ads (Sales ou Leads) |
| 6 | `/trafego-google` | Campanhas Google Ads |
| 7 | `/analise` | Métricas, relatórios e otimização |
| — | `/analista-seo` | Auditoria SEO, GEO e AEO completa |
| — | `/reset-produto` | Apaga memória do produto ativo com opção de backup |

---

## Créditos

- Skill `/apresentacao` baseada em
  [frontend-slides](https://github.com/zarazhangrui/frontend-slides)
  por Zara Zhang — licença MIT
