# N8N — Contexto

## Por que n8n

Orquestração visual de **WhatsApp (Evolution / UAZAPI)** com **Redis** (debounce / fila curta), **Supabase** (dados e vector store), **vários LLMs** (Gemini para imagem, OpenRouter para chat do agente, OpenAI para embeddings no RAG) e **Postgres** para memória de conversa — num único fluxo versionável.

## Fluxos mais críticos

- **Webhook principal de mensagens**: se falhar, o cliente não recebe resposta automática.
- **Agente `agente_refeicao` + ferramentas Supabase** (ex.: persistência em `refeicoes`): núcleo do produto “macros por refeição”.
- **Redis** na agregação de mensagens: se Redis estiver indisponível ou com TTL errado, mensagens podem fragmentar-se ou atrasar-se.

## Pontos de atenção

- **Credenciais**: nunca embutir `sk-` ou tokens de instância no JSON exportado — usar **Credentials** do n8n e reexportar sem segredos (como em `workflow-export.json`).
- **Custos**: cada mensagem pode acionar Gemini, OpenRouter e embeddings; monitorizar quotas.
- **Dependências externas**: Supabase, Redis, host UAZAPI (`BaseUrl` típico `https://alimentaai.uazapi.com` no payload), e instância Evolution devem estar saudáveis em cadeia.
- **Manutenção**: nós placeholder (`Replace Me`, `No Operation`) devem ser tratados ou removidos no editor.

## Como buscar contexto do Brain no n8n

```
Nó: HTTP Request
Método: GET  
URL: https://raw.githubusercontent.com/Alimentaai-git/alimentaai-brain/main/99-contexto-llm/contexto-completo.md
```

Injete o resultado como system prompt em qualquer nó LLM do fluxo.

## Segurança (lembrete)

Se um export antigo continha **chaves ou PII**, rodar as chaves no fornecedor e **não** voltar a commitar `pinData` nem API keys em nós `Set`.
