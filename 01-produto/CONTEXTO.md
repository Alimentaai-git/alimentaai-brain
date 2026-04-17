# Produto — Contexto

## Estado atual

- Produto entregue como **SPA** no repositório [site-alimentaai](https://github.com/Alimentaai-git/site-alimentaai) com fluxos de landing, auth, onboarding, dashboard e pagamentos descritos em `01-produto/MAPA.md` e `02-site/MAPA.md`.
- Catálogo de preços e IDs para checkout/analytics centralizados em `planCatalog` (ver `01-produto/precos/`).

## Principais decisões tomadas

- **Checkout Stripe** com sessão criada no cliente via helper dedicado; redirecionamento completo para Stripe.
- **Lead antes do pagamento**: sem `ref` UUID válido, o utilizador preenche nome e WhatsApp e o sistema chama a Edge Function `assinar-lead` para obter `refId` antes do Stripe.
- **Tracking**: eventos alinhados ao `PLAN_CATALOG` para Meta e GA4 no momento de checkout/subscrição.

## Limitações conhecidas

- Comportamento completo dos fluxos WhatsApp e automações **não** está neste repositório front — documentar em `03-n8n/` quando o fluxo estiver descrito noutro sítio.
- Dependência de variáveis `VITE_*` e de projeto Supabase/Stripe corretamente configurados em cada ambiente.

## Feedback dos utilizadores

- **A recolher** — quando houver tickets, NPS ou exportações, resumir aqui ou em `06-clientes/CONTEXTO.md`.

## Próximas evoluções

- **A documentar** em `10-roadmap/` com datas dono — não inferir a partir só do código.
