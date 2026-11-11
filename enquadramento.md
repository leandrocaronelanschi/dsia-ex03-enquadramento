# Enquadramento DSR — Lavra: um agente de IA para a manutenção do Colheita

## Pergunta de pesquisa (problema de conhecimento)

**Em que condições um agente de código resolve corretamente issues de um
sistema legado com poucos testes, e em que ponto a decisão precisa voltar para
o humano?**

A pergunta é distinta do problema de campo: a cooperativa precisa de issues
fechadas; a pesquisa precisa saber *quando* a automação acerta e *quando* ela
deve parar. Uma resposta útil nomeia condições observáveis da issue e do
repositório, e não um veredito geral sobre agentes.

## 1. Problema de campo, com evidência

**Contexto.** A Cooperativa Vale do Cedro mantém o Colheita, um sistema legado
em Python que registra a pesagem da safra, calcula pagamentos e controla o
estoque. A TI são duas pessoas: Davi Rocha, que coordena, e Marina Teles, que
desenvolve.

**Necessidade.** As correções precisam entrar em produção no ritmo em que a
safra as gera, porque o sistema move dinheiro de produtores a cada pesagem.

**Dificuldade.** As issues chegam mais rápido do que duas pessoas conseguem
fechar: o Colheita acumula centenas de issues abertas.

**Problema.** O backlog de issues do Colheita não é absorvido pela equipe, e a
fila de correções cresce de forma persistente.

**Evidência.** O histórico de issues do repositório da cooperativa: volume
aberto, tempo médio até o fechamento e crescimento da fila ao longo das safras.
Há também evidência de custo direto do erro não detectado: uma função de
cálculo de pagamento entrou em produção descartando a fração do quilo, e um
produtor recebeu a menos no fechamento do mês.

**Possibilidade de intervenção.** Só aqui entra a tecnologia: parte do trabalho
de localizar, editar e verificar código pode ser delegada a um agente de
codificação, desde que a decisão de fechar a issue continue com a equipe.

## 2. Causas

A causa não é "falta de uma ferramenta de IA". São três, e cada uma gera
requisito:

1. **Localizar o código custa mais que corrigi-lo.** O Colheita não tem
   documentação de arquitetura, e descobrir que módulo uma issue afeta consome
   a maior parte do tempo de cada correção.
2. **A suíte de testes é esparsa.** Sem teste que cubra o trecho alterado, não
   há como saber se a correção quebrou outra regra — foi assim que o erro do
   cálculo de pagamento passou.
3. **O conhecimento do sistema está concentrado em uma pessoa.** O que Marina
   sabe sobre o Colheita não está escrito, então nenhuma correção feita por
   outra pessoa (ou por um agente) pode ser auditada depois.

## 3. Requisitos do artefato

| ID | Requisito | Origem |
|----|-----------|--------|
| R1 | Localizar o módulo e o arquivo afetados antes de propor qualquer edição | Literatura |
| R2 | Não fechar issue sem aprovação humana explícita | Problema (causa 3) |
| R3 | Registrar o rastro de cada execução: issue, prompt, arquivos tocados, testes executados e resultado | Problema (causa 3) |
| R4 | Executar a suíte existente antes e depois da edição e reportar a diferença | Problema (causa 2) |
| R5 | Escalar para o humano a issue cujo módulo afetado não puder ser identificado com confiança | Literatura + evidência própria |
| R6 | Operar sobre o repositório como ele é, sem exigir reescrita ou reestruturação prévia do legado | Problema (causa 1) |

A origem e a justificativa de cada requisito estão em `rastreabilidade.md`.
Nenhum requisito desta lista nasce de preferência de implementação: R1 e R5 vêm
do ciclo de rigor, os demais do ciclo de relevância.

## 4. Tipo de artefato

O Lavra é uma **instância de software**: um agente que opera sobre um
repositório, com busca de código, edição e execução de testes.

O que ele **não** é: não é um método de manutenção de legado, não é um modelo
de qualidade de código e não é um substituto da equipe de TI. O artefato
automatiza a execução; a decisão de aceitar a correção permanece humana por
requisito (R2), e não por limitação temporária da implementação.

## 5. Demonstração

A aplicação a um caso real usa o **backlog de issues do Colheita**, com recorte
reprodutível no repositório `colheita-mini`, que reúne código, testes e issues
abertas da cooperativa. A demonstração seleciona issues já fechadas pela equipe,
de modo que exista uma correção de referência para comparação, e issues abertas,
para observar o comportamento do agente sem gabarito disponível.

## 6. Avaliação

A avaliação responde à pergunta de pesquisa, e não à impressão de uso.

- **Medida principal:** proporção de issues **resolvidas corretamente**, em que
  "correta" é definida antes da execução por testes de aceitação escritos para
  cada issue, e não por inspeção posterior do código.
- **Medida de custo:** número de **intervenções humanas** por issue, contando
  tanto correção manual quanto nova instrução ao agente.
- **Comparação:** contra uma linha de base sem localização prévia (R1
  desativado) e contra o tempo da equipe nas issues equivalentes já fechadas.
- **Estratificação:** os resultados são separados por condição da issue —
  principalmente se ela identifica ou não o módulo afetado, e se o trecho
  alterado tem cobertura de testes. É essa estratificação que transforma um
  número agregado em condições, que é o que a pergunta pede.
- **Organização:** cada estudo é escrito como uma *Learning Iteration*
  (Barcellos et al., 2022), nascido de uma necessidade de conhecimento e
  encerrado numa seção "O que aprendemos?".

A pergunta que a banca fará — "essa avaliação sustenta essa conclusão?" — é
respondida pelo critério de acerto definido antes e pela comparação com a linha
de base. O desenho tem um limite declarado: ele mede desempenho em um único
sistema legado, e a generalização para outros repositórios é hipótese, não
resultado.

## 7. Contribuição de conhecimento esperada

Se o Lavra deixasse de existir amanhã, ficaria:

1. **As condições** em que um agente de código resolve corretamente issues de
   um sistema legado com poucos testes — e as condições em que ele falha de
   forma previsível, como a issue que não identifica o módulo afetado.
2. **O ponto de devolução ao humano**: que sinais, observáveis durante a
   execução, indicam que a decisão deve voltar à equipe.
3. **Princípios de design** testados e seus limites: localizar antes de editar,
   verificar com a suíte antes e depois, registrar o rastro e exigir aprovação
   para fechar.

Essa é a diferença entre a contribuição de projeto (o agente) e a contribuição
de conhecimento (o que outro pesquisador usa sem o agente).
