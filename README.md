# 🧠 AlimentaAI — Segundo Cérebro

Repositório central de contexto, decisões e conhecimento do ecossistema AlimentaAI.
Serve como **fonte da verdade única** para produto, tecnologia, marketing e operações.

## Como usar

| Objetivo | Como |
|---|---|
| Dar contexto a um LLM | Cole o conteúdo de `99-contexto-llm/contexto-completo.md` |
| Buscar contexto no n8n | HTTP GET na URL raw de qualquer arquivo |
| Registrar uma decisão | Use o template em `12-decisoes/_template.md` |
| Entender uma área | Leia `MAPA.md` → `CONTEXTO.md` → `STACK.md` da área |
| Git: branches, PRs, commits | Ver `04-infraestrutura/REPOS-E-FLUXO-GIT.md` |

## Ecossistema

| Sistema | Repositório | Descrição |
|---|---|---|
| 🧠 Brain (este) | alimentaai-brain | Contexto e decisões |
| 🌐 Site | site-alimentaai | Landing e checkout |
| ⚙️ Automações | alimentaai-n8n | Fluxos n8n |
| 📣 Marketing | alimentaai-marketing | Estratégia e identidade visual |

## Anatomia de cada área

Toda área segue o mesmo padrão de 3 arquivos:
- **MAPA.md** — visão geral, diagrama, estrutura
- **CONTEXTO.md** — propósito, decisões tomadas, estado atual
- **STACK.md** — ferramentas, tecnologias, integrações usadas

## Áreas do cérebro

| # | Área | O que cobre |
|---|---|---|
| 00 | Identidade | Missão, visão, valores, tom de voz |
| 01 | Produto | Features, decisões, preços |
| 02 | Site | Páginas, funil, conversão |
| 03 | N8N | Automações e fluxos |
| 04 | Infraestrutura | Servidores, custos, ambientes |
| 05 | Marketing | Estratégia, canais, identidade visual |
| 06 | Clientes | Personas, feedbacks, churn |
| 07 | Métricas | KPIs, North Star, dashboards |
| 08 | Integrações | Como os sistemas se conectam |
| 09 | Operacional | Processos, rituais, responsabilidades |
| 10 | Roadmap | Agora, em breve, futuro |
| 11 | Prompts | Biblioteca de prompts e modelos LLM |
| 12 | Decisões | Log cronológico de todas as decisões |
| 99 | Contexto LLM | Arquivos gerados automaticamente para injetar em LLMs |

## Convenção de commits

Exemplos rápidos (Brain). Tipos por repo e cenários do dia a dia: **`04-infraestrutura/REPOS-E-FLUXO-GIT.md`**.

```
feat(produto): adiciona feature X
decision(tecnico): escolha do banco de dados  
fix(n8n): corrige fluxo de onboarding
docs(marketing): atualiza estratégia Q2
prompt(llm): novo system prompt de atendimento
metrics(site): atualiza KPIs do mês
refactor(site): nova estrutura de checkout
```
