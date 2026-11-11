# dsia-ex03-enquadramento

Exercício 3 da disciplina **Desenvolvimento de Software Suportado por IA**:
o enquadramento DSR em duas páginas que responde ao parecer da banca do
Problema 3 — que problema, que pergunta, que requisitos e como avaliar.

## Tema

**Não há pesquisa própria definida**, então, como permite o enunciado, o
enquadramento é do **caso-guia: o Lavra**, um agente de IA para a manutenção do
Colheita, o sistema legado da Cooperativa Vale do Cedro. Esta declaração está
aqui por exigência do enunciado ("Sem pesquisa definida, enquadre o Lavra e diga
isso no README.md").

## Artefato

Uma **instância de software**: um agente que opera sobre um repositório, com
busca de código, edição e execução de testes. Não é um método, não é um modelo
e não substitui a equipe de TI.

## Pergunta de pesquisa

Em que condições um agente de código resolve corretamente issues de um sistema
legado com poucos testes, e em que ponto a decisão precisa voltar para o humano?

## Onde está cada parte

| Parte do guia | Arquivo | Seção |
|---------------|---------|-------|
| Pergunta de pesquisa (problema de conhecimento) | `enquadramento.md` | Pergunta de pesquisa |
| 1. Problema de campo, com evidência | `enquadramento.md` | § 1 |
| 2. Causas | `enquadramento.md` | § 2 |
| 3. Requisitos do artefato | `enquadramento.md` § 3 | detalhado em `rastreabilidade.md` |
| 4. Tipo de artefato | `enquadramento.md` | § 4 |
| 5. Demonstração | `enquadramento.md` | § 5 |
| 6. Avaliação | `enquadramento.md` | § 6 |
| 7. Contribuição de conhecimento esperada | `enquadramento.md` | § 7 |
| Tabela de rastreabilidade | `rastreabilidade.md` | tabela completa |
| Declaração de uso de IA | `USO-DE-IA.md` | — |

## Conferência do checklist do enunciado

- [x] `enquadramento.md` tem as sete partes, com títulos, e **1.074 palavras**
      (a faixa pedida é de 700 a 1.100).
- [x] Cada um dos seis requisitos (R1–R6) tem origem declarada na tabela de
      rastreabilidade, com fonte específica e justificativa.
- [x] `USO-DE-IA.md` existe e está preenchido.
- [ ] Repositório público na branch `main` — **ainda não publicado**; ver abaixo.

## Estado da entrega

Estes arquivos foram produzidos como material de referência e **não foram
publicados no GitHub nem enviados na tarefa do Moodle**. Para publicar:

```bash
git init -b main && git add . && git commit -m "Enquadramento DSR do Lavra"
gh repo create dsia-ex03-enquadramento --public --source=. --push
```

## Nota sobre as referências

O texto cita as leituras do Módulo 04 pelo nome com que a disciplina as
apresenta (Hevner 2007 para os três ciclos; Johannesson e Perjons para os cinco
passos; Barcellos et al. 2022 para as Learning Iterations; vom Brocke, Hevner e
Maedche 2020 para o panorama) e menciona estudos de agentes de reparo, entre
eles o AutoCodeRover, como a origem do requisito de localização. **As citações
completas não foram montadas aqui**: antes de usar o texto na dissertação, elas
devem ser conferidas e formatadas a partir da página "Leituras do Módulo 04",
que traz os DOIs.
