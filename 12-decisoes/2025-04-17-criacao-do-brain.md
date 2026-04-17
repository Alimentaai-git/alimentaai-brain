# Criação do Segundo Cérebro no GitHub

**Data**: 2025-04-17  
**Status**: `Aceita`  
**Área**: `Técnico` | `Operacional`  

---

## Contexto
O ecossistema AlimentaAI cresceu com múltiplos repositórios, ferramentas e sistemas
sem um ponto central de contexto e decisões. Conhecimento estava disperso e
inacessível para LLMs e novas ferramentas integradas.

## Problema
- Conhecimento disperso em repositórios separados
- LLMs e ferramentas sem contexto do produto
- Decisões tomadas sem registro → risco de repetir erros
- Difícil onboarding de novos colaboradores ou ferramentas de IA

## Decisão
Criar o repositório `alimentaai-brain` no GitHub como fonte da verdade única,
com estrutura padronizada por área (MAPA + CONTEXTO + STACK) e geração automática
de contexto consolidado para injeção em LLMs.

## Alternativas consideradas
| Alternativa | Por que descartamos |
|---|---|
| Notion | Não versionado, difícil de injetar como contexto via URL |
| Confluence | Pago, overhead de setup, não integra bem com LLMs |
| Google Drive | Sem versionamento semântico, difícil de linkar em sistemas |
| Obsidian | Local, não acessível por outros sistemas |

## Consequências
- Qualquer nova decisão deve ser commitada em `12-decisoes/`
- Mudanças em produto/tech devem atualizar os `.md` da área correspondente
- N8N passa a buscar contexto do Brain antes de chamadas LLM importantes
- GitHub Actions gera `contexto-completo.md` automaticamente a cada commit

## Referências
- Conversa inicial de arquitetura do Brain com Claude (2025-04-17)
