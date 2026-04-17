# AlimentaAI — Contexto Produto
> Gerado em 2026-04-17 23:46 UTC

---
## 01-produto/MAPA.md

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


---
## 01-produto/CONTEXTO.md

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


---
## 01-produto/precos/MAPA.md

# Preços — Mapa

## Estrutura de planos

Valores em **BRL**, fonte: `PLAN_CATALOG` no código do site.

| Plano | Cobrança (código) | Valor no catálogo | Stripe `content_id` |
|-------|-------------------|-------------------|------------------------|
| Mensal | `monthly` | **R$ 27,90** (`amount: 27.9`) | `alimentaai_plan_monthly` |
| Trimestral | `quarterly` | **R$ 75,90** total (`amount: 75.9`) | `alimentaai_plan_quarterly` |
| Anual | `yearly` | **R$ 229,90** total (`amount: 229.9`) | `alimentaai_plan_yearly` |

## Apresentação na UI (`/assinar`)

| Plano | Destaques de copy (componente de vendas) |
|-------|---------------------------------------------|
| Trimestral | Badge “Escolhido por 73% dos usuários”; preço/mês = total÷3; “menos de X por dia” (total÷90); benefícios: plano 100% personalizado, ajustes ilimitados, nutricionista IA 24h no WhatsApp, receitas práticas, relatório semanal |
| Mensal | Preço/mês explícito; “X por dia” (total÷30); benefícios: plano personalizado, ajustes quando precisar, cancele quando quiser |
| Anual | Badge “Maior economia”; preço/mês = total÷12; “X por dia” (total÷365); copy “Você economiza R$ 129/ano”; benefícios: tudo do trimestral, 12 meses de acompanhamento, prioridade no suporte, novidades em primeira mão |

> O texto “73%” e “R$ 129/ano” vêm da **copy de marketing** no front — não substituem relatório financeiro ou estudo de mercado.

## Histórico de preços

- A documentar quando houver mudança de valores em `PLAN_CATALOG` / Stripe — registar data e motivo aqui ou em `12-decisoes/`.


---
## 10-roadmap/MAPA.md

# Roadmap — Mapa

## Horizonte de tempo

### 🔴 Agora (próximas 4 semanas)
- [ ] 
- [ ] 

### 🟡 Em breve (próximos 3 meses)
- [ ] 
- [ ] 

### 🟢 Futuro (3–12 meses)
- [ ] 
- [ ] 

### 🔵 Visão (12+ meses)
<!-- Onde queremos estar no longo prazo -->

## Atualizado em
<!-- Data da última revisão do roadmap -->

