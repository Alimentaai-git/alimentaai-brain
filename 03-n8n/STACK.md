# N8N — Stack

## Configuração

- **Tipo**: Self-hosted (instância com webhooks públicos).
- **Painel / hosting**: Easypanel (padrão de hostname `*.easypanel.host` para webhooks — detalhes exatos de URL e paths **apenas** em documentação interna, não neste repositório público se forem considerados sensíveis).
- **Versão**: inferir no painel n8n (export não fixa versão no root JSON analisado).

## Integrações configuradas

| Serviço | Tipo de integração | Uso no workflow |
|---------|-------------------|-----------------|
| Evolution / UAZAPI | Webhook de entrada + HTTP Request saída | Mensagens WhatsApp; `BaseUrl` tipo `https://alimentaai.uazapi.com` no payload |
| Supabase | Nó Supabase + Supabase Tool + Vector Store | Clientes, `refeicoes`, RAG; credencial nomeada **Alimentaai** |
| Redis | Nó Redis | Fila / buffer de mensagens por telefone |
| Postgres | Chat Memory (LangChain) | Memória de conversa do agente |
| Google Gemini (PaLM API) | LangChain node | Análise de imagem (`Analyze image1`) |
| OpenRouter | LangChain Chat Model | Modelo `google/gemini-2.5-flash` no agente |
| OpenAI | Embeddings (LangChain) | Vector store / RAG |
| LangChain | Agent, Memory Manager, tools | Orquestração do `agente_refeicao` |

## Credenciais

- **NÃO** armazenar segredos neste repositório Markdown nem no JSON exportado.
- No n8n: credenciais **Redis**, **Supabase**, **OpenRouter**, **Google Gemini**, **OpenAI**, e tokens de API WhatsApp/instância Evolution.

## Artefactos

| Ficheiro | Descrição |
|----------|-----------|
| [`workflow-export.json`](./workflow-export.json) | Export sanitizado (sem `pinData`, sem `sk-proj-*`, tokens de instância redigidos) |
