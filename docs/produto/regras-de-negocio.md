# Regras de negócio

Cada regra tem um identificador estável. Os **critérios de aceite das issues referenciam o identificador**
em vez de repetir o comportamento, para que a especificação viva em um só lugar. Este documento é
instrumento de trabalho do **QA**: cada regra deve ter um teste que a prove.

---

| ID | Regra | Histórias |
|---|---|---|
| **RN-01** | O e-mail de um usuário é único no sistema | #12 |
| **RN-02** | Uma chave de ativação nunca é vendida duas vezes | #20 #27 |
| **RN-03** | O preço de cada item é congelado no momento do checkout | #19 #28 #31 |
| **RN-04** | Não é possível comprar quantidade maior que o estoque disponível | #16 #17 |
| **RN-05** | Jogo com classificação etária acima da idade do usuário não entra no carrinho | #16 |
| **RN-06** | Um usuário avalia um jogo no máximo uma vez | #32 |
| **RN-07** | A nota de avaliação é um inteiro entre 1 e 5 | #32 |
| **RN-08** | Cancelar ou reembolsar um pedido devolve as chaves ao estoque | #23 #36 |
| **RN-09** | Cada usuário tem no máximo um carrinho aberto | #16 |
| **RN-10** | A senha tem no mínimo 8 caracteres e é armazenada somente como hash | #12 |
| **RN-11** | Jogo com pedido associado não é excluído de fato, apenas desativado | #26 |
| **RN-12** | Jogo inativo não aparece no catálogo público, mas continua visível em pedidos antigos | #14 #15 #25 #26 |
| **RN-13** | Só avalia um jogo quem possui pedido **Entregue** contendo esse jogo | #32 |
| **RN-14** | A chave só é revelada ao cliente depois que o pedido chega a **Entregue** | #21 #22 |

## Notas sobre as regras mais delicadas

**RN-02 — a regra mais importante do produto.** Duas pessoas comprando o último exemplar ao mesmo
tempo: exatamente uma conclui. É o principal risco técnico (RSK-01). Sem o teste de concorrência, a regra
é apenas uma afirmação.

**RN-03 — preço congelado.** Sem congelamento, alterar o preço no catálogo mudaria o valor de pedidos
antigos e os indicadores de venda passariam a mentir. Verificação: criar o pedido, alterar o preço do
jogo e confirmar que o total do pedido não mudou.

**RN-05 — classificação etária.** A idade é calculada pela data de nascimento na data da operação. A
verificação ocorre ao adicionar ao carrinho **e** de novo no checkout.

**RN-14 — visibilidade da chave.** Antes de Entregue, o código da chave não é enviado ao cliente (nem
mascarado). O dado que não trafega não vaza.

## Ciclo de vida do pedido

Referência para a história #18 (controle das transições).

| De | Para | Quem dispara | Observação |
|---|---|---|---|
| Carrinho | Aguardando pagamento | Cliente (checkout) | Congela preços e reserva chaves (RN-02, RN-03) |
| Carrinho | Cancelado | Cliente | Sem chaves reservadas |
| Aguardando pagamento | Pago | Cliente (pagamento simulado) | |
| Aguardando pagamento | Cancelado | Cliente | Devolve as chaves reservadas (RN-08) |
| Pago | Entregue | Sistema | Chaves passam a Vendida; código revelado (RN-14) |
| Entregue | Reembolsado | Administrador | Devolve as chaves (RN-08); só com motivo |

Qualquer outra transição é recusada. **Cancelado** e **Reembolsado** são estados finais.
