# Guia de contribuição

O histórico do Git, as issues e os pull requests são critério de avaliação da disciplina. A mensagem
de commit e o PR são o documento que a professora lê para entender **quem fez o quê, quando e por
quê**. Este guia padroniza isso para os três integrantes.

---

## 1. Fluxo de trabalho

```
Backlog → Pronto para a sprint → Em andamento → Em revisão → Concluído
```

1. O PO ordena o Backlog. No **Planning**, os itens da sprint vão para **Pronto para a sprint**.
2. Quem vai executar se atribui à issue e move para **Em andamento** (limite: 1 item por pessoa).
3. Crie a branch a partir da `main` atualizada e faça commits pequenos e frequentes.
4. Abra o **pull request** com `Closes #<n>` e mova a issue para **Em revisão**.
5. Outro integrante revisa. O **QA da release** valida os critérios de aceite e a Definition of Done,
   registra isso no checklist do PR e aprova.
6. Merge com **squash**. A issue fecha e vai para **Concluído**.

Item reprovado pelo QA volta para **Em andamento**, com comentário no PR dizendo o que falhou. Se for
defeito de algo já entregue, o QA abre uma issue `bug` ligada à história.

**Limites de WIP:** 1 item em Andamento por pessoa; no máximo 3 em Revisão. Se estourar, o time resolve
o acúmulo antes de puxar item novo.

Colunas, campos e critérios de entrada/saída: [`docs/gestao/github-projects.md`](docs/gestao/github-projects.md).

## 2. Branches

```
<tipo>/<numero-da-issue>-<descricao-curta-em-kebab-case>
```

| Tipo | Uso |
|---|---|
| `feature/` | Nova funcionalidade vinda de uma user story |
| `fix/` | Correção de bug |
| `chore/` | Infraestrutura, configuração, pipeline |
| `docs/` | Somente documentação |
| `refactor/` | Mudança interna sem alterar comportamento |

Exemplos: `feature/16-adicionar-ao-carrinho` · `fix/52-total-do-carrinho` · `docs/3-acordos-de-trabalho`

- A `main` é a única branch de longa duração e deve estar sempre estável.
- Ninguém faz commit direto na `main`: toda mudança entra por pull request.
- **Vida máxima da branch: 3 dias.** Passou disso, a história era grande e deveria ter sido quebrada.
- Proteção recomendada para a `main`: exigir PR, 1 aprovação e o check `backend` do CI verde.

## 3. Mensagem de commit

Conventional Commits com o número da issue:

```
<tipo>(<escopo>): <descrição no imperativo, minúscula, sem ponto final> (#<n>)
```

**Tipos:** `feat` · `fix` · `docs` · `test` · `refactor` · `chore` · `ci`
**Escopos:** `conta` · `catalogo` · `pedido` · `admin` · `avaliacao` · `infra` · `gestao` · `produto` · `qualidade`

```
feat(pedido): reserva chaves com SKIP LOCKED no checkout (#20)
fix(carrinho): recalcula total ao remover item (#52)
docs(gestao): adiciona acordos de trabalho do time (#3)
ci(infra): executa ruff e pytest a cada push (#10)
```

| Mau exemplo | Por quê |
|---|---|
| `ajustes` | Não diz o que mudou nem em qual história |
| `fix bug` | Qual bug? Em quê? |
| `#20` | Sem descrição |
| `WIP` | Não vai para a `main` |

Quando duas pessoas trabalham juntas, registre as duas:

```
Co-authored-by: Nome do Colega <email@exemplo.com>
```

## 4. Pull request

- **Título:** `<descrição> (#<n>)`, igual à convenção de commit (o squash usa o título).
- **Corpo:** preencha o [modelo do PR](.github/PULL_REQUEST_TEMPLATE.md): issue, o que mudou, como
  testar e o checklist da Definition of Done.
- **Tamanho:** até cerca de 400 linhas alteradas. PR maior não é revisado de verdade.
- **Revisão em até 24 h.** Passou disso, cobre no grupo — PR parado bloqueia a sprint.
- Comentário de revisão descreve o problema, não julga a pessoa.

## 5. Distribuição do trabalho

O critério da disciplina é **distribuição equilibrada** entre os integrantes e evidência de cada
papel. Duas regras:

- Na Planning, distribua as histórias para que cada integrante toque áreas diferentes ao longo do
  projeto.
- Não crie commits artificiais para inflar contagem. Desequilíbrio se corrige redistribuindo
  trabalho na sprint seguinte, e a decisão vai para a ata da retrospectiva.

Verificação na retrospectiva:

```bash
git shortlog -sn --all
```

## 6. Nunca vai para o repositório

- Arquivo `.env` com credencial real
- `node_modules/`, `__pycache__/`, `.venv/`, `dist/`
- Dump de banco com dado real
- Chave de ativação verdadeira — todos os dados de demonstração são fictícios
- Código comentado "para o caso de precisar" — o Git já guarda o histórico
