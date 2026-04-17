# Preços — Contexto

## Estratégia de precificação

- **Âncora**: trimestral com badge de escolha majoritária e custo-diário baixo vs. percepção de “nutricionista”.
- **Entrada**: mensal com barreira mais baixa e ênfase em cancelamento simples.
- **Upsell / retenção longa**: anual com “maior economia” e benefícios cumulativos listados na página de assinatura.

Tudo acima reflete o **posicionamento implementado no site**, não um benchmark externo anexado.

## Benchmarks do mercado

- **Não preenchidos a partir do repositório do site** — adicionar quando houver pesquisa de concorrentes ou dados internos.

## Decisões tomadas

- Preços e IDs de conteúdo para analytics/checkout vivem centralmente em `src/lib/planCatalog.ts` (valores atuais: 27,9 / 75,9 / 229,9 BRL).
- Eventos Meta (`InitiateCheckout`) e GA4 (`begin_checkout`) usam `contentId` / valor do mesmo catálogo para consistência com Stripe.
