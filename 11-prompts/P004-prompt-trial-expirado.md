# P004 — Prompt Trial Expirado

**Modelo alvo**: OpenRouter `google/gemini-2.5-flash` (temp 0.3)  
**Usado em**: n8n → nó `prompt_trial_expired` → `agente_refeicao`  
**Quando dispara**: Switch → saída fallback (usuário cadastrado mas `current_period_end` < agora E fora do período de 7 dias de trial)  
**Status**: ✅ Ativo  
**Atualizado em**: 2025-04-17  

---

## Intenção

Prompt minimalista para usuários cujo **trial ou assinatura expirou**. Objetivo único: comunicar o fim do período e direcionar para o site para continuar. **Não analisa refeições, não calcula macros, não responde sobre dieta**.

---

## Comportamento

O agente **não tem liberdade de resposta** neste estado. A instrução é enviar uma mensagem fixa exatamente como especificado, sem editar, sem chamar tools, sem responder sobre nutrição.

### Mensagem fixa enviada

```
Oi {nome}! 😊

Seu período gratuito de 7 dias do AlimentaAI chegou ao fim.

Mas não se preocupe! Você pode continuar acompanhando sua alimentação, metas e análises automáticas clicando no link abaixo:

👉 [Continuar usando o AlimentaAI](https://alimend-assist.lovable.app/auth)

Não perca suas informações e o acompanhamento das suas refeições! 💪🍽️
```

`{nome}` vem de `$('getClient').item.json.nome` — fallback para emoji `👋` se nome for nulo.

---

## Restrições absolutas deste prompt

- ❌ Não responder sobre dieta ou nutrição
- ❌ Não calcular macros
- ❌ Não chamar nenhuma tool
- ❌ Não editar o texto da mensagem
- ✅ Enviar apenas e exatamente o texto acima

---

## Lógica de verificação de expiração (Switch no n8n)

O Switch que direciona para este prompt verifica na ordem:

1. **Não Cadastrado**: `$('getClient').item.json.id` não existe
2. **Active**: `new Date($('getSubscribe').item.json.current_period_end).getTime() > new Date().getTime()` → vai para P002
3. **Trial**: `new Date().getTime() < new Date($('getClient').item.json.data_criacao).getTime() + (7 * 24 * 60 * 60 * 1000)` → vai para P002
4. **Fallback (expirado)**: qualquer outro caso → vai para P004

---

## Notas e aprendizados

- URL de retorno hardcodada no prompt: `https://alimend-assist.lovable.app/auth` — atualizar aqui e no n8n quando o domínio de produção for fixado
- Usar `onError: "continueRegularOutput"` no agente garante que mensagem de expiração seja enviada mesmo se o LLM falhar
- Este é o prompt mais simples — qualquer complexidade adicionada aqui é um bug, não uma feature
