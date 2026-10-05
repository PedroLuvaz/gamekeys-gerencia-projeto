# Priorização do Product Backlog

Responsável: **Product Owner**. Esta página justifica a **ordem de execução** do backlog. Os critérios
de aceite de cada história estão na própria issue, e prioridade, pontos, sprint e release estão nos campos
do [quadro](https://github.com/users/PedroLuvaz/projects/2).

**Estado:** backlog inicial, criado na Sprint 0 (05/10/2026). **Os Story Points são estimativas iniciais do PO** e
serão revistos pelo time em Planning Poker no Planning de cada sprint. A previsão de sprint só vira
compromisso no Planning.

---

## 1. Como priorizamos

| Critério | Pergunta |
|---|---|
| **Valor no fluxo principal** | O item é necessário para o cliente ir da busca até a chave na biblioteca? |
| **Risco** | O item tem incerteza técnica alta? Se sim, vem cedo, para sobrar tempo de reagir |
| **Dependência** | Outros itens dependem dele? Se sim, ele vem antes |
| **Esforço** | Para valor igual, o menor esforço vem primeiro |

A escala da coluna **Prioridade** segue MoSCoW:

| Prioridade | MoSCoW | Significa |
|---|---|---|
| **Alta** | Must have | Sem isso não há produto demonstrável |
| **Média** | Should have | Esperado pelo usuário; sai da sprint se ela estourar |
| **Baixa** | Could have | Melhora a experiência; fora das sprints planejadas |

**Regra de corte:** quando a sprint estoura, o time corta o item de prioridade Média mais abaixo no backlog
e **registra o corte na Review**. Cortar com registro é gestão de escopo; esconder o corte, não.

## 2. Backlog em ordem de execução

| Ordem | Issue | História | Épico | Prior. | Pts | Sprint | Rel. | Justificativa |
|---|---|---|---|---|---|---|---|---|
| 1 | #12 | Cadastro de cliente | Conta | Alta | 3 | 1 | 1 | Porta de entrada de todo cliente: sem conta não há compra. Concentra RN-01 e RN-10. |
| 2 | #13 | Login com e-mail e senha | Conta | Alta | 5 | 1 | 1 | Habilita carrinho e área do cliente. Depende do cadastro, por isso vem logo depois. |
| 3 | #14 | Listagem paginada de jogos | Catálogo | Alta | 5 | 1 | 1 | Primeira tela do produto. Inclui o modelo de dados (jogo, gênero, chave) e o seed que sustentam todas as histórias seguintes. |
| 4 | #15 | Detalhe do jogo | Catálogo | Alta | 2 | 1 | 1 | Completa a navegação do visitante e é o ponto de partida da compra. Menor item da sprint: primeiro a ser cortado. |
| 5 | #16 | Adicionar jogo ao carrinho | Carrinho | Alta | 5 | 2 | 2 | Início do fluxo de compra e onde moram as regras RN-04, RN-05 e RN-09. |
| 6 | #17 | Ajustar quantidade e remover itens do carrinho | Carrinho | Alta | 3 | 2 | 2 | Completa o carrinho; esforço baixo e sem o qual o cliente não corrige um erro. |
| 7 | #18 | Controlar as transições de status do pedido | Pedido | Alta | 5 | 2 | 2 | Habilita checkout, pagamento, cancelamento e auditoria. Antecipada para a Sprint 2 para destravar a Sprint 3. |
| 8 | #19 | Finalizar compra com preço congelado | Pedido | Alta | 5 | 3 | 2 | Núcleo do negócio. RN-03 protege o valor dos pedidos e o faturamento. |
| 9 | #20 | Reservar chaves sem risco de venda duplicada | Pedido | Alta | 5 | 3 | 2 | Maior risco técnico (RSK-01). Entra na Sprint 3, com folga antes do fim da Release 2 para corrigir se travar. |
| 10 | #21 | Pagamento simulado e entrega da chave | Pedido | Alta | 3 | 3 | 2 | Fecha o fluxo de compra: o cliente recebe a chave. É o valor central da Release 2. |
| 11 | #22 | Biblioteca de chaves do cliente | Pedido | Alta | 3 | 4 | 3 | Completa a jornada do cliente: onde ele consulta o que comprou. |
| 12 | #23 | Cancelar pedido não pago | Pedido | Alta | 3 | 4 | 3 | Fecha o ciclo do pedido e exercita a devolução de chaves ao estoque (RN-08). |
| 13 | #24 | Controle de acesso por papel | Conta | Alta | 3 | 4 | 3 | Pré-requisito de toda a administração e requisito de segurança do sistema multiusuário. |
| 14 | #25 | Busca, filtros e ordenação do catálogo | Catálogo | Média | 5 | 4 | 3 | Melhora a descoberta, mas o produto é demonstrável sem ela: Média e primeiro item cortável da Sprint 4. |
| 15 | #26 | Gerenciar jogos do catálogo | Administração | Alta | 5 | 5 (curta) | 3 | Sem ela o catálogo depende do seed. Libera o administrador a manter a loja. |
| 16 | #27 | Cadastrar chaves de ativação em lote | Administração | Alta | 3 | 5 (curta) | 3 | Sem reposição, o estoque acaba e a loja para de vender. |
| 17 | #28 | Histórico e detalhe dos meus pedidos | Pedido | Média | 2 | 5 (curta) | 3 | Acompanhamento do cliente; valioso, mas não bloqueia a compra: Média. |
| 18 | #29 | Painel de pedidos | Administração | Média | 3 | 6 | 4 | Visão operacional das vendas. Média: o PO aceita demonstrar a loja sem ela se necessário. |
| 19 | #30 | Trilha de auditoria do pedido | Administração | Média | 2 | 6 | 4 | Rastreabilidade; os eventos já são gravados desde a Sprint 2, falta a tela. Média. |
| 20 | #31 | Indicadores de venda | Administração | Média | 5 | 6 | 4 | Valor gerencial, mas é o item de maior esforço entre os Média. Candidato a corte. |
| 21 | #32 | Avaliar um jogo comprado | Avaliações | Média | 3 | 6 | 4 | Completa o ciclo pós-compra. Média: não afeta o fluxo de compra. |
| 22 | #33 | Ler avaliações no detalhe do jogo | Avaliações | Média | 2 | 6 | 4 | Consome as avaliações registradas; menor valor sem a história anterior. |
| 23 | #34 | Perfil do usuário | Conta | Baixa | 2 | — | — | Conveniência. Fora das sprints planejadas. |
| 24 | #35 | Gerenciar gêneros | Administração | Baixa | 2 | — | — | O seed já traz os gêneros iniciais. Fora das sprints planejadas. |
| 25 | #36 | Reembolsar pedido entregue | Administração | Baixa | 2 | — | — | A transição existe no ciclo do pedido; o estorno financeiro está fora do escopo. |
| 26 | #37 | Nota média na listagem do catálogo | Avaliações | Baixa | 2 | — | — | Depende das avaliações e piora o custo da listagem. Fora das sprints planejadas. |

Os itens de encerramento da Release 4 (roteiro de demonstração, lições aprendidas, release notes finais,
deploy) serão criados no refinamento de janeiro, porque dependem do que a Release 3 entregar.

## 3. Capacidade e carga por sprint

**Premissas da estimativa inicial (a validar no Planning Poker e recalibrar com o velocity real):**

- 3 integrantes dedicando cerca de **10 horas por semana** cada ao projeto, incluindo as aulas de desenvolvimento
- **1 ponto ≈ 3 horas** de trabalho de uma pessoa
- Isso dá **2 pontos por dia útil** da equipe (3 pessoas × 2 h por dia útil ÷ 3 h por ponto)
- Feriados descontados: 20/11 (Consciência Negra) e Carnaval em 08 e 09/02/2027

| Sprint | Dias úteis | Capacidade (pts) | Carga planejada (pts) | Folga (pts) | Observação |
|---|---|---|---|---|---|
| 1 | 8 | 16 | 15 | 1 | Primeira sprint do time, sem velocity de referência: folga pequena, por isso #15 é o primeiro corte |
| 2 | 8 | 16 | 13 | 3 |  |
| 3 | 7 | 14 | 13 | 1 | Feriado em 20/11. Contém a história de maior risco (#20); se travar, #21 é o primeiro a ir para a Sprint 4 |
| 4 | 8 | 16 | 14 | 2 | Primeiro item cortável: #25 |
| 5 | 6 | 12 | 10 | 2 | Sprint curta (8 dias corridos) |
| 6 | 11 | 22 | 15 | 7 | Carnaval em 08 e 09/02. Folga reservada ao Demo Day e aos itens de encerramento |

- **Total planejado nas Sprints 1 a 6:** 80 pontos
- **Prioridade Baixa, sem sprint:** 8 pontos (#34 #35 #36 #37)
- **Backlog total de histórias:** 88 pontos
- **Tarefas da Sprint 0:** 24 pontos, em issues próprias com labels `documentação` e `tech-debt`

A carga fica de propósito **abaixo da capacidade** em todas as sprints, para absorver bugs, revisão e
imprevistos de uma equipe que ainda não tem histórico. A folga das Sprints 1 e 3 é pequena e, por isso, ambas têm
um item definido como primeiro corte.

## 4. Histórico de repriorização

Toda mudança de ordem, escopo ou estimativa depois do backlog inicial é registrada aqui, com a
justificativa (métrica ou feedback da Review).

| Data | Mudança | Justificativa | Decidido por |
|---|---|---|---|
| 05/10/2026 | Criação do backlog inicial: 26 histórias, Sprints 1 a 6 | Proposta do PO a partir do escopo aprovado | PO |
