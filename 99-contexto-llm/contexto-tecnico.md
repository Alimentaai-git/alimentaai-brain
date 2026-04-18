# AlimentaAI — Contexto Técnico
> Gerado em 2026-04-18 01:29 UTC

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

- **Tipo**: Self-hosted (instância com webhooks públicos).
- **Painel / hosting**: Easypanel (padrão de hostname `*.easypanel.host` para webhooks — detalhes exatos de URL e paths **apenas** em documentação interna, não neste repositório público se forem considerados sensíveis).
- **Versão**: inferir no painel n8n (export não fixa versão no root JSON analisado).

## Integrações configuradas

| Serviço | Tipo de integração | Uso no workflow |
|---------|-------------------|-----------------|
| Evolution / UAZAPI | Webhook de entrada + HTTP Request saída | Mensagens WhatsApp; `BaseUrl` tipo `https://alimentaai.uazapi.com` no payload |
| Supabase | Nó Supabase + Supabase Tool + Vector Store | Clientes, `refeicoes`, RAG; credencial nomeada **Alimentaai** |
| Postgres (nó nativo n8n) | `n8n-nodes-base.postgres` | **Remarketing** (`REMARKETING - POS CTA`, `REMARKETING - TBF`): consultas a leads e updates de estado do funil (credencial Postgres separada da credencial “Alimentaai” se assim estiver configurado no editor) |
| Redis | Nó Redis | Fila / buffer de mensagens por telefone |
| Postgres | Chat Memory (LangChain) | Memória de conversa do agente (`Postgres Chat Memory`, `Chat Memory Manager`) |
| Google Gemini (PaLM API) | LangChain node | Análise de imagem (`Analyze image1`) |
| OpenRouter | LangChain Chat Model | Modelo `google/gemini-2.5-flash` no agente |
| OpenAI | Embeddings (LangChain) | Vector store / RAG |
| LangChain | Agent, Memory Manager, tools | Orquestração do `agente_refeicao` |

## Credenciais

- **NÃO** armazenar segredos neste repositório Markdown nem no JSON exportado.
- No n8n: credenciais **Redis**, **Supabase**, **Postgres** (memória + remarketing), **OpenRouter**, **Google Gemini**, **OpenAI**, e tokens de API WhatsApp/instância Evolution.

## Artefactos

| Local | Descrição |
|--------|-----------|
| [`workflow-export.json`](./workflow-export.json) (pasta **`03-n8n`** do Brain) | Referência sanitizada do fluxo principal de atendimento: prompts, tools e ligações com parâmetros úteis para revisão — **sem** `pinData`, `sk-*` nem tokens de instância. |
| Repo [**alimentaai-n8n**](https://github.com/Alimentaai-git/alimentaai-n8n) | Um JSON por workflow em produção (ex.: `jUpFRGibl0PhTje4O9hGW-alimentaai---novo.json`, remarketing). Útil para IDs, nomes exatos de nós e versão publicada; rever segredos antes de cada push. |
| `alimentaai-n8n/workflow-export.json` (no clone do repo n8n) | Pode ser **placeholder** mínimo até ser substituído por export completo — não confundir com o `workflow-export.json` rico do Brain. |


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

