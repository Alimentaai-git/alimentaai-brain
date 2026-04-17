# Marketing — Contexto

## Estratégia atual

- **Mensagem principal (hero)**: “Seu nutricionista no WhatsApp” com âncora de preço acessível (“por menos de R$ 1 por dia” quando o cálculo do plano trimestral o suporta).
- **Subpromessa**: emagrecer, ganhar massa ou comer melhor com plano **ajustado em tempo real**, sem app extra nem consulta cara.
- **Prova na página de planos**: badges de copy (“Escolhido por 73% dos usuários”, “Maior economia”) — tratar como **mensagem de marketing** no site, não como estatística auditada neste documento.
- **Canais técnicos**: Meta Pixel e GA4 opcionais via `VITE_META_PIXEL_ID` e `VITE_GA4_MEASUREMENT_ID` (ver `02-site/MAPA.md`).

## O que já testamos e não funcionou

- *A preencher com dados reais de campanha / retrospectivas.*

## O que está funcionando

- *A preencher com métricas por canal (CPL, ROAS, etc.) quando disponíveis.*

## Identidade visual — diretrizes principais

- Marca **AlimentaAI** com wordmark “Alimenta” em gradiente + “AI” em cor de texto.
- Uso consistente de **verde/teal** (HSL) para primário e secundário; fundo claro com ruído suave na hero.
- CTAs em **pill** com gradiente primary→secondary; ícone de presente no “Testar grátis”.
- Tom visual: moderno, saúde/digital, sem exagero “clínico frio”.

## Paleta de cores

Valores em **HSL** (componentes `h s l` sem `hsl()` — o Tailwind do site usa `hsl(var(--token))`).

| Token | HSL `:root` | Uso |
|-------|-------------|-----|
| `--background` | `0 0% 100%` | Fundo geral (tema claro) |
| `--foreground` | `160 84% 8%` | Texto principal |
| `--primary` | `160 84% 39%` | Marca, CTAs, ênfase |
| `--primary-foreground` | `0 0% 100%` | Texto sobre primário |
| `--secondary` | `160 61% 65%` | Gradientes, apoio visual |
| `--secondary-foreground` | `160 84% 8%` | Texto sobre secundário |
| `--muted` | `160 30% 96%` | Fundos suaves |
| `--muted-foreground` | `160 10% 45%` | Texto secundário |
| `--accent` | `160 100% 45%` | Destaques |
| `--accent-foreground` | `0 0% 100%` | Texto sobre accent |
| `--destructive` | `0 84.2% 60.2%` | Erros / aviso |
| `--border` / `--input` / `--ring` | `160 30% 90%` / idem / `160 84% 39%` | Limites e foco |

Tema **`.dark`**: ver mesmo ficheiro no site para valores noturnos.

## Tipografia

| Fonte | Peso | Uso |
|-------|------|-----|
| Inter | 300–900 (Google Fonts no `index.html` do site) | Títulos e corpo |
