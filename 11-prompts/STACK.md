# Prompts — Stack

## Modelos LLM em uso
| Modelo | String do modelo | Usado para | Custo aprox. |
|---|---|---|---|
| Claude Sonnet | claude-sonnet-4-20250514 | | |
| | | | |

## Como injetar o Brain como contexto
```
System prompt padrão com Brain:

Você é um assistente especialista no ecossistema AlimentaAI.
Use o contexto abaixo como sua fonte de verdade sobre o produto,
estratégia, clientes e decisões tomadas.

---CONTEXTO ALIMENTAAI---
{conteúdo de 99-contexto-llm/contexto-completo.md}
---FIM DO CONTEXTO---

Baseie todas as respostas nesse contexto.
Se não encontrar a informação, diga claramente.
```

## Ferramentas de gestão de prompts
<!-- Promptlayer, LangSmith, planilha, ou só este repositório? -->
