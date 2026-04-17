# Integrações — Contexto

## Fluxo principal ponta a ponta
<!-- Descreva o caminho completo de um lead/cliente pelo ecossistema -->
1. 
2. 
3. 

## Pontos de falha conhecidos
<!-- Onde as integrações costumam quebrar -->

## Dependências críticas
<!-- Se X cair, o que mais para? -->

## Como usar o Brain como contexto em outros sistemas

### No N8N
```
Nó: HTTP Request → GET
URL: https://raw.githubusercontent.com/Alimentaai-git/alimentaai-brain/main/99-contexto-llm/contexto-completo.md
→ Injete como system prompt no nó LLM seguinte
```

### Em qualquer sistema via API
```javascript
const res = await fetch('https://raw.githubusercontent.com/Alimentaai-git/alimentaai-brain/main/99-contexto-llm/contexto-completo.md')
const brain = await res.text()
// use brain como system prompt
```
