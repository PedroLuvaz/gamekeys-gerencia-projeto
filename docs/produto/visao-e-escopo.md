# Visão e escopo do produto

Responsável: **Product Owner**. Consistente com a [proposta aprovada no Sprint 0](../proposta).

---

## 1. Visão

> **Para** quem compra jogos digitais e para quem administra uma loja de chaves de ativação,
> **que precisam** de compras confiáveis e de estoque de chaves sob controle,
> **o GameKeys** é uma plataforma web de venda de jogos por chaves de ativação
> **que garante que cada chave seja entregue a um único comprador**.
> **Diferente** de planilhas e de vendas combinadas por mensagem, o GameKeys controla estoque, pedidos
> e entrega de forma automática e rastreável.

## 2. Problema

A venda de jogos digitais por chaves exige controle confiável do estoque de códigos: uma mesma chave não
pode ser entregue a mais de um comprador. Clientes precisam consultar pedidos e chaves adquiridas, e
administradores precisam gerenciar catálogo, estoque de chaves e pedidos. Sem um sistema, o risco é de
chaves duplicadas, pedidos perdidos e dados de clientes misturados.

## 3. Perfis de usuário

| Perfil | Quem é | Necessidade principal | Histórias principais |
|---|---|---|---|
| **Visitante** | Pessoa sem conta, navegando | Encontrar um jogo e decidir se compra | #14 #15 #25 #33 |
| **Cliente** | Comprador autenticado | Comprar com segurança e acessar suas chaves | #12 #13 #16 #17 #19 #21 #22 #23 #28 #32 |
| **Administrador** | Responsável pela loja | Manter catálogo e estoque e acompanhar vendas | #24 #26 #27 #29 #30 #31 |

Cada cliente tem **carrinho, pedidos, biblioteca e avaliações próprios**. Operações administrativas são
restritas ao perfil Administrador (sistema multiusuário com três perfis de acesso).

## 4. Critérios de sucesso do MVP

| Critério | Como se verifica |
|---|---|
| Nenhuma chave é vendida duas vezes | Teste automatizado de concorrência (história #20) passa |
| O preço pago nunca muda depois da compra | Teste que altera o preço do jogo depois do pedido (história #19) passa |
| Toda mudança de status de pedido é rastreável | Cada transição grava um evento com autor, origem, destino e momento (história #18) |
| Um cliente consegue ir da busca à chave na biblioteca sem ajuda | Demonstração do fluxo completo na Review da Release 2 |
| Um administrador opera a loja sem acessar o banco | Demonstração de cadastro de jogo, lote de chaves e painel de pedidos na Release 3 |

## 5. Escopo do MVP

| Épico | Histórias | Release prevista |
|---|---|---|
| **Conta e Acesso** — cadastro, login, controle de acesso por papel, perfil | #12 #13 #24 #34 | 1 e 3 |
| **Catálogo** — listagem, detalhe, busca, filtros e ordenação | #14 #15 #25 | 1 e 3 |
| **Carrinho e Pedido** — carrinho, checkout com preço congelado, reserva de chaves, pagamento simulado, biblioteca, cancelamento, histórico | #16 #17 #18 #19 #20 #21 #22 #23 #28 | 2 e 3 |
| **Administração** — jogos, chaves em lote, painel de pedidos, trilha de auditoria, indicadores | #26 #27 #29 #30 #31 | 3 e 4 |
| **Avaliações** — avaliar jogo comprado e ler avaliações | #32 #33 | 4 |

Itens de prioridade Baixa (#34 #35 #36 #37) ficam fora das sprints planejadas e entram se sobrar
capacidade. A ordem e a justificativa estão em [`priorizacao.md`](priorizacao.md).

## 6. Fora do escopo

| Item | Por que fica de fora |
|---|---|
| **Pagamento real** (cartão, PIX, gateway) | Integração externa com credencial, webhook e ambiente de teste: risco alto e nenhum aprendizado de gestão. O pagamento é **simulado**, por decisão do produto |
| Mídia física, endereço de entrega e frete | Produto é digital; elimina uma área inteira sem relação com a regra central |
| Aplicativo móvel nativo | A entrega principal é a aplicação web, acessível pelo navegador |
| Recomendação personalizada | Sem dados históricos e sem valor para o MVP |
| Funcionalidades de IA | Fora do foco da disciplina: estimativa e critério de pronto ficariam indefinidos |
| Upload de imagem | A capa do jogo é uma URL externa |
| Estorno financeiro real | Existe apenas a transição de estado do pedido |

## 7. Premissas e restrições

- **Equipe:** 3 integrantes, com os papéis girando a cada release.
- **Prazo:** 7 sprints (0 a 6), 4 releases, com recesso de 23/12 a 31/01. Calendário em
  [`calendario-de-cerimonias.md`](../gestao/calendario-de-cerimonias.md).
- **Custo:** zero. Ferramentas gratuitas e trabalho sem remuneração; o orçamento é declarado como
  restrição, e não como lacuna.
- **Stack:** Python, FastAPI, PostgreSQL, React com TypeScript e Docker (critério da disciplina:
  Java ou Python com PostgreSQL).
- **Dados:** todos os dados de demonstração são fictícios. Nenhuma chave de ativação real entra no projeto.
- **Capacidade:** estimativa inicial a validar com o time e recalibrar pelo velocity depois da Sprint 1.

## 8. Glossário

| Termo | Significado |
|---|---|
| **Chave de ativação** | Código único que o cliente usa para ativar o jogo em outra plataforma |
| **Estoque** | Quantidade de chaves de um jogo que ainda estão disponíveis (não reservadas nem vendidas) |
| **Reserva** | Chave separada para um pedido em andamento, ainda não paga |
| **Pedido** | Compra de um ou mais jogos por um cliente; começa como carrinho e percorre uma sequência de status |
| **Biblioteca** | Lista pessoal de chaves de pedidos entregues |
| **Exclusão lógica** | Jogo desativado, que sai do catálogo mas permanece nos pedidos antigos |
