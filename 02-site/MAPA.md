# Site — Mapa

## Estrutura de páginas

| Página | Rota | Objetivo |
|--------|------|----------|
| Landing (home) | `/` | Apresentar proposta de valor, demos WhatsApp, FAQ, CTAs para teste e assinatura |
| Autenticação | `/auth` | Login/registo; reforço de benefício (foto → macros, WhatsApp + painel) |
| Comece agora | `/comece-agora` | Onboarding inicial do lead (dados para começar) |
| Dashboard | `/dashboard` | Área logada — acompanhamento, gráficos, histórico |
| Planos | `/planos` | Página de planos (catálogo de oferta) |
| Assinar | `/assinar`, `/assinatura` | Escolha de ciclo (mensal/trimestral/anual), captura lead se necessário, checkout Stripe |
| Checkout sucesso | `/checkout/sucesso` | Pós-pagamento Stripe |
| Onboarding revisão | `/onboarding/revisao` | Passo pós-compra |
| Ativar teste | `/onboarding/ativar-teste` | Fluxo de ativação de teste |
| Política de privacidade | `/politica-de-privacidade` | Legal |
| Termos de uso | `/termos-de-uso` | Legal |
| 404 | `*` | Página não encontrada |

Fonte de rotas: repositório do site (`App.tsx` / router).

## Funil de conversão

1. **Topo**: visitante chega à `/` (orgânico, paid, indicação — canal a documentar em marketing).
2. **Meio**: interação com CTAs “Testar grátis” / WhatsApp e leitura de prova social na landing.
3. **Fundo**: `/assinar` (ou `/planos` → assinatura) com Stripe; parâmetros opcionais `?src=` (campanha) e `?ref=` (UUID de utilizador/lead já criado).
4. **Pós-compra**: `/checkout/sucesso` e rotas `/onboarding/*` conforme implementação.

Fluxo alternativo: `/comece-agora` → recolha de dados → continuação para auth/dashboard conforme produto.

## Integrações ativas no site

| Integração | Como entra | Notas |
|------------|------------|--------|
| Meta Pixel | `VITE_META_PIXEL_ID` no `.env`; carregamento em `initAnalytics()` | Eventos ex.: `InitiateCheckout` com `content_ids` do plano |
| Google Analytics 4 | `VITE_GA4_MEASUREMENT_ID` no `.env` | Eventos ex.: `begin_checkout`, subscrição alinhada ao catálogo |
| Supabase | Cliente JS + Edge Functions (ex.: `assinar-lead`) | URL e keys via variáveis de ambiente |
| Stripe | Checkout hospedado (`startStripeCheckout`) | Redirecionamento para pagamento; retorno com query `checkout=canceled` tratada em `/assinar` |

Não documentar valores secretos de API no Brain — apenas nomes de variáveis e comportamento.
