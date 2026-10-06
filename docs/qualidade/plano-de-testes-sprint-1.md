# Plano de testes — Sprint 1 (Release 1)

Responsável: **QA** da release. Período da sprint: **20/10 a 29/10/2026**. Estratégia geral e métricas em
[`plano-de-qualidade.md`](plano-de-qualidade.md).

**Estado:** casos de teste escritos na Sprint 0 a partir dos cenários de aceite (Dado que / Quando / Então) das issues. **Nenhum foi
executado ainda**: a execução acontece conforme os PRs da Sprint 1 chegarem. O Sprint Goal está em
[`sprint-goals.md`](../produto/sprint-goals.md).

---

## 1. Escopo

| Issue | História | Pts | Cenários de aceite |
|---|---|---|---|
| [#12](https://github.com/PedroLuvaz/gamekeys-gerencia-projeto/issues/12) | Cadastro de cliente | 3 | 6 |
| [#13](https://github.com/PedroLuvaz/gamekeys-gerencia-projeto/issues/13) | Login com e-mail e senha | 5 | 5 |
| [#14](https://github.com/PedroLuvaz/gamekeys-gerencia-projeto/issues/14) | Listagem paginada de jogos | 5 | 6 |
| [#15](https://github.com/PedroLuvaz/gamekeys-gerencia-projeto/issues/15) | Detalhe do jogo | 2 | 4 |

**Fora do escopo desta sprint:** carrinho, pedido, administração e avaliações (sprints seguintes).

## 2. Abordagem

- Cada **cenário de aceite** (exceção ou sucesso) tem ao menos **um caso de teste**. A numeração dos cenários
  (C1, C2…) segue a ordem em que aparecem na issue (Cenário 1, Cenário 2…).
- Comportamento de API: **teste automatizado** (pytest + httpx), escrito junto da história e verificado pelo QA.
- Telas do front-end: **teste manual** seguindo os passos do caso.
- Banco de teste isolado; **sem mock de banco**.
- Dados: o seed da história #14 (20 jogos ou mais, alguns sem chave disponível).

## 3. Ambiente

| Item | Valor |
|---|---|
| Ambiente | Local, conforme [`ambiente-de-desenvolvimento.md`](../devops/ambiente-de-desenvolvimento.md) |
| Dados | Seed de demonstração (fictícios) |
| Navegadores (testes manuais) | Chrome e Firefox, versões atuais |
| Pipeline | O CI precisa estar verde no PR antes da validação manual |

## 4. Cronograma

| Quando | Atividade |
|---|---|
| Até 20/10 (Planning) | Casos revisados com o PO; cenários ambíguos ajustados antes de entrar na sprint |
| 22/10 a 28/10 | Execução dos casos conforme os PRs são abertos; bugs registrados |
| 27/10 a 28/10 | Regressão completa dos casos da sprint |
| 29/10 (antes da Review) | Relatório de qualidade da sprint e dados das métricas M1 a M9 |

## 5. Critérios de entrada e de saída

| | Critério |
|---|---|
| **Entrada (por item)** | PR aberto, CI verde, cenários claros na issue |
| **Saída (por item)** | Todos os casos do item aprovados e DoD validado pelo QA |
| **Saída (sprint)** | Nenhum bug crítico ou alto aberto; regressão executada; relatório publicado |

## 6. Casos de teste

Legenda de **Tipo**: **A** = automatizado (API) · **M** = manual (tela) · **A+M** = ambos.
**Status** inicial de todos os casos: _Não executado_.

### #12 — Cadastro de cliente

| ID | Cenário | Pré-condição | Passos | Resultado esperado | Tipo |
|---|---|---|---|---|---|
| CT-12-01 | C1 | Nenhuma conta com o e-mail usado | 1. Enviar cadastro com nome, e-mail, senha de 8+ caracteres e data de nascimento válidos | Conta criada com papel Cliente; usuário é avisado do sucesso | A+M |
| CT-12-02 | C4 | — | 1. Enviar cadastro sem nome, depois sem e-mail, sem senha e sem data de nascimento | Cada envio é rejeitado com mensagem indicando o campo obrigatório; nenhuma conta criada | A+M |
| CT-12-03 | C2 | Já existe conta com o e-mail `a@teste.com` | 1. Cadastrar de novo com `a@teste.com` | Mensagem clara de e-mail em uso; total de contas não aumenta | A+M |
| CT-12-04 | C2 | Conta com `a@teste.com` existe | 1. Cadastrar com `A@TESTE.COM` | Tratado como e-mail em uso, sem distinção de maiúsculas (derivado de RN-01; se o PO decidir o contrário, o caso é ajustado) | A |
| CT-12-05 | C3 | — | 1. Cadastrar com senha de 7 caracteres 2. Repetir com 8 caracteres | 7 caracteres: rejeitada, com mensagem do mínimo. 8 caracteres: aceita (valor-limite) | A+M |
| CT-12-06 | C5 | Conta criada no CT-12-01 | 1. Inspecionar a resposta do cadastro e do login 2. Consultar o registro no banco | Resposta não contém a senha; o banco guarda apenas o hash, diferente da senha em texto | A |
| CT-12-07 | C6 | — | 1. Enviar cadastro incluindo o campo de papel com valor Administrador | Conta criada como Cliente (ou envio rejeitado); nunca como Administrador | A |

### #13 — Login com e-mail e senha

| ID | Cenário | Pré-condição | Passos | Resultado esperado | Tipo |
|---|---|---|---|---|---|
| CT-13-01 | C1 | Cliente cadastrado | 1. Fazer login com e-mail e senha corretos | Recebe token, prazo de expiração de 60 minutos e o papel Cliente | A+M |
| CT-13-02 | C2 | Cliente cadastrado | 1. Login com senha incorreta | Mensagem genérica de credenciais inválidas | A+M |
| CT-13-03 | C2 | — | 1. Login com e-mail que não existe | **Mesma** mensagem do CT-13-02, sem revelar se o e-mail existe | A+M |
| CT-13-04 | C3 | — | 1. Acessar uma área protegida com token adulterado | Acesso negado; na tela, redirecionado ao login | A+M |
| CT-13-05 | C3 | Token com validade vencida (expiração reduzida no teste) | 1. Acessar uma área protegida com o token vencido | Acesso negado; na tela, redirecionado ao login | A |
| CT-13-06 | C4 | Cliente autenticado | 1. Recarregar a página | Continua autenticado enquanto o token for válido | M |
| CT-13-07 | C5 | Cliente autenticado | 1. Clicar em sair (logout) 2. Tentar voltar a uma área protegida | Sessão encerrada; áreas protegidas exigem novo login | M |

### #14 — Listagem paginada de jogos

| ID | Cenário | Pré-condição | Passos | Resultado esperado | Tipo |
|---|---|---|---|---|---|
| CT-14-01 | C1 | Catálogo com 25 jogos ativos | 1. Abrir a listagem 2. Ir para a página 2 | Página 1 com 20 jogos; página 2 com 5; total de resultados e navegação visíveis | A+M |
| CT-14-02 | C2 | Seed carregado | 1. Observar os cards da listagem | Cada card mostra capa, título, preço, plataforma e disponibilidade | M |
| CT-14-03 | C3 | Um jogo sem chave disponível e um com chaves | 1. Observar a disponibilidade de cada um | Sem chave: **Esgotado**. Com chave: **Em estoque** | A+M |
| CT-14-04 | C4 | Um jogo marcado como inativo | 1. Abrir a listagem | O jogo inativo não aparece (RN-12) | A |
| CT-14-05 | C5 | — | 1. Simular a API lenta 2. Simular catálogo vazio 3. Simular API fora do ar | Mensagem de carregamento, de lista vazia e de erro, respectivamente; nunca tela em branco | M |
| CT-14-06 | C6 | Banco recém-criado | 1. Rodar o seed 2. Contar jogos e verificar disponibilidade | 20 jogos ou mais; ao menos alguns esgotados; dados fictícios | A |

### #15 — Detalhe do jogo

| ID | Cenário | Pré-condição | Passos | Resultado esperado | Tipo |
|---|---|---|---|---|---|
| CT-15-01 | C1 | Jogo ativo com todos os campos | 1. Abrir o detalhe a partir da listagem | Mostra capa, título, descrição, gênero, plataforma, classificação etária, preço e disponibilidade | A+M |
| CT-15-02 | C2 | Jogo esgotado | 1. Abrir o detalhe | Ação de compra desabilitada, com aviso de indisponibilidade | M |
| CT-15-03 | C3 e C4 | — | 1. Abrir o endereço de um jogo que não existe 2. Abrir o endereço de um jogo inativo (RN-12) | Mensagem amigável de não encontrado nos dois casos | A+M |

**Total: 23 casos** (7 + 7 + 6 + 3).

## 7. Rastreabilidade

| Issue | Cenário | Casos de teste |
|---|---|---|
| #12 | C1 Cadastro válido | CT-12-01 |
| #12 | C2 E-mail já cadastrado | CT-12-03, CT-12-04 |
| #12 | C3 Senha curta | CT-12-05 |
| #12 | C4 Campo obrigatório em branco | CT-12-02 |
| #12 | C5 Senha protegida | CT-12-06 |
| #12 | C6 Tentativa de criar administrador | CT-12-07 |
| #13 | C1 Login válido | CT-13-01 |
| #13 | C2 Credenciais inválidas | CT-13-02, CT-13-03 |
| #13 | C3 Acesso inválido ou expirado | CT-13-04, CT-13-05 |
| #13 | C4 Sessão mantida | CT-13-06 |
| #13 | C5 Logout | CT-13-07 |
| #14 | C1 Lista paginada | CT-14-01 |
| #14 | C2 Dados de cada jogo | CT-14-02 |
| #14 | C3 Jogo esgotado | CT-14-03 |
| #14 | C4 Jogo inativo | CT-14-04 |
| #14 | C5 Lista vazia ou falha | CT-14-05 |
| #14 | C6 Dados de demonstração | CT-14-06 |
| #15 | C1 Detalhe completo | CT-15-01 |
| #15 | C2 Jogo esgotado | CT-15-02 |
| #15 | C3 Jogo inexistente | CT-15-03 |
| #15 | C4 Jogo inativo | CT-15-03 |

**Cobertura (M2):** 21 de 21 cenários de aceite com ao menos 1 caso de teste = **100%**.

Os testes automatizados usam o ID do caso no nome da função (por exemplo, `test_ct_12_03_email_duplicado`),
para ligar o caso ao código.

## 8. Registro de execução

Preenchido pelo QA durante a sprint. Cada falha gera uma issue `bug` e o número vai na última coluna.

| Data | Caso | Resultado (Aprovado / Reprovado) | Executor | Evidência | Bug aberto |
|---|---|---|---|---|---|
| | | | | | |

## 9. Bugs encontrados

Nenhum registrado até aqui: os primeiros bugs surgem da execução dos casos durante a Sprint 1, e serão
listados em issues com o label `bug`.

## 10. Relatório de qualidade da sprint

A ser preenchido antes da Review de 29/10, com as métricas M1 a M9 do
[plano de qualidade](plano-de-qualidade.md).

| Métrica | Valor | Meta |
|---|---|---|
| M1 Conformidade com o DoD | | 100% |
| M2 Cobertura de cenários de aceite | 100% (planejada) | 100% |
| M3 Taxa de aprovação dos casos | | ≥ 90% |
| M4 Bugs abertos críticos/altos | | 0 |
| M5 Bugs corrigidos ÷ encontrados | | ≥ 80% |
| M6 Escape de defeitos | | tendência decrescente |
| M7 Sucesso do pipeline | | ≥ 80% (100% na `main`) |
| M8 Tempo para corrigir build quebrado | | ≤ 1 dia útil |
| M9 Tempo até a primeira revisão de PR | | ≤ 24 h |
