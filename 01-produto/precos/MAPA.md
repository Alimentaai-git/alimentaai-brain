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
