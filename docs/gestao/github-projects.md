# Configuração do GitHub Projects

Quadro do time: <https://github.com/users/PedroLuvaz/projects/2>, vinculado ao repositório. É a fonte das
métricas da disciplina (burndown, velocity, fluxo). **Item que não está no quadro não existe para a sprint.**

Responsável pela manutenção: **Scrum Master** da release. Esta página descreve como o quadro é
configurado e usado, para que a organização não dependa da memória de ninguém.

---

## 1. Colunas (campo Status)

```
Backlog → Pronto para a sprint → Em andamento → Em revisão → Concluído
```

| Coluna | Significa | Quem move para cá | Condição de saída |
|---|---|---|---|
| **Backlog** | Item priorizado pelo PO, ainda não puxado para uma sprint | PO | Entrar no Planning e atender ao DoR |
| **Pronto para a sprint** | Comprometido no Planning da sprint atual; atende ao DoR | Time, no Planning | Alguém se atribui e começa |
| **Em andamento** | Em desenvolvimento ou elaboração | Quem executa (limite: 1 item por pessoa) | Branch pronta e PR aberto |
| **Em revisão** | PR aberto aguardando revisão de código e validação do QA | Autor, ao abrir o PR | QA aprova, PR é mesclado e a issue fecha |
| **Concluído** | Atende integralmente ao [DoD](../produto/definition-of-done.md) | Automático, ao fechar a issue pelo merge | — |

Regras que fazem o quadro significar alguma coisa:

1. **O QA da release é a trava de qualidade.** Ele aprova o PR somente depois de validar os critérios de
   aceite e o checklist de DoD. Como o merge fecha a issue, "Concluído" só acontece depois dessa aprovação.
2. **Item reprovado volta para Em andamento**, com comentário do QA no PR dizendo o que falhou. Se o
   defeito é de algo já entregue, o QA abre uma issue `bug` ligada à história.
3. **Limites de WIP:** 1 item por pessoa em Em andamento e no máximo 3 itens em Em revisão. Estourou,
   a sprint resolve o acúmulo antes de puxar item novo.
4. **O quadro é atualizado no momento da mudança**, não na hora da daily.

## 2. Campos personalizados

| Campo | Tipo | Valores | Uso |
|---|---|---|---|
| **Story Points** | Número | 1, 2, 3, 5 (Fibonacci). Item de 8 ou mais deve ser quebrado | Estimativa de esforço relativo; base do velocity |
| **Sprint** | Iteração | Sprint 0 a Sprint 6, com as datas do [calendário](calendario-de-cerimonias.md) | Em que sprint o item está (ou está previsto) |
| **Release** | Seleção única | Release 1 a Release 4 | A qual release o item pertence |
| **Prioridade** | Seleção única | Alta, Média, Baixa | Ver escala abaixo |

A Sprint de um item de Backlog indica a **previsão** do PO; ela só vira compromisso no Planning, quando o
item passa para Pronto para a sprint.

### Escala de prioridade

| Prioridade | MoSCoW | Significa |
|---|---|---|
| **Alta** | Must have | Sem isso não há produto demonstrável |
| **Média** | Should have | Esperado pelo usuário; sai da sprint se ela estourar |
| **Baixa** | Could have | Melhora a experiência; fora das sprints planejadas, entra se sobrar capacidade |

A **ordem do backlog é a ordem de execução**. Dois itens com a mesma prioridade são desempatados pela
posição: o de cima vem primeiro. Justificativa da ordem em
[`docs/produto/priorizacao.md`](../produto/priorizacao.md).

## 3. Labels

| Label | Uso | Quem aplica |
|---|---|---|
| `user-story` | História de usuário do Product Backlog | PO |
| `bug` | Defeito registrado com passos, evidência e severidade | QA |
| `tech-debt` | Trabalho técnico sem ator de negócio | Qualquer integrante |
| `risco` | Risco do projeto (consolidado no [registro de riscos](registro-de-riscos.md)) | SM |
| `documentação` | Documentação de produto, gestão, qualidade ou ambiente | Qualquer integrante |

## 4. Views

Criadas pela interface do GitHub (a API não cria views). Em cada uma, depois de configurar, abra
**View options** (engrenagem) e clique em **Save changes**.

