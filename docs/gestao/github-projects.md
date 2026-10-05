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

As views são criadas pela interface do GitHub (a API não cria views). Configuração esperada:

| View | Layout | Configuração |
|---|---|---|
| **Board da sprint** | Board | Agrupar por Status. Filtro: `sprint:@current` |
| **Backlog** | Tabela | Campos: Título, Status, Story Points, Prioridade, Sprint, Release, Labels. Agrupar por Sprint. Ordem manual = ordem de execução |
| **Roadmap** | Roadmap | Eixo: campo Sprint. Agrupar por Release |
| **Bugs** | Tabela | Filtro: `label:bug`. Campos: Status, Sprint, Assignees |

## 5. Métricas (Insights)

Gráficos criados em **Insights** do projeto. Valores de referência para configurar:

| Métrica | Configuração do gráfico | Como ler |
|---|---|---|
| **Velocity** | Colunas. Eixo X: Sprint. Eixo Y: soma de Story Points. Filtro: `status:Concluído` | Pontos concluídos por sprint; base da capacidade da sprint seguinte |
| **Burndown da sprint** | Histórico. Filtro: `sprint:@current`. Eixo Y: soma de Story Points restantes (itens fora de Concluído) | Linha plana por 3 dias = problema não relatado; investigar na daily |
| **Fluxo** | Histórico, agrupado por Status, itens da sprint atual | Acúmulo em Em revisão indica gargalo de revisão ou de QA |

O SM tira um **print dos gráficos no dia da Review** e o anexa à ata da sprint
([`atas/`](atas)), porque o histórico do GitHub Insights muda conforme os filtros. O texto da
interpretação ("o que os números dizem e o que vamos fazer") também vai na ata.

## 6. Automações do quadro (Workflows do projeto)

Ativadas pela interface, em **Project → ⋯ → Workflows**. Ao trocar as opções de Status, confirme que cada
workflow aponta para a coluna certa:

| Workflow | Efeito |
|---|---|
| Auto-add to project | Issues e PRs do repositório entram sozinhos no quadro (Status inicial: Backlog) |
| Item closed | Status passa para **Concluído** |
| Pull request merged | Status passa para **Concluído** |
| Item reopened | Status volta para **Em andamento** |

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
6. Convidar integrantes e professora como colaboradores do repositório e do projeto.
