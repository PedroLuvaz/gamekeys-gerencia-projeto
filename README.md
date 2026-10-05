# GameKeys — Plataforma web de venda de jogos digitais por chaves de ativação

![CI](https://github.com/PedroLuvaz/gamekeys-gerencia-projeto/actions/workflows/ci.yml/badge.svg)

Projeto da disciplina **CPT01096 — Gerência de Projeto** · Ciência da Computação · UEPB · 2026.2
Professora: **Ana Isabella Muniz Leite**

> A disciplina avalia o **processo e os artefatos de gestão**, não o código. Este repositório é a
> evidência do processo: backlog, board, cerimônias, métricas, qualidade e pipeline estão aqui.
> Ponto de partida para avaliação: [Gestão](#6-gestão-do-projeto) e [Estado do projeto](#8-estado-do-projeto).

---

## 1. O problema

Quem vende jogos digitais por **chaves de ativação** precisa garantir que a mesma chave nunca seja
entregue a dois compradores. Ao mesmo tempo, o cliente precisa consultar seus pedidos e suas chaves
adquiridas, e o administrador precisa gerenciar catálogo, estoque de chaves e pedidos.

O GameKeys organiza esse processo em um único sistema, reduzindo o risco de **chave duplicada**,
mantendo os dados de cada usuário **separados** e as mudanças de estado dos pedidos **rastreáveis**.

## 2. Solução

Aplicação web em que:

- **Visitantes** navegam, pesquisam e filtram o catálogo;
- **Clientes** mantêm carrinho, finalizam a compra com pagamento simulado, recebem automaticamente uma
  chave disponível e consultam sua biblioteca pessoal;
- **Administradores** cadastram jogos, inserem lotes de chaves, acompanham pedidos e veem indicadores.

| Perfil | Pode |
|---|---|
| Visitante | Navegar, buscar e filtrar o catálogo; ver detalhe e avaliações dos jogos |
| Cliente | Tudo do visitante, mais carrinho, compra, biblioteca de chaves, histórico de pedidos e avaliações |
| Administrador | Gerenciar jogos e chaves, acompanhar pedidos, ver trilha de auditoria e indicadores |

**Dentro do MVP:** cadastro e autenticação; controle de acesso por papel; catálogo com busca, filtros,
ordenação e paginação; carrinho persistido; checkout com congelamento de preço; pagamento simulado;
reserva e entrega automática de chaves únicas; biblioteca do cliente; painel administrativo;
avaliações de compradores; trilha de auditoria dos pedidos.

**Fora do MVP:** pagamento real, mídia física, frete, aplicativo móvel nativo, recomendação
personalizada e funcionalidades de IA. Detalhes em [`docs/produto/visao-e-escopo.md`](docs/produto/visao-e-escopo.md).

## 3. Stack

Back-end **Python 3.12 + FastAPI** · banco **PostgreSQL 16** · front-end **React + TypeScript** ·
API REST com autenticação JWT · CI com **GitHub Actions** · ambiente conteinerizado com **Docker**.
Ambiente de desenvolvimento: [`docs/devops/ambiente-de-desenvolvimento.md`](docs/devops/ambiente-de-desenvolvimento.md).

## 4. Equipe e papéis

| Integrante | Papel na Release 1 (Sprints 0 e 1) |
|---|---|
| Pedro Lucas Vaz de Andrade | **Product Owner** |
| Wagner Tiburcio da Silva Junior | **QA** (Analista de Qualidade) |
| Rodrigo Almeida Gomes | **Scrum Master** |
| _(a definir pela equipe)_ | **DevOps** — papel acumulado por um dos integrantes na Release 1 |

Os papéis giram ao fim de cada release. Rodízio previsto na [programação da disciplina](#5-calendário):

| Release | Sprints | Rotação de papéis em |
|---|---|---|
| 1 | 0 e 1 | 29/10/2026 |
| 2 | 2 e 3 | 26/11/2026 |
| 3 | 4 e 5 | 22/12/2026 |
| 4 | 6 | — (Demo Day final) |

## 5. Calendário

| Sprint | Release | Período | Planning | Review + Retrospectiva |
|---|---|---|---|---|
| 0 | 1 | 06/10 a 15/10 | 06/10 (abertura) | 15/10 (interna) |
| 1 | 1 | 20/10 a 29/10 | 20/10 | 29/10 · **fim da Release 1** |
| 2 | 2 | 03/11 a 12/11 | 03/11 | 12/11 |
| 3 | 2 | 17/11 a 26/11 | 17/11 | 26/11 · **fim da Release 2** |
| 4 | 3 | 01/12 a 10/12 | 01/12 | 10/12 |
| 5 (curta) | 3 | 15/12 a 22/12 | 15/12 | 22/12 · **fim da Release 3** |
| — | — | Recesso de 23/12/2026 a 31/01/2027 | — | — |
| 6 | 4 | 02/02 a 18/02/2027 | 02/02 | 16/02 e 18/02 · **Demo Day final** |

Cerimônias, horários e regras: [`docs/gestao/calendario-de-cerimonias.md`](docs/gestao/calendario-de-cerimonias.md).

## 6. Gestão do projeto

| O quê | Onde |
|---|---|
| Quadro do time (GitHub Projects) | Aba **Projects** do repositório — configuração em [`docs/gestao/github-projects.md`](docs/gestao/github-projects.md) |
| Product Backlog | [Issues](../../issues) com label `user-story`, ordenadas no quadro |
| Visão, escopo e regras de negócio | [`docs/produto/`](docs/produto) |
| Priorização justificada e carga por sprint | [`docs/produto/priorizacao.md`](docs/produto/priorizacao.md) |
| Definition of Ready e Definition of Done | [`docs/produto/definition-of-done.md`](docs/produto/definition-of-done.md) |
| Sprint Goals | [`docs/produto/sprint-goals.md`](docs/produto/sprint-goals.md) |
| Acordos de trabalho e cerimônias | [`docs/gestao/`](docs/gestao) |
| Registro de riscos | [`docs/gestao/registro-de-riscos.md`](docs/gestao/registro-de-riscos.md) |
| Atas de planning, review e retrospectiva | [`docs/gestao/atas/`](docs/gestao/atas) |
| Plano de qualidade, de testes e bugs | [`docs/qualidade/`](docs/qualidade) · issues com label `bug` |
| Pipeline de CI | [`.github/workflows/ci.yml`](.github/workflows/ci.yml) · aba **Actions** |
| Como contribuir (branches, commits, PR) | [`CONTRIBUTING.md`](CONTRIBUTING.md) |
| Proposta aprovada no Sprint 0 | [`docs/proposta/`](docs/proposta) |

### Labels

| Label | Uso |
|---|---|
| `user-story` | História de usuário do Product Backlog |
| `bug` | Defeito registrado pelo QA, com passos, evidência e severidade |
| `tech-debt` | Trabalho técnico sem ator de negócio (infraestrutura, refatoração) |
| `risco` | Risco do projeto |
| `documentação` | Documentação de produto, gestão, qualidade ou ambiente |

## 7. Estrutura do repositório

```
.
├── .github/
│   ├── ISSUE_TEMPLATE/      # modelos de user story e de bug
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── workflows/ci.yml     # lint e testes a cada push
├── backend/                 # API FastAPI (esqueleto da Sprint 0)
├── docs/
│   ├── devops/              # ambiente de desenvolvimento
│   ├── gestao/              # acordos, calendário, riscos, atas, GitHub Projects
│   ├── produto/             # visão, regras de negócio, DoD, priorização, sprint goals
│   ├── proposta/            # proposta aprovada
│   └── qualidade/           # plano de qualidade e plano de testes
├── CONTRIBUTING.md
└── README.md
```

O diretório `frontend/` será criado na Sprint 1, junto com a primeira história que o exige.

## 8. Estado do projeto

| Release | Sprint | Objetivo | Status |
|---|---|---|---|
| 1 | 0 | Repositório, board, backlog inicial e planos de gestão e qualidade | Em andamento |
| 1 | 1 | Visitante vê o catálogo; cliente cria conta e entra | Planejada |
| 2 | 2 | Cliente monta o carrinho | Prevista |
| 2 | 3 | Compra ponta a ponta com entrega de chave | Prevista |
| 3 | 4 | Biblioteca, cancelamento, controle de acesso e busca | Prevista |
| 3 | 5 | Administrador gerencia jogos e chaves | Prevista |
| 4 | 6 | Painel, indicadores, avaliações e Demo Day | Prevista |

Sprints 2 a 6 são previsões: o escopo é confirmado em cada Planning, com base na velocity medida.
