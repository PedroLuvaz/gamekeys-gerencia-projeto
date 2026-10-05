# Registro de riscos

Versão inicial: **05/10/2026** (Sprint 0). Responsável: **Scrum Master**. Revisado em **toda
retrospectiva**: reavaliar exposição, encerrar o que não se aplica mais, abrir o que apareceu.

## Como ler

- **P** (probabilidade) e **I** (impacto) em escala de 1 a 5. **Exposição = P × I**.
- Exposição **maior ou igual a 12** exige **resposta ativa**, dono definido e acompanhamento semanal
  pelo SM. Entre 6 e 11, monitorar. Abaixo de 6, aceitar.
- Estratégias: **Evitar** (eliminar a causa), **Mitigar** (reduzir P ou I), **Transferir**, **Aceitar**.
- Novo risco entra por pull request neste arquivo e, se precisar de acompanhamento próprio, também como
  issue com o label `risco`.

## Resumo

| ID | Risco | Categoria | P | I | Exp. | Estratégia | Dono | Status |
|---|---|---|---|---|---|---|---|---|
| **RSK-01** | Mesma chave vendida para dois compradores por concorrência | Técnico | 4 | 5 | **20** | Mitigar | Quem assumir a história #20 | Aberto |
| **RSK-03** | Escopo inflado por ideia nova no meio da sprint | Gestão | 4 | 4 | **16** | Evitar | PO | Aberto |
| **RSK-04** | Recesso de 6 semanas quebra o ritmo e comprime a Release 4 | Cronograma | 4 | 4 | **16** | Mitigar | SM | Aberto |
| **RSK-02** | Indisponibilidade de integrantes em semana de prova | Acadêmico | 5 | 3 | **15** | Mitigar | SM | Aberto |
| **RSK-05** | Evidência de papéis e de commits concentrada em um só integrante | Acadêmico | 3 | 5 | **15** | Mitigar | SM | Aberto |
| **RSK-06** | Preço não congelado corrompe faturamento e pedidos antigos | Técnico | 3 | 4 | **12** | Mitigar | Quem assumir a história #19 | Aberto |
| **RSK-07** | "Pagamento simulado" interpretado como entrega incompleta | Comunicação | 3 | 4 | **12** | Mitigar | PO | Aberto |
| **RSK-10** | Estimativas otimistas, sem histórico de velocity | Gestão | 4 | 3 | **12** | Mitigar | PO e SM | Aberto |
| **RSK-12** | Ambiente de desenvolvimento não sobe na máquina de algum integrante | Técnico | 3 | 4 | **12** | Mitigar | DevOps | Aberto |
| **RSK-11** | Demonstração falha no Demo Day | Comunicação | 2 | 5 | 10 | Mitigar | Equipe | Monitorar |
| **RSK-08** | Ferramentas novas (GitHub Projects, Actions, FastAPI) consomem a Sprint 1 | Técnico | 3 | 3 | 9 | Mitigar | DevOps | Monitorar |
| **RSK-09** | Build quebrado bloqueia o time | Técnico | 3 | 3 | 9 | Mitigar | DevOps | Monitorar |

## Respostas planejadas

### RSK-01 — Venda duplicada de chave · exposição 20
- **Resposta:** unicidade do código da chave no banco e reserva das chaves dentro da transação do
  checkout, com bloqueio de linha. Teste de concorrência obrigatório: duas compras simultâneas do
  último exemplar, e exatamente uma deve ter sucesso (história #20).
- **Gatilho:** item travado por mais de 4 horas. O desenvolvedor avisa o SM no mesmo dia.
- **Acompanhamento:** é a história de maior risco técnico; entra na Sprint 3 com tempo de folga.

### RSK-03 — Escopo inflado · exposição 16
- **Resposta:** o Sprint Goal não muda no meio da sprint. "E se a gente também colocasse…" vira issue
  com prioridade Baixa e só é avaliada no próximo Planning.
- **Gatilho:** item sem issue ou fora do Sprint Goal aparecendo em Em andamento.

### RSK-04 — Recesso entre a Release 3 e a Release 4 · exposição 16
- **Resposta:** a Release 3 termina com a `main` estável, a documentação em dia e uma tag. Antes do
  recesso, o PO deixa o Backlog da Release 4 refinado e o SM registra na ata o "estado de retomada"
  (o que está pronto, o que falta, quem faz o quê). Combinar um contato curto no fim de janeiro.
- **Gatilho:** Backlog da Release 4 sem itens prontos para o Planning de 22/12.

### RSK-02 — Semana de prova · exposição 15
- **Resposta:** a capacidade inicial é conservadora. Quem sabe que terá semana pesada avisa no Planning.
  Itens de prioridade Média são cortados primeiro e o corte é registrado na Review.
- **Gatilho:** velocity abaixo de 70% do planejado por duas sprints.

### RSK-05 — Evidência concentrada em um integrante · exposição 15
- **Resposta:** cada artefato de papel é escrito e commitado por quem exerce o papel. Distribuição
  verificada na retrospectiva com `git shortlog -sn --all` e pelas issues e PRs por pessoa. A rotação de
  papéis ao fim de cada release é cumprida de fato.
- **Gatilho:** mais de 60% dos commits de uma sprint de um único integrante.

### RSK-06 — Preço não congelado · exposição 12
- **Resposta:** regra RN-03 implementada no checkout, com teste que altera o preço do jogo depois do
  pedido e confirma que o total não muda (história #19).

### RSK-07 — Pagamento simulado visto como entrega incompleta · exposição 12
- **Resposta:** o escopo declara pagamento simulado como decisão, não como falha. A interface sinaliza
  que o pagamento é simulado, e o PO declara isso na apresentação.

### RSK-10 — Estimativas otimistas · exposição 12
- **Resposta:** capacidade inicial conservadora; item estimado acima de 5 pontos é quebrado; velocity
  real da Sprint 1 recalibra o plano das sprints seguintes.
- **Gatilho:** sprint concluída com menos de 70% dos pontos comprometidos.

### RSK-12 — Ambiente não sobe em alguma máquina · exposição 12
- **Resposta:** cada integrante executa o [guia de ambiente](../devops/ambiente-de-desenvolvimento.md)
  até **13/10** e abre uma issue com o problema, se houver. Quem não conseguir faz par com o DevOps.
- **Gatilho:** integrante sem ambiente funcionando no Planning da Sprint 1 (20/10). Passa a ser a
  primeira prioridade do time.

### RSK-11, RSK-08 e RSK-09 — monitorados
- **RSK-11:** roteiro de demonstração ensaiado antes do Demo Day, dados de demonstração determinísticos
  e ambiente local como plano B se o deploy falhar.
- **RSK-08:** stack congelada; ferramenta nova só entra como investigação de até 4 horas, com decisão
  registrada.
- **RSK-09:** check do CI exigido nos PRs; build quebrado é a prioridade do time.

## Histórico de revisões

| Data | Revisão | Mudanças |
|---|---|---|
| 05/10/2026 | Criação (Sprint 0) | Registro inicial com 12 riscos |
