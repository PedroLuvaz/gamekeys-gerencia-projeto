# Sprint Goals

O Sprint Goal é uma frase que diz **o resultado esperado da sprint**, e não uma lista de tarefas. Ele
**não muda no meio da sprint**: se o time perceber que não entrega tudo, corta o item de menor prioridade
e registra o corte na Review.

Nesta etapa, só a **Sprint 1** tem proposta de goal e de itens, e só a Sprint 0 tem itens atribuídos no quadro.
O goal e os itens das demais sprints são definidos no Planning de cada uma, a partir do velocity medido.

---

## Sprint 0 — Release 1 · 06/10 a 15/10

> O time tem a infraestrutura de gestão pronta: repositório, quadro, backlog inicial priorizado, planos
> de qualidade e riscos, e pipeline de CI funcionando.

Itens: tarefas `[Sprint 0]` no quadro (#1 a #11).

## Sprint 1 — Release 1 · 20/10 a 29/10

> **Um visitante consegue navegar pelo catálogo de jogos e abrir o detalhe de um jogo, e um cliente
> consegue criar uma conta e entrar no sistema.**

| Issue | Item candidato | Pontos |
|---|---|---|
| #12 | Cadastro de cliente | 3 |
| #13 | Login com e-mail e senha | 5 |
| #14 | Listagem paginada de jogos | 5 |
| #15 | Detalhe do jogo | 2 |
| | **Total** | **15** |

No quadro, essas histórias ficam **sem Sprint** até o Planning de 20/10, quando o time confirma o que cabe.

**Como o goal será verificado na Review (29/10):** demonstração do roteiro abaixo, no ambiente local, com os
dados de demonstração.

1. Abrir a listagem sem login e navegar entre as páginas.
2. Abrir o detalhe de um jogo em estoque e de um jogo esgotado.
3. Cadastrar um cliente novo; tentar repetir o e-mail e ver a mensagem de erro.
4. Entrar com o cliente criado; tentar uma senha errada e ver a mensagem genérica.

**O que é cortado primeiro se a sprint estourar:** #15 (Detalhe do jogo), porque não bloqueia nenhuma
outra história da sprint.

## Sprints seguintes

Não há previsão de goal nem de itens por sprint. A cada Planning, o time toma do topo do
[backlog priorizado](priorizacao.md) o que cabe na capacidade, e o PO propõe o Sprint Goal. O roteiro abaixo é por **release**.

## Objetivo de cada release

| Release | Entrega de valor | Histórias previstas |
|---|---|---|
| **1** (Sprints 0 e 1) | Time organizado e produto com **catálogo navegável e conta de cliente** | #12 #13 #14 #15 |
| **2** (Sprints 2 e 3) | **Compra ponta a ponta**: do carrinho à chave entregue, com preço congelado e sem chave duplicada | #16 a #21 |
| **3** (Sprints 4 e 5) | **Loja operável**: biblioteca, cancelamento, busca e administração de jogos e chaves | #22 a #28 |
| **4** (Sprint 6) | **Produto completo**: painel, indicadores, avaliações e Demo Day | #29 a #33 |
