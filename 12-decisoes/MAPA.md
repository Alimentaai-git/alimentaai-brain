# Decisões — Mapa

## O que é esta área

Registo **versionado** de decisões relevantes do ecossistema AlimentaAI (produto, técnico, marketing, operacional, financeiro). Cada ficheiro é uma decisão concluída ou em discussão, com contexto explícito para não “perder o porquê” no tempo.

## Fluxo sugerido

1. **Ideia ou tensão** — surge uma dúvida que afeta direção, stack, preço ou processo.
2. **Rascunho** — copiar [`_template.md`](./_template.md), renomear e preencher (pode começar em `Proposta`).
3. **Revisão** — alinhar com quem decide; ajustar alternativas e consequências.
4. **Commit** — ficheiro `YYYY-MM-DD-slug-descritivo.md` na pasta `12-decisoes/`.
5. **Propagação** — quando a decisão muda comportamento real, atualizar o `CONTEXTO.md` (ou `STACK.md`) da área correspondente (`00`–`11`).

## Convenção de nomes

```
YYYY-MM-DD-slug-curto-em-kebab-case.md
```

Exemplo: `2025-04-17-criacao-do-brain.md`

Evitar espaços e caracteres especiais; o slug deve ser legível em URLs e logs.

## Relação com outras pastas

| Quando a decisão impacta… | Atualizar também |
|---------------------------|------------------|
| Posicionamento, tom, missão | `00-identidade/` |
| Features, preços, oferta | `01-produto/`, `01-produto/precos/` |
| Páginas, funil | `02-site/` |
| Fluxos e automações | `03-n8n/` |
| Ambientes, custos, deploy | `04-infraestrutura/` |
| Canais, campanhas | `05-marketing/` |
| Personas, suporte | `06-clientes/` |
| KPIs, medição | `07-metricas/` |
| APIs, sistemas ligados | `08-integracoes/` |
| Processos internos | `09-operacional/` |
| Prioridades temporais | `10-roadmap/` |
| Prompts e modelos | `11-prompts/` |

## Inclusão no contexto LLM

O workflow [`.github/workflows/build-contexto.yml`](../.github/workflows/build-contexto.yml) acrescenta ao `99-contexto-llm/contexto-completo.md` as **últimas 5** decisões (exclui `_template.md`). Manter decisões autocontidas ajuda o modelo a responder sem ambiguidade.
