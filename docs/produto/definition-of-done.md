# Definition of Ready e Definition of Done

Acordadas com o time. Alteração só entra por PR, com o aceite dos três integrantes, normalmente na
retrospectiva.

**Status:** proposta do PO, a ser aceita pelo time no PR que a incorpora à `main`.

| Aceite | Integrante | Papel (Release 1) | Data |
|---|---|---|---|
| [ ] | Pedro Lucas Vaz de Andrade | Product Owner | |
| [ ] | Wagner Tiburcio da Silva Junior | QA e DevOps | |
| [ ] | Rodrigo Almeida Gomes | Scrum Master | |

---

## 1. Definition of Ready (DoR)

Uma história só passa para **Pronto para a sprint** se:

- [ ] Está no formato **Como… quero… para…**, com o ator identificado
- [ ] Tem **critérios de aceite verificáveis** (nada de "funcionar bem")
- [ ] Foi **estimada** pelo time (Planning Poker) e vale **no máximo 5 pontos**
- [ ] Referencia a **regra de negócio** correspondente, quando houver
- [ ] Não depende de item que não esteja na sprint nem já concluído
- [ ] Tem **Prioridade**, **Release** e **Sprint** preenchidos no quadro
- [ ] O time não tem dúvida pendente com o PO sobre o que se espera

Quem verifica: o **PO** prepara; o **time** confirma no Planning. Item que não atende ao DoR não é
puxado para a sprint.

## 2. Definition of Done (DoD) do item

Um item só vai para **Concluído** se **todos** os pontos abaixo forem verdadeiros. O autor marca o
checklist no PR e o **QA valida ao aprovar**.

- [ ] Todos os **critérios de aceite** da issue foram validados pelo QA
- [ ] O código foi **revisado e aprovado por outro integrante** em pull request
- [ ] Há **testes automatizados** para os critérios comportamentais, e eles passam
- [ ] O **CI está verde** na branch e permanece verde na `main` após o merge
- [ ] A **documentação foi atualizada**, se a mudança afeta regras, fluxos ou ambiente
- [ ] Não há `TODO`, código comentado nem dado sensível no que foi entregue
- [ ] O PR segue o padrão (`<tipo>(<escopo>): descrição (#n)`, com `Closes #n`)
- [ ] A issue está com os campos do quadro corretos (Sprint, Release, Story Points)

### Variante para itens de documentação e gestão

Para issues com labels `documentação` ou `tech-debt` sem código de produto:

- [ ] Entregáveis da issue estão no repositório, com links funcionando
- [ ] Foi revisado e aprovado por outro integrante
- [ ] Quem exerce o papel responsável é o autor dos commits (ou há `Co-authored-by`)
- [ ] O índice (README ou `docs/`) aponta para o novo documento

## 3. Definition of Done da sprint

Ao fim da sprint, na Review:

- [ ] Todos os itens aceitos pelo PO estão em **Concluído**
- [ ] O incremento está **integrado na `main`** e funciona a partir do repositório
- [ ] O PO registrou **aceite ou rejeição** de cada item na issue
- [ ] O Sprint Goal foi avaliado (atingido, parcial ou não) e registrado na ata
- [ ] Métricas atualizadas no quadro (burndown, velocity e fluxo) e anexadas à ata
- [ ] Item não concluído voltou ao Backlog com nova previsão e motivo registrado

### Ao fim de uma release

- [ ] **Release notes** publicadas, a partir do [modelo](release-notes/modelo.md)
- [ ] **Tag de versão** criada no repositório (`v<release>.0.0`)
- [ ] Relatório de qualidade da release publicado pelo QA
- [ ] Rotação de papéis registrada na ata da retrospectiva

## 4. Por que o QA fecha a porta

O QA da release aprova o PR somente depois de validar os critérios de aceite. Como o merge fecha a issue
e o quadro move o item para Concluído, **ninguém conclui o próprio trabalho sozinho**. Isso dá ao papel
de QA um registro objetivo no histórico do GitHub.
