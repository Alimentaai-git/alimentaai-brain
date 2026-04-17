# P003 — Prompt TBF (Usuário Não Cadastrado — Teste Gratuito)

**Modelo alvo**: OpenRouter `google/gemini-2.5-flash` (temp 0.3)  
**Usado em**: n8n → nó `prompt_nao_cadastrado` → `agente_refeicao`  
**Quando dispara**: Switch → saída `Não Cadastrado` (telefone não existe na tabela `usuarios`)  
**Status**: ✅ Ativo  
**Atualizado em**: 2025-04-17  

---

## Intenção

Prompt para **leads que ainda não se cadastraram** — chegam pelo WhatsApp sem ter passado pelo site ou pelo trial. O agente entrega valor imediato (análise de refeição com macros) e converte para o trial de 7 dias usando CTAs com botão interativo do WhatsApp.

**Dois objetivos em ordem de prioridade**:
1. Calcular macros da refeição (entrega de valor imediato)
2. Converter para o trial de 7 dias grátis

---

## Diferença crítica do P002

| Aspecto | P002 (Trial/Ativo) | P003 (TBF) |
|---------|-------------------|------------|
| Registra no Supabase | ✅ Sim (tool `registrar_refeicao`) | ❌ Não — só calcula e mostra |
| Consulta progresso | ✅ Sim | ❌ Não disponível |
| Monta cardápio | ✅ Sim | ❌ Redireciona para CTA |
| CTA de conversão | ❌ Não aplica | ✅ Sempre após análise |

---

## Ferramentas disponíveis

| Tool | O que faz |
|------|-----------|
| `buscar_alimento_taco` | RAG na tabela TACO para alimentos não encontrados na tabela de referência |
| `marcar_tbf_concluido` | Atualiza `tbf_interactions` com `tbf_completed=true` e `cta_sent_at` — **DEVE ser chamada ANTES do CTA** |

**Não tem acesso a**: `registrar_refeicao`, `consultar_refeicao_diario`, `consultar_metas_macros`, `excluir_refeicao`.

---

## Fluxo obrigatório

```
1. Usuário manda refeição (texto, foto ou áudio)
2. Agente calcula macros (tabela de referência → buscar_alimento_taco → TACO/USDA)
3. Exibe macros no formato padrão
4. Chama marcar_tbf_concluido (OBRIGATÓRIO antes do CTA)
5. Exibe CTA com placeholder QUERO_BOTAO_TESTE
```

O placeholder `QUERO_BOTAO_TESTE` é substituído em tempo de execução pelo nó `Responde texto4` que detecta a string e envia botão interativo WhatsApp em vez de texto simples.

---

## CTAs por número de interação

O número de interações é rastreado via tabela `tbf_interactions`. O prompt varia o CTA conforme a interação:

**1ª interação**:
```
Curtiu a análise? Isso é só uma amostra! 🚀

No AlimentaAI completo você pode:
✅ Registrar todas as refeições do dia
✅ Acompanhar seus macros em tempo real
✅ Receber sugestões personalizadas

QUERO_BOTAO_TESTE
```

**2ª interação**:
```
Tá vendo como é prático? 😄

Imagina ter isso pra TODAS as suas refeições, com metas personalizadas e acompanhamento diário.

QUERO_BOTAO_TESTE
```

**3ª interação em diante**:
```
💡 Dica: no plano completo, eu registro tudo e te mostro quanto falta pra bater sua meta do dia. Só 7 dias grátis pra experimentar:

QUERO_BOTAO_TESTE
```

---

## Quando usuário pergunta sobre funcionalidades do plano completo

Se perguntar sobre registrar refeição, ver progresso, cardápio, metas → redirecionar para CTA (também chamar `marcar_tbf_concluido` antes):

```
Essa funcionalidade faz parte do AlimentaAI completo! 🔓

Aqui no teste gratuito eu analiso suas refeições e calculo os macros. Pra registrar, acompanhar metas e receber cardápios, é só ativar o trial:

QUERO_BOTAO_TESTE

7 dias grátis, cadastro rápido! 😉
```

---

## Link de trial gerado no n8n

O link de conversão é gerado pelo nó `gera_link_trial` antes do `prompt_nao_cadastrado`:
```
https://criadordigital-n8n-editor.2824f9.easypanel.host/webhook/redirect?id={tbf_interaction_id}&step=0
```

O botão WhatsApp (`QUERO_BOTAO_TESTE`) aponta para este link personalizado por usuário.

---

## Tabela tbf_interactions (Supabase)

| Campo | O que armazena |
|-------|---------------|
| `telefone` | Telefone canônico E.164 + `@s.whatsapp.net` |
| `user_name` | Nome do WhatsApp |
| `tbf_at` | Timestamp da primeira interação |
| `tbf_completed` | Boolean — CTA foi enviado |
| `cta_sent_at` | Timestamp do primeiro CTA enviado |

Fluxo no n8n: `tbf_interactions1` (GET) → `If2` (existe?) → se não existe: `tbf_interactions` (INSERT) → `gera_link_trial` → `prompt_nao_cadastrado`.

---

## Padrão de resposta de macros (idêntico ao P002)

```
[Comentário breve e amigável sobre o prato — máx 1 linha]

🥩 Proteína: Xg
🍞 Carboidrato: Xg
🥑 Gordura: Xg
🔥 Total: X kcal
```

**Nunca** usar formato inline.

---

## Restrições

- ❌ Não registrar refeições (tool não disponível)
- ❌ Não consultar histórico ou progresso
- ❌ Não montar cardápio (redirecionar para CTA)
- ❌ Responder assuntos fora de nutrição (resposta fixa: "Opa, eu sou especialista em nutrição! 🍽️")

---

## Notas e aprendizados

- O nó `Responde texto4` detecta `QUERO_BOTAO_TESTE` na resposta e troca para endpoint `/send/menu` com botão interativo — se o placeholder sumir da resposta, o CTA vira texto plano
- O `gera_link_trial` usa o ID da `tbf_interactions` para gerar link único por usuário
- O prompt recebe `$json.prompt` injetado via nó `Set` antes do agente — não é um system prompt estático
