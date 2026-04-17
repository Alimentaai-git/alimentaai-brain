# Integrações — Mapa

## Diagrama do ecossistema

```
[SITE] ──webhook──► [N8N] ──api──► [LLM / IA]
  │                   │
  │                   ├──────────► [CRM / Email]
  │                   └──────────► [Notificações]
  │
  ├──────────────────────────────► [Analytics]
  └──────────────────────────────► [Pagamentos]

[BRAIN] ◄──── contexto para todos os sistemas via raw URL
```

## Mapa de integrações
| De | Para | O que passa | Como | Crítico? |
|---|---|---|---|---|
| Site | N8N | Lead capturado | Webhook | ✅ Sim |
| N8N | LLM | Prompt + contexto | API REST | ✅ Sim |
| | | | | |

## APIs externas
| API | Uso | Quem chama | Documentação |
|---|---|---|---|
| | | | |
