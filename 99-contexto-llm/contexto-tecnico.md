# AlimentaAI — Contexto Técnico
> Gerado em 2026-04-17 20:09 UTC

---
## 02-site/STACK.md

# Site — Stack

## Tecnologias

| Tecnologia | Uso |
|------------|-----|
| Vite | Build e dev server (`vite`, `vite build`) |
| React 18 | UI |
| TypeScript | Tipagem |
| react-router-dom | Rotas SPA |
| Tailwind CSS | Estilos utilitários |
| Radix UI / shadcn | Primitivos acessíveis (accordion, dialog, tabs, etc.) |
| @supabase/supabase-js | Auth, dados, chamadas a APIs/Edge |
| @tanstack/react-query | Cache e fetching |
| react-hook-form + Zod | Formulários e validação |
| Stripe | Checkout (sessão via `startStripeCheckout` no front) |
| Font Awesome | Ícones na landing e fluxos |
| Highcharts + Recharts | Gráficos no dashboard (dependências presentes) |
| date-fns | Datas |

## Hospedagem e deploy

- O projeto é uma **SPA Vite**; o repositório **não fixa** URL pública de produção nem provedor (Vercel, Netlify, Cloudflare Pages, etc.). Documentar aqui quando a equipa tiver o domínio oficial e o pipeline de deploy.

## Repositório

- Código fonte do site/app: **https://github.com/Alimentaai-git/site-alimentaai.git** (nome local do clone: `alimend-assist`).


---
## 03-n8n/STACK.md

# N8N — Stack

## Configuração
- **Tipo**: Self-hosted / Cloud
- **Versão**: 
- **URL**: 

## Integrações configuradas
| Serviço | Tipo de integração | Fluxos que usam |
|---|---|---|
| | | |

## Credenciais
<!-- NÃO armazene credenciais aqui. Documente onde elas ficam. -->


---
## 04-infraestrutura/STACK.md

# Infraestrutura — Stack

## Serviços em uso
| Serviço | Função | Plano |
|---|---|---|
| | | |

## DNS e domínios
<!-- Onde estão registrados, quem gerencia -->

## Monitoramento e alertas
<!-- Como sabemos quando algo quebra -->


---
## 08-integracoes/STACK.md

# Integrações — Stack

## Webhooks ativos

| Endpoint / origem | Origem | Destino | Evento |
|---------------------|--------|---------|--------|
| *A documentar no backend* | Stripe | Supabase / serviço interno | `checkout.session.completed`, etc. |
| *A documentar* | WhatsApp / n8n | Supabase ou API | Mensagens e automações |

O repositório **front** do site não lista webhooks servidor — completar esta tabela quando o backend estiver mapeado.

## Autenticação entre sistemas

- **Browser → Supabase**: `anon` / publishable key no cliente; sessão de utilizador via Supabase Auth.
- **Browser → Edge Function `assinar-lead`**: header `apikey` com a mesma publishable key (padrão Supabase).
- **Stripe Checkout**: sessão criada no servidor ou via função exposta ao cliente conforme implementação de `startStripeCheckout` — **sem** expor secret key no Brain.

## Onde ficam os secrets e API keys

- Ficheiro **`.env`** local (gitignored) no projeto do site: `VITE_SUPABASE_URL`, `VITE_*` para analytics, `VITE_WHATSAPP_NUMBER`, etc.
- **GitHub Secrets** / painel Supabase / Stripe Dashboard para produção — nunca commitar valores neste repositório Markdown.

