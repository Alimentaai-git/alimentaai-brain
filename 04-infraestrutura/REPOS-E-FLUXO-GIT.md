# Repositórios, branches e commits (AlimentaAI)

Guia operacional para a organização **Alimentaai-git** no GitHub. Passos marcados como **(GitHub UI)** devem ser feitos no browser; não há `gh` CLI neste ambiente.

## Repositórios na organização

| Repositório | Função | Branch(es) |
|-------------|--------|------------|
| `alimentaai-brain` | Fonte da verdade (Markdown) | `main` apenas — commit direto |
| `site-alimentaai` | SPA React (Vite) | `main` (produção), `dev` (integração), `feat/*`, `fix/*` |
| `alimentaai-n8n` | Export sanitizado do workflow | `main` apenas |
| `alimentaai-marketing` | Assets e estratégia (fora do Brain quando fizer sentido) | `main` (ajustar conforme necessidade) |

Criar na org (se ainda não existirem): **New repository** → nome exato → visibilidade à escolha → sem README se já tens clone local (ou com README e depois `git pull --rebase` antes do primeiro push).

## 1. Proteger a `main` do site **(GitHub UI)**

Repositório: `Alimentaai-git/site-alimentaai` → **Settings** → **Branches** → **Add branch protection rule** → Branch name pattern: `main`.

Ativar:

- **Require a pull request before merging**
- **Require approvals**: 1
- **Dismiss stale pull request approvals when new commits are pushed**
- **Do not allow bypassing the above settings** (inclui administradores, se quiseres disciplina total)

Guardar a regra. O Brain e o n8n **não** precisam de proteção de branch (velocidade em `main`).

## 2. Branch `dev` do site (local)

Já criada e enviada a partir de `main`:

```powershell
cd C:\Users\Dariva\Documents\ALIMENTAAI_SITE\alimend-assist
git fetch origin
git checkout dev
git pull origin dev
```

Fluxo: `feat/...` ou `fix/...` → PR para `dev` → testar → PR `dev` → `main` (deploy). **Não** commits diretos em `main` depois das proteções ativas.

## 3. Primeiro push: `alimentaai-n8n` e `alimentaai-marketing`

Depois de criar o repositório vazio na org:

```powershell
cd C:\Users\Dariva\Documents\ALIMENTAAI_SITE\alimentaai-n8n
git remote -v
git push -u origin main
```

```powershell
cd C:\Users\Dariva\Documents\ALIMENTAAI_SITE\alimentaai-marketing
git push -u origin main
```

Se o GitHub tiver criado um commit inicial (README), usar:

```powershell
git pull origin main --allow-unrelated-histories
# resolver conflito se houver, depois:
git push -u origin main
```

## 4. Export n8n (`workflow-export.json`)

1. Exportar o workflow no n8n **sem** `pinData` e **sem** credenciais em texto claro.
2. Substituir `workflow-export.json` na raiz do repo `alimentaai-n8n`.
3. Antes de commitar (PowerShell):

```powershell
Select-String -Path workflow-export.json -Pattern 'sk-|api_key|token' -CaseSensitive:$false
```

Se aparecer correspondência suspeita, rever o ficheiro antes do commit.

4. Commit sugerido: `feat(workflow): descrição curta no imperativo`

5. No Brain, atualizar `03-n8n/MAPA.md` / `CONTEXTO.md` quando o fluxo mudar (`docs(n8n): ...`).

## 5. Brain — contextos gerados (`99-contexto-llm`)

**Não** colocar `99-contexto-llm/contexto-*.md` no `.gitignore`: a Action precisa de commitar esses ficheiros. O workflow já usa `[skip ci]` no commit automático para evitar loop.

## 6. Convenção de commits (resumo)

Formato: `tipo(área): descrição no imperativo` (+ corpo opcional + `refs:`).

**Brain (documentação):** `docs`, `decision`, `feat`, `prompt`, `metrics`, `fix`, `refactor` com áreas como `identidade`, `tecnico`, `produto`, `n8n`, `site`, `integracoes`.

**Site (código):** `feat`, `fix`, `style`, `refactor`, `perf`, `chore` com áreas como `checkout`, `auth`, `landing`, `deps`.

**n8n:** `feat(workflow)`, `fix(workflow)`, `prompt(agente)`, `chore(workflow)`, etc.

## 7. Cenários do dia a dia

- **Só código no site:** branch a partir de `dev` → PR para `dev` → PR `dev` → `main` → no Brain, `docs(site): ...` em `02-site/`.
- **Decisão importante:** novo ficheiro em `12-decisoes/` (a partir de `_template.md`) + STACKs afetados → `decision(tecnico): ...` (ou equivalente).
- **Workflow n8n:** export sanitizado → commit em `alimentaai-n8n` → `docs(n8n): ...` no Brain.
- **Prompt:** editar `11-prompts/P00X.md` no Brain → copiar texto atualizado para o nó no n8n.

Princípio: **código no repo de código; conhecimento no Brain** — manter os dois alinhados.
