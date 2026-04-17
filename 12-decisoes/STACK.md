# Decisões — Stack

## Ferramentas

| Ferramenta | Uso |
|------------|-----|
| **Git** | Versionamento dos ficheiros `.md` |
| **GitHub** | Remoto, histórico, (opcional) revisão em pull request |
| **Markdown** | Formato único dos registos |

## Automação

| Componente | Função |
|------------|--------|
| [`.github/workflows/build-contexto.yml`](../.github/workflows/build-contexto.yml) | Em cada push à `main`, concatena excertos do Brain e inclui as **5 decisões mais recentes** em `99-contexto-llm/contexto-completo.md` |
| `GITHUB_TOKEN` | Permite checkout e push do commit gerado pela Action |

## Boas práticas

- Um ficheiro por decisão (facilita diff, blame e inclusão ordenada no contexto LLM).
- Não renomear decisões antigas só para “organizar”; o histórico perde-se no Git de forma confusa.
- Manter `_template.md` estável; mudanças ao template podem ser uma decisão documentada.