| View | Layout | Configuração |
|---|---|---|
| **Quadro** | Board | Column field: Status. Sem filtro. Cartões com Story Points, Prioridade e Sprint. Field sum: Story Points. Limite de coluna: Em andamento = 3 e Em revisão = 3 |
| **Sprint atual** | Board | Igual ao Quadro, com filtro `sprint:@current` |
| **Backlog** | Tabela | Campos: Title, Status, Story Points, Prioridade, Sprint, Release, Labels. Group by: Sprint. Field sum: Story Points. Ordem manual = ordem de execução |
| **Roadmap** | Roadmap | Date fields: Sprint (início e fim). Group by: Release. Zoom: Month |
| **Bugs** | Tabela | Filtro `label:bug`. Campos: Title, Status, Sprint, Assignees, Labels |

O limite de **3 itens em Em andamento** equivale a 1 item por pessoa, e o de **3 em Em revisão** vem do
[CONTRIBUTING](../../CONTRIBUTING.md).

## 5. Métricas (Insights)

Gráficos criados em **Insights** (ícone de gráfico, canto superior direito do projeto), com
**New chart**, **Configure** e **Save changes**.

| Gráfico | Configuração | Como ler |
|---|---|---|
| **Burn up** (já existe) | Gráfico histórico, filtro `sprint:@current` | Itens concluídos subindo contra o total da sprint. O trabalho que falta é a diferença entre as duas linhas, o equivalente ao burndown |
| **Velocity** | Layout: Column. X-axis: Sprint. Y-axis: Sum de Story Points. Filtro `status:Concluído` | Pontos concluídos por sprint; base da capacidade da sprint seguinte |
| **Fluxo** | Layout: Stacked column. X-axis: Sprint. Group by: Status | Acúmulo em Em revisão indica gargalo de revisão ou de QA |

O GitHub Projects não tem um gráfico de burndown pronto: o **Burn up** cumpre esse papel, e a ata de
cada Review registra a interpretação. O SM tira um **print dos gráficos no dia da Review** e o anexa à ata
([`atas/`](atas)), porque o histórico muda conforme os filtros.

## 6. Automações do quadro (Workflows)

Em **Project → ⋯ → Workflows**, abra cada workflow, clique em **Edit**, escolha o valor e clique em
**Save and turn on workflow**. Como as opções de Status foram trocadas, confirme o valor de cada um:

| Workflow | Configuração |
|---|---|
| Item added to project | Status = **Backlog** |
| Item reopened | Status = **Em andamento** |
| Item closed | Status = **Concluído** |
| Pull request merged | Status = **Concluído** |
| Auto-add to project | Repositório `PedroLuvaz/gamekeys-gerencia-projeto`, filtro `is:issue`. Novas issues entram sozinhas no quadro (as existentes já foram adicionadas) |

Os pull requests não são adicionados ao quadro: cada PR aparece como **Linked pull request** na issue
que ele fecha, e o merge fecha a issue.

## 7. Rotina de uso por cerimônia

| Cerimônia | O que acontece no quadro |
|---|---|
| **Planning** | PO apresenta o Backlog ordenado; o time estima o que falta (Planning Poker), confirma a capacidade e move os itens aceitos para Pronto para a sprint |
| **Daily assíncrona** (seg, qua, sex) | Cada um atualiza o status dos próprios itens e posta feito / próximo / impedimento |
| **Refinamento** (meio da sprint) | PO e time detalham e estimam os itens das sprints seguintes; ajustam ordem e Sprint prevista |
| **Review** | PO aceita ou rejeita cada item; o aceite fica registrado na issue |
| **Retrospectiva** | SM anexa os gráficos do Insights e registra ações; itens não concluídos voltam ao Backlog com nova previsão |

## 8. Como reproduzir a configuração do zero

1. Criar o projeto em **Projects → New project** e vinculá-lo ao repositório.
2. Em **Status**, trocar as opções padrão pelas cinco colunas da seção 1.
3. Criar os campos Story Points (Número), Sprint (Iteração), Release e Prioridade (Seleção única).
4. Criar as views da seção 4 e os gráficos da seção 5.
5. Ativar as automações da seção 6.
6. Em **Settings → Manage access**, convidar integrantes (Write) e professora (Read) como colaboradores.
