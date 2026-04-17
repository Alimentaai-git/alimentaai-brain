# Preços — Stack

## Ferramentas de cobrança

| Ferramenta | Uso |
|------------|-----|
| Stripe | Checkout em sessão (`startStripeCheckout`); redirecionamento do browser para pagamento hospedado |
| Supabase Edge Function | `assinar-lead` — cria/prepara referência (`refId`) para o checkout quando o fluxo não traz `ref` válido na URL |

## Como o pagamento flui pelos sistemas

1. Utilizador escolhe plano em `/assinar` (ciclo: mensal / trimestral / anual).
2. Se não existir `ref` UUID válido na query: pede **nome + WhatsApp**, chama **POST** à função `assinar-lead` com `apikey` publishable e recebe `refId`.
3. Front chama `startStripeCheckout` com `billingCycle`, `refId` / `ref`, `source`, etc.
4. Browser redireciona para **Stripe Checkout**; sucesso leva a `/checkout/sucesso`; cancelamento pode voltar com `?checkout=canceled`.

Secrets (Stripe secret, keys Supabase service) **não** ficam no Brain — apenas no backend e `.env` seguros.
