# Integrações — Mapa

## Diagrama do ecossistema

```
[Visitante] ──► [Site SPA] ──► [Stripe] + [Supabase Edge]
                    │
                    └──► [Meta / GA4]

[WhatsApp] ◄──► [Evolution / UAZAPI] ──webhook──► [n8n]
                                              │
                    ┌─────────────────────────┼─────────────────────────┐
                    ▼                         ▼                         ▼
              [Redis buffer]            [Supabase DB + Vector]     [OpenRouter / Gemini / OpenAI]
                    │                         │
                    └────────► [LLM Agent] ◄───┘
                                    │
                                    └──► [HTTP] ──► [Evolution / UAZAPI] ──► [WhatsApp]

[BRAIN] ◄──── contexto para LLM (raw GitHub URL) ◄── usado pelo n8n e outros
```

## Mapa de integrações

| De | Para | O que passa | Como | Crítico? |
|----|------|-------------|------|----------|
| Site | Supabase | Auth, dados, `assinar-lead` | HTTPS + anon key | Sim |
| Site | Stripe | Checkout de plano | Redirect sessão | Sim |
| Site | Meta / GA4 | Eventos de funil | Browser + `VITE_*` | Não |
| Evolution / UAZAPI | n8n | Payload mensagem / instância | Webhook POST JSON | Sim |
| n8n | Redis | Mensagens agregadas por chave | Redis protocol | Sim |
| n8n | Supabase | Queries, tools, vector store | REST / API Supabase | Sim |
| n8n | OpenRouter / Google / OpenAI | Prompts, imagem, embeddings | HTTPS API | Sim |
| n8n | Evolution / UAZAPI | Envio de texto / mídia | HTTP Request | Sim |
| n8n | Brain (GitHub raw) | `contexto-completo.md` | GET HTTP | Recomendado para qualidade das respostas |

## APIs externas

| API | Uso | Quem chama | Documentação |
|-----|-----|------------|----------------|
| Supabase | DB, Auth, Edge Functions, Storage (conforme projeto) | Site, n8n | docs.supabase.com |
| Stripe | Pagamentos | Site | stripe.com/docs |
| UAZAPI / Evolution | WhatsApp Business API layer | n8n | Documentação do fornecedor UAZAPI |
| OpenRouter | Chat completions | n8n (LangChain) | openrouter.ai |
| Google Gemini | Visão / imagem | n8n | Google AI |
| OpenAI | Embeddings | n8n | platform.openai.com |
