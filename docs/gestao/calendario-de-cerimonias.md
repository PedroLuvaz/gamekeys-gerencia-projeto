# Calendário de cerimônias

Datas extraídas da programação oficial da disciplina (_Gerência de Projeto 2026.2_). As aulas são às
**terças e quintas** (em fevereiro, **segundas e quartas**) e cada aula é uma oportunidade de cerimônia
ou de desenvolvimento.

---

## 1. Cadência padrão de cada sprint

| Cerimônia | Quando | Duração | Quem conduz | Entrada | Saída e registro |
|---|---|---|---|---|---|
| **Sprint Planning** | 1ª aula da sprint | 60 min | SM | Backlog ordenado pelo PO, velocity da sprint anterior, [DoR](../produto/definition-of-done.md) | Sprint Goal, itens em Pronto para a sprint e ata de planning |
| **Daily assíncrona** | Seg, qua e sex | 5 min por pessoa | Cada integrante | Quadro atualizado | Mensagem: feito / vou fazer / impedimento |
| **Refinamento do Backlog** | 3ª aula da sprint (meio) | 20 min | PO | Itens das próximas sprints | Itens detalhados e estimados; ordem revista |
| **Sprint Review** | Última aula da sprint | 30 min | PO | Incremento da sprint | Aceite ou rejeição de cada item na issue; ata de review |
| **Retrospectiva** | Logo após a Review | 30 min | SM | Métricas do quadro, ações da retrospectiva anterior | Até 3 ações com responsável e prazo; ata de retrospectiva |

Nas demais aulas (_Desenvolvimento e dúvidas_) o time trabalha nos itens da sprint e tira dúvidas com a
professora.

## 2. Calendário por sprint

| Sprint | Release | Planning | Refinamento | Desenvolvimento | Review + Retrospectiva |
|---|---|---|---|---|---|
| **0** | 1 | ter 06/10 (abertura) | ter 13/10 | qui 08/10 | qui 15/10 (interna) |
| **1** | 1 | ter 20/10 | ter 27/10 | qui 22/10 | **qui 29/10** — fim da Release 1 |
| **2** | 2 | ter 03/11 | ter 10/11 | qui 05/11 | qui 12/11 |
| **3** | 2 | ter 17/11 | ter 24/11 | qui 19/11 | **qui 26/11** — fim da Release 2 |
| **4** | 3 | ter 01/12 | ter 08/12 | qui 03/12 | qui 10/12 |
| **5 (curta)** | 3 | ter 15/12 | qui 17/12 (curto) | — | **ter 22/12** — fim da Release 3 |
| **6** | 4 | seg 02/02 | seg 09/02 | qua 04/02 e qua 11/02 (ensaio do Demo Day) | seg 16/02 e **qua 18/02 — Demo Day final** |

Recesso: **23/12/2026 a 31/01/2027**, sem aulas. Prova final: segunda, 23/02/2027.

### Rodízio de papéis

| Release | Fim | Rotação de papéis |
|---|---|---|
| 1 | qui 29/10 | Sim |
| 2 | qui 26/11 | Sim |
| 3 | ter 22/12 | Sim |
| 4 | qua 18/02 | Encerramento da disciplina |

## 3. Entregas e marcos da Sprint 0

| Data | Entrega | Onde |
|---|---|---|
| qui 08/10 | Links do repositório e do GitHub Projects (um envio por equipe) | Google Classroom |
| sex 09/10 | Proposta de 1 página (um envio por equipe) | Google Classroom |
| seg 12/10 | Parecer da professora: aprovado, aprovado com ajustes ou não aprovado | Retorno da professora |
| qui 15/10 | Review + Retrospectiva internas da Sprint 0 | Ata em `docs/gestao/atas/` |

## 4. Pontos de atenção do calendário

- **Sprint 5 é curta** (3 aulas, 8 dias corridos): o Planning já considera capacidade menor e o
  escopo da sprint deve ser menor.
- **O recesso de 6 semanas** vem logo depois do fim da Release 3. Ele é tratado como risco
  (RSK-04 no [registro de riscos](registro-de-riscos.md)): a Release 3 termina com tudo integrado,
  documentado e com o Backlog da Release 4 pronto.
- **Release 4 tem uma sprint longa** (02/02 a 18/02). O SM divide a sprint em marcos internos para que o
  Demo Day não dependa dos últimos dias.
- **Divergência a confirmar com a professora:** as descrições dos papéis no Classroom citam a Release 4
  como Sprints 6 e 7, mas a programação oficial traz apenas a Sprint 6 na Release 4. Este calendário
  segue a **programação oficial**.

## 5. Capacidade por sprint

Capacidade é calculada no Planning a partir da disponibilidade real de cada integrante. A estimativa
**inicial** (a recalibrar com o velocity real depois da Sprint 1) está em
[`priorizacao.md`](../produto/priorizacao.md).
