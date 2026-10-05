# Ambiente de desenvolvimento

Guia para qualquer integrante preparar o ambiente e rodar o projeto do zero. Instalação, testes, lint e
subida da API foram executados em um ambiente virtual novo (Windows 11, Python 3.12) durante a Sprint 0.
Cada integrante deve repetir o passo a passo na própria máquina e registrar problemas como issue.

**Objetivo (marco M1):** qualquer integrante clona o repositório, roda os testes e sobe a API em menos
de 10 minutos.

---

## 1. Pré-requisitos

| Ferramenta | Versão | Para quê | Obrigatório na Sprint 0 |
|---|---|---|---|
| Git | 2.40+ | Controle de versão | Sim |
| Python | 3.12 | Back-end | Sim |
| Conta no GitHub com acesso ao repositório | — | Branches, PRs, board | Sim |
| Node.js | 20 LTS ou superior | Front-end (a partir da Sprint 1) | Não |
| Docker Desktop | Recente | PostgreSQL local (a partir da Sprint 1) | Não |

O banco PostgreSQL e o front-end só entram com a primeira história que os exige (Sprint 1). Até lá, o
ambiente é Python + Git.

## 2. Primeira execução

```bash
git clone git@github.com:PedroLuvaz/gamekeys-gerencia-projeto.git
cd gamekeys-gerencia-projeto/backend

python -m venv .venv
```

Ative o ambiente virtual:

| Sistema | Comando |
|---|---|
| Windows (PowerShell) | `.venv\Scripts\Activate.ps1` |
| Windows (Git Bash) | `source .venv/Scripts/activate` |
| Linux e macOS | `source .venv/bin/activate` |

Instale as dependências, incluindo as de desenvolvimento:

```bash
pip install -e ".[dev]"
```

## 3. Comandos do dia a dia

Todos executados em `backend/`, com o ambiente virtual ativo. São os **mesmos comandos do CI**: se
passam na sua máquina, passam no pipeline.

| Objetivo | Comando |
|---|---|
| Rodar os testes | `pytest` |
| Verificar o lint | `ruff check .` |
| Verificar a formatação | `ruff format --check .` |
| Corrigir a formatação | `ruff format .` |
| Subir a API com recarga automática | `uvicorn app.main:app --reload` |

Com a API no ar:

- Verificação de saúde: <http://127.0.0.1:8000/saude> → `{"status":"ok"}`
- Documentação interativa (OpenAPI): <http://127.0.0.1:8000/docs>

## 4. Pipeline de CI

Arquivo: [`.github/workflows/ci.yml`](../../.github/workflows/ci.yml). Dispara a **cada push**, em
qualquer branch, e também manualmente (aba **Actions → CI → Run workflow**).

| Etapa | Comando | Falha quando |
|---|---|---|
| Instalar dependências | `pip install -e ".[dev]"` | Dependência inexistente ou conflito |
| Lint | `ruff check .` | Erro de estilo ou import não usado |
| Formatação | `ruff format --check .` | Arquivo fora do padrão |
| Testes | `pytest -v` | Qualquer teste falha |

O resultado aparece na aba **Actions**, no PR e no selo do README. É a fonte da métrica "taxa de sucesso
do pipeline" do [plano de qualidade](../qualidade/plano-de-qualidade.md).

**Build quebrado é prioridade.** Quem quebrou corrige na hora; se não puder, avisa o grupo. O tempo até
o conserto é registrado como métrica de resposta a falhas.

## 5. Fluxo de branches

Resumo; o detalhe está no [CONTRIBUTING](../../CONTRIBUTING.md).

```
main  ●──────●──────●──────●        (sempre estável, só recebe PR com squash)
       \    /  \    /
        ●──●    ●──●                branches curtas: <tipo>/<n>-<descricao>
```

Proteção recomendada para `main` (Settings → Branches → Add rule): exigir pull request, exigir 1
aprovação e exigir o check `backend` verde.

## 6. Estrutura do repositório

```
backend/
├── app/                 # código da API (FastAPI)
│   └── main.py          # aplicação e rota /saude
├── tests/               # testes automatizados (pytest)
└── pyproject.toml       # dependências, ruff e pytest
```

A estrutura em módulos (`conta`, `catalogo`, `pedido`, `admin`, `avaliacao`) é criada junto com as
primeiras histórias da Sprint 1, e não antes: cada pasta nasce quando existe uma história que a usa.

## 7. Problemas comuns

| Sintoma | Causa provável | Solução |
|---|---|---|
| `python` não encontrado no Windows | Python fora do PATH | Use `py -3.12 -m venv .venv` |
| PowerShell bloqueia o `Activate.ps1` | Política de execução | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| `ModuleNotFoundError: app` ao rodar `pytest` | Pacote não instalado | Rode `pip install -e ".[dev]"` dentro de `backend/` |
| `ruff format --check` falha no CI | Arquivo não formatado | Rode `ruff format .` e faça novo commit |
| Aviso do Starlette sobre `httpx` nos testes | Aviso de depreciação, não é erro | Pode ser ignorado por enquanto |

## 8. Próximos passos de infraestrutura

Registrados como histórias técnicas do backlog quando entram em uma sprint:

- Docker Compose com PostgreSQL 16 e a API (Sprint 1, junto com o modelo de dados do catálogo)
- Migrations com Alembic (Sprint 1)
- Job de front-end no CI, quando o diretório `frontend/` existir
- Deploy automatizado em homologação e tag de versão da release (Release 2)
