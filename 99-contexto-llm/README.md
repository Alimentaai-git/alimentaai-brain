# Contextos para LLM

Esta pasta é **gerada automaticamente** pelo GitHub Actions a cada commit na main.
**Não edite estes arquivos diretamente.**

## Arquivos disponíveis

| Arquivo | Conteúdo | Quando usar |
|---|---|---|
| `contexto-completo.md` | Tudo | Contexto geral, onboarding de novas ferramentas |
| `contexto-produto.md` | Produto + Preços + Roadmap | Decisões de produto, features |
| `contexto-tecnico.md` | Site + N8N + Infra + Integrações | Problemas técnicos, arquitetura |
| `contexto-marketing.md` | Identidade + Marketing + Clientes | Copywriting, campanhas, personas |

## URL base para fetch
```
https://raw.githubusercontent.com/Alimentaai-git/alimentaai-brain/main/99-contexto-llm/ARQUIVO.md
```

## Exemplo de uso no N8N
```
HTTP Request → GET → URL acima → salvar em variável
LLM Node → system prompt = {variavel}
```
