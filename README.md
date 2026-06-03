# VTSD OS — Agentic OS para Marketing Digital de Infoprodutos

Sistema de skills para criar e vender infoprodutos digitais. Cada etapa do
pipeline de marketing (nicho → produto → concepção → copy → tráfego) é uma
skill independente, invocada como slash command dentro do Claude Code.

---

## Como funciona

O VTSD OS usa o sistema de skills do Claude Code. Ao abrir o projeto no Claude
Code, os comandos abaixo ficam disponíveis automaticamente. Cada skill lê a
memória do projeto (`memoria/`), executa sua tarefa e salva o output na pasta
correspondente — sem precisar pedir.

```
memoria/
  nicho.md       ← quem é o avatar e o mercado
  produto.md     ← o que está sendo criado e a que preço
  funil.md       ← estrutura completa do funil de vendas
  design.md      ← paleta, tipografia e componentes visuais
```

---

## Pré-requisito

[Claude Code](https://claude.ai/code) com acesso a um projeto local (CLI ou
extensão VS Code / JetBrains).

---

## Primeiro uso

```bash
git clone https://github.com/seu-usuario/vtsd-os
cd vtsd-os
# Abra a pasta no Claude Code e rode:
/instalar
```

O comando `/instalar` conduz uma entrevista de 8 minutos, preenche os arquivos
de memória e desbloqueia o pipeline completo.

---

## Pipeline de Skills

| # | Comando | O que entrega |
|---|---------|---------------|
| 0 | `/instalar` | Entrevista inicial — configura nicho, produto e funil |
| 0 | `/design` | Sistema de design (paleta, tipografia, componentes) |
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

---

## Estrutura de pastas

```
memoria/          ← contexto persistente do projeto
01-nicho/         ← outputs de /nicho
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
backup/           ← gerado por /reset-produto
.claude/skills/   ← skills do sistema
```

Todos os arquivos gerados seguem a convenção `YYYY-MM-DD-descricao-curta.ext`.

---

## Créditos

- Skill `/apresentacao` baseada em
  [frontend-slides](https://github.com/zarazhangrui/frontend-slides)
  por Zara Zhang — licença MIT
