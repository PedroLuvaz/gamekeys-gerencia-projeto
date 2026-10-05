# Plano de qualidade

Responsável: **QA** da release. Define **o que é qualidade neste projeto, como é medida e como é
garantida**. Versão inicial da Sprint 0; metas serão recalibradas com os dados reais da Sprint 1.

---

## 1. Objetivo

Garantir que cada incremento entregue atenda aos critérios de aceite das histórias, respeite as
[regras de negócio](../produto/regras-de-negocio.md) e a [Definition of Done](../produto/definition-of-done.md),
com evidência rastreável no GitHub.

## 2. Itens de qualidade

| # | Item | Por que importa | Como é garantido |
|---|---|---|---|
| Q1 | **Corretude funcional** | O cliente só percebe valor se o comportamento prometido acontece | Casos de teste derivados de cada critério de aceite, executados antes do PR ser aprovado |
| Q2 | **Regras de negócio protegidas** | Chave duplicada e preço alterado são os defeitos mais caros do produto | Cada RN tem teste automatizado que a prova; RN-02 tem teste de concorrência |
| Q3 | **Testes automatizados** | Evitam regressão e documentam o comportamento | Critério comportamental tem teste de API; regra com mais de uma ramificação tem teste de serviço |
| Q4 | **Revisão de código** | Um segundo par de olhos pega o que o autor não vê | Todo PR é revisado por outro integrante, em até 24 h |
| Q5 | **Integração contínua** | Falha detectada no push custa menos do que no dia da Review | Pipeline com lint e testes a cada push; `main` sempre verde |
| Q6 | **Rastreabilidade** | Mostra que o que foi pedido é o que foi testado e entregue | Issue ↔ commit ↔ PR ↔ caso de teste, ligados por número |
| Q7 | **Definition of Done cumprida** | Evita "pronto" subjetivo | Checklist no PR, validado pelo QA ao aprovar |
| Q8 | **Defeitos sob controle** | Bug sem registro vira surpresa na demonstração | Todo bug é uma issue com passos, evidência, severidade e status |

## 3. Métricas

Metas **iniciais**: sem histórico, são hipóteses a recalibrar na retrospectiva da Sprint 1.

| ID | Métrica | Fórmula | Fonte | Meta inicial | Item |
|---|---|---|---|---|---|
| **M1** | Conformidade com o DoD | Itens concluídos com checklist de DoD completo ÷ itens concluídos | Checklist dos PRs mesclados | 100% | Q7 |
| **M2** | Cobertura de critérios de aceite | Critérios de aceite com ao menos 1 caso de teste ÷ critérios de aceite da sprint | [Plano de testes](plano-de-testes-sprint-1.md) | 100% até o Planning | Q1, Q6 |
| **M3** | Taxa de aprovação dos casos de teste | Casos aprovados ÷ casos executados | Registro de execução do plano de testes | ≥ 90% na 1ª rodada; 100% na regressão final | Q1 |
| **M4** | Bugs abertos por severidade | Contagem de issues `bug` abertas, por severidade | Issues com label `bug` | 0 críticos e 0 altos abertos na Review | Q8 |
| **M5** | Bugs encontrados × corrigidos | Corrigidos na sprint ÷ encontrados na sprint | Issues `bug` por sprint | ≥ 80% | Q8 |
| **M6** | Escape de defeitos | Bugs achados depois do item em Concluído ÷ total de bugs da sprint | Issues `bug` ligadas a itens já concluídos | Tendência decrescente | Q1, Q7 |
| **M7** | Taxa de sucesso do pipeline | Execuções com sucesso ÷ execuções totais | Aba Actions (`gh run list`) | ≥ 80% geral; 100% na `main` | Q5 |
| **M8** | Tempo para corrigir build quebrado | Da execução vermelha até a próxima verde | Aba Actions | ≤ 1 dia útil | Q5 |
| **M9** | Tempo até a primeira revisão de PR | Da abertura do PR até a primeira revisão | Histórico dos PRs | ≤ 24 h | Q4 |

**Como coletar** (todos a partir do GitHub, sem planilha paralela):

```bash
gh issue list --label bug --state all --json number,title,state,createdAt,closedAt
gh run list --workflow ci.yml --limit 100 --json conclusion,createdAt,headBranch
gh pr list --state merged --json number,title,createdAt,mergedAt,reviews
git shortlog -sn --all
```

Os números entram no **relatório de qualidade da release** e na ata da retrospectiva. Tendência
importa mais do que o valor absoluto.

