# Decisões — Contexto

## Por que decisões vivem no Git

- **Histórico auditável** — data, autor e evolução ficam explícitos.
- **Mesma fonte que o código e o Brain** — um único fluxo de revisão e branches.
- **Injeção em LLMs** — trechos recentes entram no `contexto-completo.md` gerado pela Action.

## O que entra aqui

- Escolhas com **efeito duradouro** (stack, fornecedor, preço, posicionamento, processo crítico).
- Decisões com **trade-offs** que vale a pena documentar para o futuro.
- **Substituições** de decisões antigas (marcar a anterior como `Substituída` e referenciar a nova).

## O que não entra

- Notas de reunião sem conclusão (use rascunho local ou PR até fechar).
- Detalhe operacional do dia a dia que já cabe em `09-operacional/CONTEXTO.md`.
- Dados pessoais de clientes ou credenciais.

## Estados

Usar o campo **Status** do template: `Proposta`, `Aceita`, `Descartada`, `Substituída`.

- `Proposta` — ainda em discussão; pode coexistir com outras propostas sobre o mesmo tema.
- `Aceita` — passa a ser referência; outras áreas do Brain devem refletir a mudança quando aplicável.

## Revisão periódica

De tempos em tempos, rever decisões `Aceitas` que deixaram de refletir a realidade: criar uma nova decisão que **substitui** a anterior em vez de apagar o ficheiro antigo.
