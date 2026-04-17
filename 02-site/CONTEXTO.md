# Site — Contexto

## Objetivo principal do site

**Converter** visitantes em utilizadores: teste de WhatsApp sem fricção, clareza de preço (“menos de R$ 1 por dia” como âncora na hero quando o cálculo do trimestral o permite) e **assinatura** via Stripe. O site também suporta **autenticação** e **painel** para quem já é cliente.

## Estado atual

- Landing em `/` com hero focado em **nutrição no WhatsApp**, plano ajustado em tempo real, **sem app extra** e **sem consulta cara** (copy alinhada ao componente `Index`).
- Destaques de confiança na navegação: **100% no WhatsApp**, **cancele quando quiser**, **teste grátis sem cartão** onde aplicável.
- Checkout e planos vivem em `/assinar` (alias `/assinatura`), com planos mensal, trimestral e anual definidos no código (`PLAN_CATALOG`).
- Fluxo de checkout cancelado: query `?checkout=canceled` mostra toast e limpa o parâmetro da URL.

## Decisões de design e UX tomadas

- **Mobile-first** e demos estilo conversa WhatsApp na home para reduzir abstração do produto.
- **Gradientes** e cores em torno de verde/teal (tokens HSL — ver `05-marketing` e `00-identidade/STACK`).
- **Shadcn/Radix** para componentes acessíveis (accordion, dialog, toast).
- **Proxy Vite** em desenvolvimento para chamadas ao mesmo origin em relação ao Supabase (evitar erros de CORS no dev).

## Principais métricas

- **Ainda não documentadas neste repositório** — preencher quando houver GA4/Meta exportados ou dashboard interno (CTR, conversão por página, CAC).