## 4. Severidade e prazo de correção

| Severidade | Definição | Exemplo | Prazo alvo |
|---|---|---|---|
| **Crítica** | Bloqueia o fluxo principal, perde dado ou viola uma regra de negócio central | Duas contas com o mesmo e-mail; chave vendida duas vezes | Mesmo dia. Bloqueia o merge e a Review |
| **Alta** | Funcionalidade importante não funciona e o contorno é difícil | Login falha para senha com acento | Na sprint corrente |
| **Média** | Funcionalidade com defeito, mas há contorno | Filtro não mantém a página ao voltar | Na sprint corrente ou na próxima |
| **Baixa** | Cosmético ou de baixo impacto | Texto cortado em tela pequena | Vai ao Backlog; PO decide |

**Ciclo de vida do bug** no quadro: `Backlog` → `Em andamento` (correção) → `Em revisão` (PR da correção)
→ `Concluído` (QA reteste e fechou). O QA **reexecuta o caso de teste** que falhou antes de aprovar a
correção, e referencia o bug no registro de execução.

**Registro:** issue com o [modelo de bug](../../.github/ISSUE_TEMPLATE/bug.yml), ligada à história
de origem. Uma issue que não é defeito é fechada com comentário explicando o motivo.

## 5. Estratégia de testes

| Nível | O que cobre | Ferramenta | Quando |
|---|---|---|---|
| **Serviço** | Regra de negócio com mais de uma ramificação | pytest | Junto da história |
| **API** | Critério de aceite comportamental, pela rota real | pytest + httpx | Junto da história |
| **Concorrência** | RN-02: duas compras simultâneas do último exemplar | pytest com threads | História #20 |
| **Manual / exploratório** | Telas e fluxos do front-end; usabilidade e mensagens | Roteiro nos casos de teste | Antes de aprovar o PR |
| **Regressão** | Fluxos já entregues continuam funcionando | Suíte automatizada + roteiro manual acumulado | Antes de cada Review e de cada release |

Princípios:

- **Sem mock de banco** nos testes de comportamento: o comportamento transacional é o que se testa. Cada
  teste usa um banco isolado.
- **Sem meta de cobertura percentual.** Teste escrito para inflar número é desperdício; o critério é
  "todo critério de aceite tem teste".
- Dados de teste são **fictícios**; nenhuma chave de ativação real entra no projeto.
- Teste que falha de forma intermitente é tratado como bug do teste e corrigido, não repetido até passar.

**Critério de entrada para testar um item:** PR aberto, CI verde e critérios de aceite claros na issue.
**Critério de saída (item):** todos os casos de teste do item aprovados e DoD validado.
**Critério de saída (sprint):** nenhum bug crítico ou alto aberto; regressão executada; relatório publicado.

## 6. Ciclo de regressão

| Quando | Escopo | Registro |
|---|---|---|
| **Antes de cada Review** | Suíte automatizada completa + roteiro manual dos fluxos entregues até a sprint | Seção "Registro de execução" do plano de testes da sprint |
| **Antes do Demo Day** | Regressão final completa, em ambiente limpo, a partir do seed | Relatório final de qualidade |

## 7. Rotina do QA em cada sprint

| Momento | Atividade |
|---|---|
| **Planning** | Revisa os critérios de aceite e o DoR dos itens; confirma que cada critério é testável |
| **Início da sprint** | Publica o plano de testes e os casos de teste da sprint; atualiza M2 |
| **Durante** | Executa os casos conforme os PRs chegam; registra bugs; aprova ou devolve PRs |
| **Antes da Review** | Roda a regressão e fecha o relatório de qualidade da sprint |
| **Review** | Informa o resultado de qualidade; valida o DoD dos itens apresentados |
| **Retrospectiva** | Apresenta M1 a M9 e propõe ações de melhoria |

## 8. Relatório de qualidade da release

Publicado pelo QA no fim de cada release, em `docs/qualidade/relatorios/release-N.md`. Conteúdo:

1. Resumo do resultado e recomendação (a release está apta?)
2. Métricas M1 a M9, **comparadas com a release anterior**
3. Bugs encontrados × corrigidos, por severidade
4. Análise de tendência e causa dos escapes
5. Resultado da regressão
6. Ações de melhoria para a próxima release

## 9. Riscos de qualidade

Os riscos que afetam qualidade (RSK-01, RSK-06, RSK-09, RSK-10) estão no
[registro de riscos](../gestao/registro-de-riscos.md).
