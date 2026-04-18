# N8N — Contexto

## Por que n8n

Orquestração visual de **WhatsApp (Evolution / UAZAPI)** com **Redis** (debounce / fila curta), **Supabase** (dados e vector store), **vários LLMs** (Gemini para imagem, OpenRouter para chat do agente, OpenAI para embeddings no RAG) e **Postgres** (memória LangChain + **remarketing** com nós `postgres` nativos). Hoje há **vários workflows** na mesma instância: atendimento (**ALIMENTAAI - NOVO**) e remarketing (**REMARKETING - POS CTA**, **REMARKETING - TBF**) — ver `MAPA.md`.

## Fluxos mais críticos

- **Webhook principal de mensagens** (workflow **ALIMENTAAI - NOVO**): se falhar, o cliente não recebe resposta automática.
- **Webhook `recebe_do_site`** (no mesmo workflow): ligação site ↔ automação; falhas aqui quebram fluxos pós-site (ex.: trial / onboarding conforme implementado nos nós).
- **Agente `agente_refeicao` + ferramentas Supabase** (ex.: persistência em `refeicoes`): núcleo do produto “macros por refeição”.
- **Redis** na agregação de mensagens: se Redis estiver indisponível ou com TTL errado, mensagens podem fragmentar-se ou atrasar-se.
- **Remarketing (Cron + Postgres + HTTP)**: envio em massa ou sequenciado — risco de **spam**, custo de API e **inconsistência de estado** se updates Postgres falharem a meio do loop; validar janelas e limites no editor n8n.

## Pontos de atenção

- **Credenciais**: nunca embutir `sk-` ou tokens de instância no JSON exportado — usar **Credentials** do n8n e reexportar sem segredos (como em `workflow-export.json`).
- **Custos**: cada mensagem pode acionar Gemini, OpenRouter e embeddings; monitorizar quotas.
- **Dependências externas**: Supabase, Redis, host UAZAPI (`BaseUrl` típico `https://alimentaai.uazapi.com` no payload), e instância Evolution devem estar saudáveis em cadeia.
- **Manutenção**: nós placeholder (`Replace Me`, `No Operation`) devem ser tratados ou removidos no editor.
- **Exports no GitHub**: os JSON em `alimentaai-n8n` podem vir com `parameters: {}` vazios conforme a ferramenta de export/redação; horários de **Cron**, URLs completas de webhook e SQL não ficam fiáveis só pelo ficheiro — confirmar sempre no **editor n8n** em produção.

## Como buscar contexto do Brain no n8n

```
Nó: HTTP Request
Método: GET  
URL: https://raw.githubusercontent.com/Alimentaai-git/alimentaai-brain/main/99-contexto-llm/contexto-completo.md
```

Injete o resultado como system prompt em qualquer nó LLM do fluxo.

## Segurança (lembrete)

Se um export antigo continha **chaves ou PII**, rodar as chaves no fornecedor e **não** voltar a commitar `pinData` nem API keys em nós `Set`.
