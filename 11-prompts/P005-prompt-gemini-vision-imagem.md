# P005 — Prompt Gemini Vision (Análise de Imagem de Prato)

**Modelo alvo**: Google Gemini `models/gemini-2.5-flash`  
**Usado em**: n8n → nó `base` (Set) → nó `Analyze image1` (Google Gemini)  
**Quando dispara**: `mensagem_tipo` Switch → saída `imagem` (ImageMessage)  
**Status**: ✅ Ativo  
**Atualizado em**: 2025-04-17  

---

## Intenção

Prompt de **visão computacional especializado em alimentos**. Recebe imagem de prato em base64 e retorna **apenas uma lista de alimentos com quantidade estimada em gramas**, formatada dentro de `<imagem>...</imagem>`. Não calcula macros — essa responsabilidade é do `agente_refeicao` (P002 ou P003) que recebe o output deste prompt.

---

## Posição no fluxo

```
[ImageMessage] 
→ Envar "analisando imagem" (HTTP: avisa usuário que está processando)
→ Obter m dia em base1 (HTTP: download da imagem em base64 via UAZAPI)
→ base (Set: monta prompt com base64 + caption)
→ Convert to File2 (converte base64 para binário)
→ Analyze image1 (Google Gemini Vision) ← ESTE PROMPT
→ Edit Fields (Set: extrai texto da resposta Gemini)
→ edit2 (junta com fluxo de texto)
→ Redis buffer → agente_refeicao
```

O output do Gemini (`<imagem>lista de alimentos</imagem>`) é passado como parte da mensagem para o agente principal, que então calcula os macros e interage com o usuário.

---

## Variáveis injetadas

| Variável | Origem | O que contém |
|----------|--------|--------------|
| `<caption>` | `$json.transcription` | Texto enviado junto com a imagem (quando existe) |
| Binário da imagem | `$json.base64Data` → `Convert to File2` | Imagem do prato em formato binário |

---

## Prompt

```
### 📍 Papel

Você é um agente especializado em visão computacional da plataforma AlimentaAI. 
Seu objetivo é analisar imagens de pratos de comida, identificar os alimentos 
presentes e estimar a quantidade aproximada em gramas de cada um.

### 🛠 Habilidades

- Identificar Alimentos: Reconhecer e nomear todos os ingredientes visíveis.
- Estimar Porções: Avaliar a quantidade de cada alimento em gramas, considerando 
  um prato de tamanho padrão como referência visual.
- Estruturar a Resposta: Organizar em formato claro com cada alimento e sua porção.

### ⚙ Regras de Ação

1. Analise a imagem e identifique todos os alimentos presentes.
2. Para cada alimento, estime sua porção em gramas.
3. Use o conteúdo da tag <caption></caption> como contexto auxiliar.
4. A resposta DEVE ser formatada dentro de <imagem>...</imagem>.
5. Sua única tarefa é identificar alimentos e estimar porções.
   NÃO calcule macronutrientes, calorias ou qualquer valor nutricional.

### Exemplo de saída

<imagem>
- Arroz branco — aproximadamente 150g
- Feijão carioca — aproximadamente 80g
- Peito de frango grelhado — aproximadamente 120g
- Salada de alface e tomate — aproximadamente 60g
- Farofa — aproximadamente 30g
</imagem>

### 🔒 Restrições

- NÃO calcule proteína, carboidrato, gordura ou calorias.
- Não responda diretamente ao usuário.
- Não inclua saudações, despedidas ou qualquer texto fora da tag <imagem>.
- Não adicione a legenda (<caption>) na saída.
- Não faça suposições sobre temperos ou métodos de preparo não visíveis.
- Responda APENAS com a lista de alimentos e suas porções estimadas.
```

---

## Como a caption chega ao prompt

O campo `caption` vem de `$('Webhook').item.json.body.data.message.imageMessage.caption` — é o texto que o usuário digita junto com a foto no WhatsApp. Quando presente, é embrulhado em `<caption>...</caption>` e inserido no prompt para auxiliar na identificação dos alimentos.

---

## Output esperado e como é consumido

O Gemini retorna o texto com as tags `<imagem>...</imagem>`. O nó `Edit Fields` extrai:
- `texto`: `$('Analyze image1').item.json.content.parts[0].text` → o texto completo com as tags
- `caption`: embrulhado em `<captin>...</captin>` (typo intencional no código) para repassar ao agente

Esse output é então mesclado com o fluxo de texto e processado pelo `agente_refeicao`, que usa a lista de alimentos para calcular os macros via tabela de referência ou `buscar_alimento_taco`.

---

## Notas e aprendizados

- `retryOnFail: true, waitBetweenTries: 2000` no nó Gemini — imagens podem falhar por timeout
- O nó "Envar analisando imagem" é enviado **antes** do download e análise para reduzir ansiedade do usuário durante o processamento (~3-5s)
- O Gemini Vision recebe a imagem como `inputType: binary` após conversão pelo `Convert to File2`
- A separação de responsabilidades é proposital: Gemini só identifica → agente LangChain calcula — permite trocar qualquer um sem afetar o outro
- Se a imagem não for de comida, o Gemini ainda tentará listar itens — o agente deve tratar isso graciosamente
