# Produto — Mapa

## Visão geral do produto

Acompanhamento de nutrição/hábito alimentar com **IA no WhatsApp** (conversa, ajustes de plano) e **painel web** para metas e histórico; registro simplificado incluindo **foto da refeição** interpretada como macros/calorias no discurso do produto. Planos pagos com **Stripe**; identidade e auth com **Supabase**.

## Funcionalidades ativas

| Feature | Status | Descrição |
|---------|--------|-----------|
| Landing e marketing | Ativo no código | `/` — hero, demos, FAQ, CTAs |
| Auth (login/registo) | Ativo no código | `/auth` |
| Onboarding “Comece agora” | Ativo no código | `/comece-agora` |
| Dashboard | Ativo no código | `/dashboard` |
| Planos | Ativo no código | `/planos` |
| Assinatura Stripe | Ativo no código | `/assinar`, `/assinatura` + `checkout/sucesso` |
| Onboarding pós-compra | Ativo no código | `/onboarding/revisao`, `/onboarding/ativar-teste` |
| Documentos legais | Ativo no código | privacidade e termos |
| Analytics | Ativo no código (se env configurado) | Meta Pixel + GA4, eventos de checkout/subscribe |
| Teste WhatsApp | Ativo no código | CTA abre WhatsApp (`VITE_WHATSAPP_NUMBER` no `.env`) |

## Funcionalidades planejadas

| Feature | Prioridade | ETA |
|---------|------------|-----|
| A definir pela equipa | — | Documentar em `10-roadmap/` quando houver decisão |

## Fluxo principal do utilizador

1. **Descoberta** → `/`
2. **Interesse** → teste WhatsApp ou `/comece-agora` ou `/planos`
3. **Conta** → `/auth` quando necessário
4. **Compra** → `/assinar` → Stripe → `/checkout/sucesso`
5. **Uso** → `/dashboard` + interação WhatsApp (fora deste repo front)
