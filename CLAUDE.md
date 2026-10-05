# Instruções para agentes de código — GameKeys

Lido automaticamente pelo Claude Code. Em conflito entre este arquivo e o hábito do agente, **este
arquivo vence**.

## Contexto

Projeto da disciplina de Gerência de Projeto (equipe de 3, Scrum, 4 releases). **O que vale nota é a
evidência de gestão, não a sofisticação do código.** Prefira sempre a solução mais simples que atenda
ao critério de aceite da história. Não antecipe requisito nem crie abstração para um único caso.

Leia antes de implementar: [`README.md`](README.md), [`CONTRIBUTING.md`](CONTRIBUTING.md),
[`docs/produto/regras-de-negocio.md`](docs/produto/regras-de-negocio.md),
[`docs/produto/definition-of-done.md`](docs/produto/definition-of-done.md) e a **issue** da história
(os critérios de aceite vivem nela, não em arquivo).

## Stack

Python 3.12 · FastAPI · PostgreSQL 16 · React + TypeScript · pytest + httpx · ruff · GitHub Actions ·
Docker. **Dependência nova exige perguntar à equipe antes e registrar a decisão.**

Fora de escopo, não implemente: gateway de pagamento real (pagamento é simulado), upload de imagem
(capa é URL externa), app móvel, qualquer recurso de IA, microsserviços, filas, cache externo.

## Convenções

- Domínio em **português**: tabelas, colunas, classes, rotas, mensagens de erro. Palavras-chave da
  linguagem e nomes de biblioteca ficam em inglês.
- Estoque de um jogo é a **contagem** de chaves disponíveis. Não existe coluna de quantidade.
- Regra de negócio só no back-end. O front pergunta à API e não decide.
- Mudança de status do pedido passa por uma função única de transição, nunca por atribuição direta.
- Sem `except Exception: pass`. Sem mock de banco nos testes de comportamento.

## Fluxo

1. Identifique a issue (`#n`) e cite o número na resposta.
2. Liste os critérios de aceite que a mudança precisa satisfazer.
3. Branch `<tipo>/<n>-<descricao>` a partir da `main`. **Nunca commit direto na `main`.**
4. Commit: `<tipo>(<escopo>): <descrição no imperativo> (#n)`. **Nunca** adicione `Co-Authored-By`
   nem qualquer atribuição a agente de IA (Claude, Codex, Gemini etc.) em commit, PR ou issue.
   `Co-authored-by` só é usado para colegas humanos que programaram juntos.
5. Rode `ruff check .`, `ruff format --check .` e `pytest` em `backend/` antes de concluir.
6. Abra o PR com `Closes #n` e o checklist da Definition of Done preenchido.
7. Reporte quais critérios de aceite ficaram atendidos e quais não.

Se a tarefa exigir uma decisão técnica ou de escopo que não está documentada, **pare e pergunte**.
Decisão tomada em silêncio é decisão que ninguém da equipe consegue defender na apresentação.
