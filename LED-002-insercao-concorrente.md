# LED-002 — Inserção concorrente sem duplicar nem corromper

**Labels:** `area:backend` `area:db` `fase:nucleo-contabil`
**Épico:** Núcleo contábil

## Estudo

- Condição de corrida: dois fluxos lendo/escrevendo o mesmo dado.
- UNIQUE como barreira de correção vs. lock pessimista; custo de cada abordagem.

## Fazer

1. Criar método `RegistrarLancamentoAsync` (caso de uso) que trata violação de UNIQUE retornando o lançamento existente (sem estourar 500).
2. Escrever teste de concorrência: 50 tasks registrando a **mesma** chave de idempotência em paralelo.
3. Medir: quantos registros criados? quantas exceções? tempo total?

## Critério de pronto

- [ ] 50 inserções paralelas com a mesma chave → exatamente 1 registro no banco.
- [ ] Chamadas repetidas retornam o existente (comportamento idempotente observável).
- [ ] Sem deadlock nem conexão esgotada (logs limpos).

## Falha provocada

- Rodar o mesmo teste com 200 tasks e pool de conexões reduzido (`Max Pool Size=5`): observar fila/timeout e anotar o limite encontrado.

## Papel da IA

- Revisora: procurar TOCTOU (check-then-insert), exceção engolida, `DbContext` compartilhado entre threads.
- Examinadora: "qual a complexidade do retry aqui? e se a chave colidir por coincidência (não reenvio)?"
