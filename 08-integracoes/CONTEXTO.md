# Integrações — Contexto

## Fluxo principal ponta a ponta (site → pagamento)

Fluxo documentado a partir da página **`/assinar`** no site [site-alimentaai](https://github.com/Alimentaai-git/site-alimentaai):

1. **Entrada**: utilizador abre `/assinar` ou `/assinatura`. Query opcional `?src=` (campanha) e `?ref=` (UUID de utilizador/lead já existente).
2. **Validação de `ref`**: se `ref` for um UUID válido, o checkout pode prosseguir **sem** o mini-formulário de nome/WhatsApp.
3. **Criação de lead** (quando não há `ref` válido): utilizador preenche **nome** e **WhatsApp** (normalização para dígitos BR); **POST** à Edge Function Supabase **`assinar-lead`** com header `apikey` (chave publishable) e corpo `telefone` / `user_name`; resposta deve incluir `refId` UUID.
4. **Stripe Checkout**: front chama `startStripeCheckout` com ciclo de faturação (`monthly` | `quarterly` | `yearly`), `refId`/`ref`, `source`, etc.; browser é redirecionado para a URL de sessão Stripe.
5. **Retorno**: sucesso → `/checkout/sucesso`. Cancelamento: Stripe pode devolver com `?checkout=canceled` — o site mostra toast “Pagamento não concluído” e remove o parâmetro da URL.

Passos **fora** deste repositório (WhatsApp bot, n8n, webhooks Stripe no backend) devem ser descritos em `03-n8n/` e na documentação do Supabase quando existirem.

## Mensagens WhatsApp (automação)

Fluxo de alto nível documentado a partir do export em [`03-n8n/workflow-export.json`](../03-n8n/workflow-export.json):

1. **Evolution / UAZAPI** envia **POST** para o webhook do n8n com corpo JSON (`EventType`, `BaseUrl`, `instanceName`, dados de `chat` e `message`, etc.).
2. **Normalização**: nós `Set` / `Code` extraem telefone, texto, tipo de mensagem e ignoram mensagens enviadas pela própria API ou pelo “eu” (`fromMe` / `wasSentByApi`).
3. **Redis**: leitura/escrita de mensagens por telefone e esperas controladas para agrupar burst de texto.
4. **Supabase**: obtenção do registo de cliente (`getClient` e variantes) com credencial de projeto **Alimentaai**.
5. **Ramificação**: mensagem de **imagem** (ou mídia) segue conversão e análise com **Google Gemini**; mensagem de **texto** segue para o agente **LangChain** (`agente_refeicao`) com modelo via **OpenRouter** (`google/gemini-2.5-flash`).
6. **Memória e ferramentas**: Postgres (memória de chat), ferramentas Supabase (ex.: `registrar_refeicao` na tabela `refeicoes`), vector store + embeddings para RAG.
7. **Resposta**: pedidos HTTP de volta à API UAZAPI/Evolution para o utilizador receber mensagem no WhatsApp.

Tokens de instância e chaves de API **não** devem aparecer em repositórios — apenas no n8n **Credentials** e nos serviços de origem.

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
| n8n (webhooks) | Automatização WhatsApp para de responder |
| Redis (buffer n8n) | Mensagens podem duplicar-se ou atrasar-se |
| Evolution / UAZAPI | Entrada e saída de WhatsApp indisponíveis |

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
