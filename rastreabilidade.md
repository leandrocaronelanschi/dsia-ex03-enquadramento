# Rastreabilidade dos requisitos

Cada requisito do Lavra, de onde ele vem e por que ele existe. A coluna
**Origem** diz se o requisito nasce do problema de campo (ciclo de relevância)
ou da base de conhecimento (ciclo de rigor), como pede o template DSR.

| ID | Requisito | Origem | Fonte específica | Justificativa | Como se verifica |
|----|-----------|--------|------------------|---------------|------------------|
| R1 | Localizar o módulo e o arquivo afetados antes de propor qualquer edição | Literatura (rigor) | Estudos de agentes de reparo de programas, entre eles o AutoCodeRover, que mostram o papel da localização no acerto | Editar sem localizar aumenta a chance de alterar o trecho errado num repositório sem documentação de arquitetura | Log da execução registra o arquivo escolhido antes do primeiro diff; execuções sem etapa de localização são rejeitadas na auditoria |
| R2 | Não fechar issue sem aprovação humana explícita | Problema (relevância) | Causa 3: o conhecimento do Colheita está concentrado em uma pessoa e não está escrito | Sem alguém que conheça a regra de negócio conferindo, uma correção plausível pode violar uma regra não documentada — foi o que ocorreu no cálculo de pagamento | Nenhuma issue muda de estado sem registro de aprovação de um membro da equipe |
| R3 | Registrar o rastro de cada execução: issue, prompt, arquivos tocados, testes executados e resultado | Problema (relevância) | Causa 3; e a exigência de reprodutibilidade da própria disciplina | Sem rastro, nenhuma correção feita pelo agente pode ser auditada nem reexecutada depois, e a avaliação da pesquisa perde o dado bruto | Cada execução produz um registro completo; a ausência de qualquer campo invalida a execução para a análise |
| R4 | Executar a suíte existente antes e depois da edição e reportar a diferença | Problema (relevância) | Causa 2: a suíte do Colheita é esparsa | Sem o par antes/depois não se distingue teste que já falhava de regressão introduzida pela edição | Comparação dos dois relatórios de execução anexada ao rastro (R3) |
| R5 | Escalar para o humano a issue cujo módulo afetado não puder ser identificado com confiança | Literatura + evidência própria (rigor + design) | Mesma literatura de R1, e o achado da Learning Iteration de que o agente erra mais quando a issue não aponta o módulo afetado | Converte uma falha previsível em devolução explícita, em vez de uma correção errada entregue com confiança | Taxa de escalonamento medida por estrato de issue; nenhum fechamento automático em issues sem módulo identificado |
| R6 | Operar sobre o repositório como ele é, sem exigir reescrita ou reestruturação prévia do legado | Problema (relevância) | Causa 1 e o contexto: uma TI de duas pessoas não tem folga para refatorar antes de corrigir | Um artefato que exige preparação do legado não resolve o problema de campo: ele o adia | O agente roda sobre o `colheita-mini` sem nenhuma alteração estrutural prévia |

## Leitura cruzada

- **Ciclo de relevância** (origem no problema): R2, R3, R4, R6.
- **Ciclo de rigor** (origem na literatura): R1, R5.
- **Ciclo de design** (origem na própria construção e nos estudos): R5 tem
  componente de design, porque o limiar de confiança que dispara o
  escalonamento é decidido com a evidência das Learning Iterations.

Nenhum requisito desta tabela tem origem apenas em preferência de
implementação. Requisito sem origem vira pergunta na defesa.
