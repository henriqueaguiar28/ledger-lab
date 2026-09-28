# LAB-003 — Kanban, épicos-filhos e modelo de issue

**Labels:** `area:processo` `fase:fundacao`
**Épico:** Fundação

## Estudo

- GitHub Projects: campos, filtros por label e automação de colunas.

## Fazer

1. Criar o Project "Ledger — Épico Infinito" com as colunas:
   - `Backlog` → `Pronto p/ fazer` → `Fazendo` → `Revisão IA` → `Quebrado de propósito` → `Concluído`.
2. Criar os épicos-filhos como issues-mãe (checklist de issues filhas):
   - Fundação, Núcleo contábil, Mensageria, Conciliação, Escala k8s, Operação/VPS.
3. Fixar o modelo de issue no repo (`docs/modelo-issue.md`): Estudo / Fazer / Critério de pronto / Falha provocada / Papel da IA.
4. Importar as issues `LAB-*`, `LED-*`, `NET-*` e `HTTP-*` desta leva para o `Backlog`.

## Critério de pronto

- [ ] Board criado com as 6 colunas e automação (ex: PR vinculado move para Revisão).
- [ ] 6 épicos-filhos criados com descrição de 3–5 linhas cada.
- [ ] Todas as issues desta leva estão no `Backlog` com labels aplicadas.

## Falha provocada

- N/A (processo). Revisar em 30 dias se as colunas estão sendo usadas ou viraram burocracia — ajustar sem cerimônia.

## Papel da IA

- Examinadora: propor 2 melhorias no fluxo após ver o board pronto.
