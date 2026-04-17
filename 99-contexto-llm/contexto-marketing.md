# AlimentaAI — Contexto Marketing
> Gerado em 2026-04-17 23:13 UTC

---
## 00-identidade/CONTEXTO.md

# Identidade — Contexto

## Público-alvo principal

Pessoas que querem **emagrecer, ganhar massa ou comer melhor** sem se perder em apps complexos ou em consultas presenciais caras. Valorizam **conversar no WhatsApp**, ter plano **ajustado em tempo real** e acompanhar evolução (incluindo **fotos de refeição** que viram interpretação de macros e calorias no fluxo do produto). Perfil Brasil: linguagem **pt-BR**, tom próximo e incentivo à consistência sem culpa.

## Dores que resolvemos

- **Fricção dos apps de dieta**: abrir app várias vezes ao dia, buscar alimentos em listas enormes, ajustar gramas manualmente e gastar muitos minutos só para registrar uma refeição.
- **Planos rígidos que não cabem na vida real**: imprevistos (jantar fora, família, evento) derrubam o plano; falta alguém que **reorganize o dia** sem “começar do zero”.
- **Custo e acesso**: nutrição de qualidade parece inacessível; o AlimentaAI posiciona acompanhamento contínuo **no canal que a pessoa já usa** (WhatsApp), com **teste sem cartão** e **sem fidelidade** onde o produto assim o comunica.

## Proposta de valor

**Nutrição guiada por IA no WhatsApp** — plano personalizado que **se adapta ao que aconteceu** (incluindo ajustes após “exagerou” ou mudou o dia), mais **registro e leitura de refeições** (foto do prato → interpretação do que comeu) e **painel** para metas e histórico, conforme o ecossistema do produto.

Em uma linha (alinhada à landing): *Seu nutricionista no WhatsApp, com plano ajustado em tempo real — sem app extra, sem consulta cara e sem complicação.*

## Tom de voz

- **Brasileiro, direto e acolhedor** — “beleza”, “sem culpa”, “é assim que funciona de verdade”, celebração de pequenas vitórias.
- **Claro sobre limites** — se não houver dado no contexto (produto, política, saúde), dizer honestamente; não inventar orientação clínica individual.
- **Motivador sem ser grosseiro** — empurra consistência, não vergonha; erros do dia viram **ajuste**, não julgamento eterno.
- **Evitar** — tom corporativo frio, jargão médico excessivo sem necessidade, promessas milagrosas (“em X dias garantido”).

## O que NÃO somos

- **Não somos substituto de médico ou nutricionista presencial** para casos que exijam avaliação clínica presencial, exames ou patologias específicas — somos ferramenta de hábito e acompanhamento no modelo do produto.
- **Não somos app de contagem genérico** que obriga microgerenciar cada grama no silêncio; o diferencial é **conversa + IA + WhatsApp** (e painel quando aplicável).
- **Não somos conteúdo de choque ou restrição extrema** — evitamos linguagem que normalize transtorno alimentar ou culpa pesada.


---
## 05-marketing/MAPA.md

# Marketing — Mapa

## Canais ativos

| Canal | Objetivo | Frequência | Responsável |
|-------|----------|------------|-------------|
| Site (landing) | Conversão e teste | Contínua | *A definir dono* |
| Meta Ads (Pixel) | Remarketing / conversões | Quando `VITE_META_PIXEL_ID` configurado | *A definir* |
| Google Analytics 4 | Medição de funil | Quando `VITE_GA4_MEASUREMENT_ID` configurado | *A definir* |
| WhatsApp (CTA) | Teste e suporte comercial | Contínua | *A definir* |

## Funil de marketing

- **Topo**: tráfego para `/` (orgânico, paid, indicação — detalhar em campanhas).
- **Meio**: prova social e demos de conversa; secção “Por que você sempre desiste?” contrastando apps tradicionais vs. AlimentaAI.
- **Fundo**: `/assinar` com planos e Stripe; parâmetros `?src=` e `?ref=` para atribuição e checkout com utilizador já referenciado.

## Calendário editorial

- *Fora do repositório do site — ligar Notion/planilha aqui quando existir.*


---
## 05-marketing/CONTEXTO.md

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


---
## 06-clientes/MAPA.md

# Clientes — Mapa

## Personas

### Persona 1 — “Exausta de apps de dieta”

- **Perfil**: Adulto que já tentou vários apps de contagem de calorias; usa smartphone no dia a dia; quer resultado sem microgestão.
- **Dor principal**: Abrir app várias vezes ao dia; procurar alimentos em listas longas; ajustar gramas à mão; gastar vários minutos só para registar um almoço simples.
- **Como nos encontrou**: Orgânico ou anúncio (a confirmar em dados) — landing `/`.
- **O que mais valoriza**: **100% no WhatsApp**, plano que **se adapta** quando o dia foge ao planeado, linguagem sem culpa excessiva.
- **Maior objeção de compra**: “Será mais um serviço que abandono?” — resposta na copy: teste grátis sem cartão onde comunicado, cancelamento simples.

### Persona 2 — “Vida real imprevisível”

- **Perfil**: Pessoa com eventos sociais, família, viagens; precisa de flexibilidade, não de plano rígido que “estraga” com um jantar fora.
- **Dor principal**: Culpa e sensação de “recomeçar do zero” após escorregar; falta de acompanhamento humano/IA que **reorganize o dia**.
- **Como nos encontrou**: Indicação ou redes (a confirmar).
- **O que mais valoriza**: Ajustes em **tempo real**; mensagens estilo “sem problema, amanhã equilibramos” alinhadas à demo da landing.
- **Maior objeção de compra**: Preço vs. nutricionista presencial — contrapor com **custo por dia** baixo e conveniência.

## Segmentos de clientes

| Segmento | Tamanho estimado | Característica principal |
|----------|------------------|---------------------------|
| Perda de peso | *A medir* | Foco em déficit e consistência |
| Ganho de massa / performance | *A medir* | Foco em proteína e calorias |
| Reeducação alimentar geral | *A medir* | Foco em hábito e simplicidade |

