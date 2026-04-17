# Produto — Stack

## Tecnologias do produto

| Tecnologia | Uso | Versão (package.json) |
|------------|-----|------------------------|
| React | UI | ^18.3.1 |
| Vite | Build | (devDependency @vitejs/plugin-react-swc) |
| TypeScript | Tipagem | devDependency |
| Supabase JS | Cliente browser, auth, RPC/REST, chamadas a Functions | ^2.76.1 |
| TanStack Query | Data fetching | ^5.83.0 |
| Stripe | Checkout via sessão no browser | integração em `src/lib/checkoutSession` |
| Zod + react-hook-form | Validação de formulários | conforme package.json |
| Highcharts / Recharts | Visualização no dashboard | conforme package.json |

## Dependências externas

| Serviço | Função |
|---------|--------|
| Supabase | Auth, base de dados, **Edge Functions** (ex.: `assinar-lead` via `supabaseEdgeFunctionUrl`) |
| Stripe | Pagamentos Checkout |
| Meta (Facebook) Pixel | Opcional — conversões / PageView |
| Google Analytics 4 | Opcional — eventos de funil |

## Repositórios relacionados

- **Site / app**: https://github.com/Alimentaai-git/site-alimentaai.git  
- **Brain (contexto)**: https://github.com/Alimentaai-git/alimentaai-brain.git  
