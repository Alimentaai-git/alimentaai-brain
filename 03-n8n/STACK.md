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
| Postgres (nó nativo n8n) | `n8n-nodes-base.postgres` | **Remarketing** (`REMARKETING - POS CTA`, `REMARKETING - TBF`): consultas a leads e updates de estado do funil (credencial Postgres separada da credencial “Alimentaai” se assim estiver configurado no editor) |
| Redis | Nó Redis | Fila / buffer de mensagens por telefone |
| Postgres | Chat Memory (LangChain) | Memória de conversa do agente (`Postgres Chat Memory`, `Chat Memory Manager`) |
| Google Gemini (PaLM API) | LangChain node | Análise de imagem (`Analyze image1`) |
| OpenRouter | LangChain Chat Model | Modelo `google/gemini-2.5-flash` no agente |
| OpenAI | Embeddings (LangChain) | Vector store / RAG |
| LangChain | Agent, Memory Manager, tools | Orquestração do `agente_refeicao` |

## Credenciais

- **NÃO** armazenar segredos neste repositório Markdown nem no JSON exportado.
- No n8n: credenciais **Redis**, **Supabase**, **Postgres** (memória + remarketing), **OpenRouter**, **Google Gemini**, **OpenAI**, e tokens de API WhatsApp/instância Evolution.

## Artefactos

| Local | Descrição |
|--------|-----------|
| [`workflow-export.json`](./workflow-export.json) (pasta **`03-n8n`** do Brain) | Referência sanitizada do fluxo principal de atendimento: prompts, tools e ligações com parâmetros úteis para revisão — **sem** `pinData`, `sk-*` nem tokens de instância. |
| Repo [**alimentaai-n8n**](https://github.com/Alimentaai-git/alimentaai-n8n) | Um JSON por workflow em produção (ex.: `jUpFRGibl0PhTje4O9hGW-alimentaai---novo.json`, remarketing). Útil para IDs, nomes exatos de nós e versão publicada; rever segredos antes de cada push. |
| `alimentaai-n8n/workflow-export.json` (no clone do repo n8n) | Pode ser **placeholder** mínimo até ser substituído por export completo — não confundir com o `workflow-export.json` rico do Brain. |
