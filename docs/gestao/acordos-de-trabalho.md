# Acordos de trabalho do time

Regras que o time combina para trabalhar junto. Se uma regra deixa de funcionar, ela é alterada na
**retrospectiva**, por PR, e não ignorada em silêncio.

**Status:** proposta do Scrum Master, a ser aceita pelo time no PR que a incorpora à `main`.

| Aceite | Integrante | Papel (Release 1) | Data |
|---|---|---|---|
| [ ] | Pedro Lucas Vaz de Andrade | Product Owner | |
| [ ] | Wagner Tiburcio da Silva Junior | QA | |
| [ ] | Rodrigo Almeida Gomes | Scrum Master | |

---

## 1. Comunicação

- **Canal oficial do time:** grupo de mensagens da equipe _(registrar aqui qual: WhatsApp, Discord etc.)_.
  Decisão que afeta o projeto e foi tomada em conversa de canto vira comentário na issue ou ata.
- **Daily assíncrona:** segunda, quarta e sexta, até as 18h, em uma mensagem com três linhas:
  _Feito desde a última daily · Vou fazer · Impedimentos_.
- **Resposta a pergunta direta ao time:** em até 24 h, em dia útil.
- **Dúvida de requisito:** vai ao PO por comentário na issue da história, para ficar registrada.
- **Dúvida sobre a disciplina:** o PO leva à professora, nas aulas ou por e-mail.

## 2. Cerimônias

- Acontecem nas aulas, conforme o [calendário](calendario-de-cerimonias.md). Presença é esperada;
  quem não puder avisa o SM com antecedência e deixa por escrito sua posição sobre os pontos da pauta.
- O **SM** conduz, respeita o tempo de cada cerimônia e **escreve a ata** no mesmo dia.
- A ata é publicada em [`atas/`](atas) por pull request.
- Retrospectiva termina com **no máximo 3 ações**, cada uma com responsável e prazo.

## 3. Trabalho e quadro

- Todo trabalho tem uma **issue** e aparece no quadro. Sem issue, sem trabalho reconhecido.
- Cada integrante tem **no máximo 1 item em Em andamento**. Terminou ou travou, atualiza.
- O quadro é atualizado **no momento da mudança**.
- Item novo no meio da sprint **não entra**: vai para o Backlog com prioridade Baixa e é avaliado no
  próximo Planning. Exceção: bug crítico, decidido pelo PO com o QA.
- Estimativa por **Planning Poker**, com escala 1, 2, 3, 5. Item que o time estima em 8 ou mais é quebrado.

## 4. Código, branches e pull requests

- Seguem o [CONTRIBUTING](../../CONTRIBUTING.md): branch curta, commit padronizado, PR com `Closes #n`.
- Ninguém faz commit direto na `main`.
- **Todo PR é revisado por outro integrante** em até 24 h. O QA da release aprova.
- Build quebrado tem prioridade sobre qualquer item novo. Quem quebrou corrige ou pede ajuda no mesmo dia.
- Documento de um papel é escrito e commitado por **quem exerce o papel** (ou em par, com
  `Co-authored-by`). Assim o histórico mostra quem fez cada coisa.

## 5. Qualidade

- O que é "pronto" está na [Definition of Done](../produto/definition-of-done.md). Ninguém a flexibiliza
  sozinho.
- O QA tem a palavra final sobre aprovar ou não um PR do ponto de vista dos critérios de aceite.
- Todo bug é registrado como issue `bug`, mesmo que seja corrigido em 5 minutos.

## 6. Decisões

- **Produto** (o que construir e em que ordem): o PO decide, ouvindo o time. Em empate, vale a decisão do PO.
- **Processo** (como trabalhamos): o SM facilita e o time decide por consenso. Sem consenso, vota-se, e a
  maioria decide.
- **Técnica** (como construir): quem executa propõe e o time revisa no PR. Decisão relevante vira nota
  no PR ou na issue.
- **Dependência nova** no projeto exige aprovação do PO e registro da decisão.

## 7. Impedimentos e escalada

| Prazo sem solução | O que acontece |
|---|---|
| Imediato | Quem está bloqueado avisa o grupo e marca o SM |
| 24 h | Vira issue com o texto "Impedimento:" no título, fica visível no quadro e entra na pauta da próxima daily |
| 72 h | O SM leva o assunto à professora, com o histórico do quadro e do Git como registro |

O SM mantém o registro de impedimentos com **status** e **data de resolução** nas atas.

## 8. Disponibilidade

- Quem sabe que ficará indisponível (prova, viagem, trabalho) avisa no **Planning**, para entrar no
  cálculo de capacidade.
- Ausência não avisada por mais de 2 semanas é comunicada à professora, com os dados do quadro e do Git
  como fato registrado, e não como acusação.

## 9. Rodízio de papéis

- Os papéis giram ao **fim de cada release**, na Review + Retrospectiva marcada no calendário.
- Na passagem, o papel que sai entrega ao próximo: estado do backlog e do quadro (PO), registro de riscos
  e ações pendentes da retrospectiva (SM), bugs abertos e plano de testes (QA), estado do pipeline (DevOps).
- A atribuição da release seguinte é registrada no [README](../../README.md) e na ata da retrospectiva.

## 10. Revisão dos acordos

Os acordos são revistos em toda retrospectiva de release. Alteração entra por PR, com o aceite dos três.
