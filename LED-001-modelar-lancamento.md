# LED-001 — Modelar e migrar Lancamento (double-entry + idempotência)

**Labels:** `area:backend` `fase:nucleo-contabil`
**Épico:** Núcleo contábil

## Estudo

- Partidas dobradas: todo lançamento tem conta débito + conta crédito + valor positivo; a soma do razão é sempre zero.
- Chave de idempotência: restrição UNIQUE que torna o reenvio seguro.

## Fazer

1. Criar entidade `Lancamento`: `Id`, `ContaDebito`, `ContaCredito`, `Valor` (decimal 18,2, > 0), `ChaveIdempotencia` (UNIQUE), `DataCriacao` (UTC), `Status` (Pendente/Liquidado).
2. Criar entidade `Conta`: `Codigo` (UNIQUE), `Nome`.
3. Gerar migração EF Core e aplicar no Postgres local.
4. Escrever nota de 5 linhas em `docs/decisoes/LED-001.md`: o que o modelo garante / o que pode falhar.

## Critério de pronto

- [ ] Migração aplica limpo num banco vazio (`migrate` + `migrate` reversa testada).
- [ ] Inserir 2 lançamentos espelhados e conferir soma zero via SQL.
- [ ] Inserir 2 lançamentos com a mesma chave → o segundo falha por UNIQUE (comportamento documentado).

## Falha provocada

- Tentar `Valor <= 0` e `ContaDebito = ContaCredito` direto no banco: o que deveria barrar e em que camada (banco vs. aplicação)? Anotar a decisão.

## Papel da IA

- Tutora (antes): explicar double-entry e por que UNIQUE é a base da idempotência.
- Revisora (depois): criticar tipos, constraints e o que falta (ex: índice por conta/data para extratos futuros).
- Examinadora: quiz — "o que acontece se dois POSTs com a mesma chave chegarem juntos?" (resposta vem na LED-002).
