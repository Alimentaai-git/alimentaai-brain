# Integrações — Stack

## Webhooks ativos

| Endpoint / origem | Origem | Destino | Evento |
|---------------------|--------|---------|--------|
| *A documentar no backend* | Stripe | Supabase / serviço interno | `checkout.session.completed`, etc. |
| *A documentar* | WhatsApp / n8n | Supabase ou API | Mensagens e automações |

O repositório **front** do site não lista webhooks servidor — completar esta tabela quando o backend estiver mapeado.

## Autenticação entre sistemas

- **Browser → Supabase**: `anon` / publishable key no cliente; sessão de utilizador via Supabase Auth.
- **Browser → Edge Function `assinar-lead`**: header `apikey` com a mesma publishable key (padrão Supabase).
- **Stripe Checkout**: sessão criada no servidor ou via função exposta ao cliente conforme implementação de `startStripeCheckout` — **sem** expor secret key no Brain.

## Onde ficam os secrets e API keys

- Ficheiro **`.env`** local (gitignored) no projeto do site: `VITE_SUPABASE_URL`, `VITE_*` para analytics, `VITE_WHATSAPP_NUMBER`, etc.
- **GitHub Secrets** / painel Supabase / Stripe Dashboard para produção — nunca commitar valores neste repositório Markdown.
