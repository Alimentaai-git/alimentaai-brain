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
