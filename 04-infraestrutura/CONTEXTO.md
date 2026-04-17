# Infraestrutura — Contexto

## Decisões de arquitetura

- **Supabase** como backend único para dados e funções serverless consumidas pelo site e referenciadas no n8n.
- **n8n self-hosted** (Easypanel) para colar **WhatsApp ↔ Redis ↔ LLM ↔ Supabase** sem deployar lógica pesada no site estático.
- **Redis** dedicado ao debounce / fila curta de mensagens no fluxo WhatsApp (não substitui o Postgres do Supabase).

## Custos mensais

| Serviço | Custo | Renovação |
|---------|-------|-----------|
| Supabase | *A preencher* | |
| Stripe | % + fixo conforme faturação | |
| n8n / Easypanel / VPS | *A preencher* | |
| Redis | *A preencher* | |
| UAZAPI / Evolution | *A preencher* | |
| OpenRouter + Gemini + OpenAI | *A preencher* (uso variável) | |

## Pontos de atenção

- **Segurança**: exports do n8n não devem conter `pinData` com PII nem chaves `sk-*` — ver incidente corrigido com `03-n8n/workflow-export.json` sanitizado.
- **Disponibilidade**: webhook n8n é **ponto único** de entrada da automação WhatsApp; monitorizar uptime e TLS.
- **Rotação de segredos**: qualquer chave que tenha estado em Git público deve ser **rotacionada** no fornecedor.
