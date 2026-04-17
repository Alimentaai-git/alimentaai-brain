# Infraestrutura — Mapa

## Arquitetura geral

| Componente | Função | Notas |
|--------------|--------|--------|
| **Site (SPA)** | Landing, auth, dashboard, checkout | Vite/React — ver `02-site/STACK.md`; hosting público a documentar quando fixo |
| **Supabase** | Postgres, Auth, Edge Functions, Storage (conforme projeto) | Usado pelo site e pelo n8n |
| **Stripe** | Pagamentos | Checkout a partir do site |
| **n8n** | Orquestração WhatsApp + LLM | Self-hosted; padrão de deploy observado: **Easypanel** (`*.easypanel.host` para webhooks) |
| **Redis** | Buffer de mensagens no fluxo n8n | Credencial “Redis account” no n8n |
| **Evolution / UAZAPI** | Camada WhatsApp | Ex.: `BaseUrl` `https://alimentaai.uazapi.com` no payload típico (domínio de produto, não segredo) |
| **LLM externos** | OpenRouter, Google Gemini, OpenAI | Chamados a partir do n8n |

Diagrama lógico alinhado a `03-n8n/MAPA.md` e `08-integracoes/MAPA.md`.

## Ambientes

| Ambiente | URL | Uso |
|----------|-----|-----|
| Produção | *A preencher* (domínio do site + projeto Supabase) | Tráfego real |
| Staging | *Opcional* | Testes |
| Dev | `localhost` (site); n8n pode usar execução manual / webhooks de teste | Desenvolvimento |

## Git e repositórios

Proteção da `main` do site, branch `dev`, repos `alimentaai-n8n` / `alimentaai-marketing` e convenção de commits: [**REPOS-E-FLUXO-GIT.md**](REPOS-E-FLUXO-GIT.md).
