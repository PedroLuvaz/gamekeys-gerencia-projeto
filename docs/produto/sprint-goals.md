# Sprint Goals

O Sprint Goal é uma frase que diz **o resultado esperado da sprint**, e não uma lista de tarefas. Ele
**não muda no meio da sprint**: se o time perceber que não entrega tudo, corta o item de menor prioridade
e registra o corte na Review.

Só o goal da Sprint 1 é compromisso do PO nesta etapa. Os demais são **previsões** e serão confirmados
no Planning de cada sprint, a partir do velocity medido.

---

## Sprint 0 — Release 1 · 06/10 a 15/10

> O time tem a infraestrutura de gestão pronta: repositório, quadro, backlog inicial priorizado, planos
> de qualidade e riscos, e pipeline de CI funcionando.

Itens: tarefas `[Sprint 0]` no quadro (#1 a #11).

## Sprint 1 — Release 1 · 20/10 a 29/10

> **Um visitante consegue navegar pelo catálogo de jogos e abrir o detalhe de um jogo, e um cliente
> consegue criar uma conta e entrar no sistema.**

| Issue | Item | Pontos |
|---|---|---|
| #12 | Cadastro de cliente | 3 |
| #13 | Login com e-mail e senha | 5 |
| #14 | Listagem paginada de jogos | 5 |
| #15 | Detalhe do jogo | 2 |
| | **Total** | **15** |

**Como o goal será verificado na Review (29/10):** demonstração do roteiro abaixo, no ambiente local, com os
dados de demonstração.

1. Abrir a listagem sem login e navegar entre as páginas.
2. Abrir o detalhe de um jogo em estoque e de um jogo esgotado.
3. Cadastrar um cliente novo; tentar repetir o e-mail e ver a mensagem de erro.
4. Entrar com o cliente criado; tentar uma senha errada e ver a mensagem genérica.

**O que é cortado primeiro se a sprint estourar:** #15 (Detalhe do jogo), porque não bloqueia nenhuma
outra história da sprint.

## Previsão das sprints seguintes

| Sprint | Release | Goal previsto | Itens | Pontos |
|---|---|---|---|---|
| **2** | 2 | Um cliente autenticado monta e ajusta o carrinho, e o sistema controla o ciclo de vida do pedido com transições validadas | #16 #17 #18 | 13 |
| **3** | 2 | Um cliente finaliza a compra e recebe a chave, sem que ela possa ser vendida duas vezes | #19 #20 #21 | 13 |
| **4** | 3 | O cliente acessa sua biblioteca e cancela pedidos, as áreas administrativas ficam protegidas e o catálogo é pesquisável | #22 #23 #24 #25 | 14 |
| **5 (curta)** | 3 | O administrador mantém o catálogo e o estoque de chaves, e o cliente consulta seu histórico de pedidos | #26 #27 #28 | 10 |
| **6** | 4 | A loja é operável pelo administrador e avaliada pelos clientes, pronta para o Demo Day | #29 #30 #31 #32 #33 + encerramento | 15 + encerramento |

## Objetivo de cada release

| Release | Entrega de valor |
|---|---|
| **1** (Sprints 0 e 1) | Time organizado e produto com **catálogo navegável e conta de cliente** |
| **2** (Sprints 2 e 3) | **Compra ponta a ponta**: do carrinho à chave entregue, com preço congelado e sem chave duplicada |
| **3** (Sprints 4 e 5) | **Loja operável**: biblioteca, cancelamento, busca e administração de jogos e chaves |
| **4** (Sprint 6) | **Produto completo**: painel, indicadores, avaliações e Demo Day |
