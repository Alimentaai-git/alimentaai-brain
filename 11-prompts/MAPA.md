# Prompts — Mapa

## Biblioteca de prompts

| ID | Nome | Usado em | Modelo | Quando dispara | Status | Atualizado |
|----|------|----------|--------|----------------|--------|------------|
| P001 | System Prompt Padrão (Brain) | N8N, integrações externas | claude-sonnet-4 | Injeção manual de contexto | ✅ Ativo | 2025-04-17 |
| P002 | Prompt Trial / Ativo | n8n → `agente_refeicao` | OpenRouter `google/gemini-2.5-flash` | Assinatura ativa ou em trial (7 dias) | ✅ Ativo | 2025-04-17 |
| P003 | Prompt TBF (Não Cadastrado) | n8n → `agente_refeicao` | OpenRouter `google/gemini-2.5-flash` | Telefone não existe em `usuarios` | ✅ Ativo | 2025-04-17 |
| P004 | Prompt Trial Expirado | n8n → `agente_refeicao` | OpenRouter `google/gemini-2.5-flash` | Trial e assinatura expirados | ✅ Ativo | 2025-04-17 |
| P005 | Gemini Vision — Análise de Imagem | n8n → `Analyze image1` | Google Gemini `models/gemini-2.5-flash` | Mensagem do tipo ImageMessage | ✅ Ativo | 2025-04-17 |

---

## Categorias

- **Sistema** — P001: system prompt para injeção do Brain em qualquer LLM
- **Cliente / conversacional** — P002, P003, P004: prompts que interagem diretamente com clientes no WhatsApp
- **Visão** — P005: análise multimodal de imagens de pratos

---

## Árvore de decisão dos prompts no n8n

```
Mensagem WhatsApp recebida
│
├── [ImageMessage] → P005 (Gemini Vision) → output <imagem> → Redis buffer
├── [AudioMessage] → Transcrição UAZAPI → Redis buffer  
└── [Conversation] → Redis buffer
         │
         └── Switch (verificação de acesso)
              │
              ├── Não Cadastrado → P003 (TBF)
              ├── Active (assinatura válida) → P002 (Trial/Ativo)
              ├── Trial (dentro de 7 dias) → P002 (Trial/Ativo)
              └── Fallback (expirado) → P004 (Trial Expirado)
```

---

## Relação entre prompts e ferramentas (tools)

| Tool Supabase | P002 ✅ | P003 ✅ | P004 ❌ |
|---------------|---------|---------|---------|
| `registrar_refeicao` | ✅ | ❌ | ❌ |
| `consultar_refeicao_diario` | ✅ | ❌ | ❌ |
| `consultar_metas_macros` | ✅ | ❌ | ❌ |
| `excluir_refeicao` | ✅ | ❌ | ❌ |
| `buscar_alimento_taco` | ✅ | ✅ | ❌ |
| `marcar_tbf_concluido` | ❌ | ✅ | ❌ |
