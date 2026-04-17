# Integrações — Contexto

## Fluxo principal ponta a ponta (site → pagamento)

Fluxo documentado a partir da página **`/assinar`** no site [site-alimentaai](https://github.com/Alimentaai-git/site-alimentaai):

1. **Entrada**: utilizador abre `/assinar` ou `/assinatura`. Query opcional `?src=` (campanha) e `?ref=` (UUID de utilizador/lead já existente).
2. **Validação de `ref`**: se `ref` for um UUID válido, o checkout pode prosseguir **sem** o mini-formulário de nome/WhatsApp.
3. **Criação de lead** (quando não há `ref` válido): utilizador preenche **nome** e **WhatsApp** (normalização para dígitos BR); **POST** à Edge Function Supabase **`assinar-lead`** com header `apikey` (chave publishable) e corpo `telefone` / `user_name`; resposta deve incluir `refId` UUID.
4. **Stripe Checkout**: front chama `startStripeCheckout` com ciclo de faturação (`monthly` | `quarterly` | `yearly`), `refId`/`ref`, `source`, etc.; browser é redirecionado para a URL de sessão Stripe.
5. **Retorno**: sucesso → `/checkout/sucesso`. Cancelamento: Stripe pode devolver com `?checkout=canceled` — o site mostra toast “Pagamento não concluído” e remove o parâmetro da URL.

Passos **fora** deste repositório (WhatsApp bot, n8n, webhooks Stripe no backend) devem ser descritos em `03-n8n/` e na documentação do Supabase quando existirem.

## Pontos de falha conhecidos

- **`assinar-lead` indisponível ou erro**: checkout não abre; toast genérico no front.
- **`ref` inválido** na URL: mensagem pedindo novo link de pagamento.
- **Stripe / sessão**: falhas de rede ou configuração — utilizador vê “Não foi possível abrir o pagamento”.
- **Variáveis `VITE_*` em falta**: analytics não carrega; WhatsApp de teste pode não abrir (`VITE_WHATSAPP_NUMBER` referenciado no fluxo de teste da app).

## Dependências críticas

| Dependência | Impacto se cair |
|-------------|-----------------|
| Supabase (projeto + Functions) | Auth, dados, `assinar-lead`, URLs Edge |
| Stripe | Impossível cobrar novas assinaturas via fluxo atual |
| Domínio / hosting do site | Utilizadores não chegam ao funil |
| Meta / GA4 | Perda de medição — **não** bloqueia o produto |

## Como usar o Brain como contexto em outros sistemas

### No N8N
```
Nó: HTTP Request → GET
URL: https://raw.githubusercontent.com/Alimentaai-git/alimentaai-brain/main/99-contexto-llm/contexto-completo.md
→ Injete como system prompt no nó LLM seguinte
```

### Em qualquer sistema via API
```javascript
const res = await fetch('https://raw.githubusercontent.com/Alimentaai-git/alimentaai-brain/main/99-contexto-llm/contexto-completo.md')
const brain = await res.text()
// use brain como system prompt
```
