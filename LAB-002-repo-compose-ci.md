# LAB-002 — Repo ledger-lab + compose + CI mínima

**Labels:** `area:infra` `fase:fundacao`
**Épico:** Fundação

## Estudo

- `docker compose` para dependências locais (Postgres + RabbitMQ).
- GitHub Actions: pipeline mínimo (restore/build/test) a cada push.

## Fazer

1. Criar o repo `ledger-lab` (monorepo) com estrutura inicial:
   - `services/ledger-core/` (API .NET — recebe lançamentos via HTTP, publica eventos)
   - `services/ledger-worker/` (placeholder — ver abaixo o que ele será)
   - `devops/compose.yaml` (postgres:16 + rabbitmq:3-management)
   - `devops/docker/` (Dockerfiles futuros), `devops/k8s/` (manifestos futuros)
   - `.github/workflows/` (o Actions exige esse caminho; os workflows chamam scripts de `devops/` quando crescerem)
   - `docs/` (roteiro de estudo e decisões)
2. Subir `docker compose up -d` e validar: Postgres acessível, painel do RabbitMQ (`http://localhost:15672`).
3. Criar workflow `.github/workflows/ci.yml`: build + `dotnet test` (mesmo que só com 1 teste placeholder).

## Critério de pronto

- [ ] `docker compose up -d` sobe Postgres e RabbitMQ saudáveis.
- [ ] Push dispara o Actions com build verde.
- [ ] README com como subir o lab em 3 comandos.

## Falha provocada

- Derrubar o container do Postgres (`docker stop`) com a API ligada: registrar o comportamento observado (qual exceção, onde estoura). Sem corrigir ainda — só observar e anotar.

## O que será o ledger-worker

Um **.NET Worker Service** (`BackgroundService`) — processo sem UI que roda em loop contínuo. Evolução prevista, uma responsabilidade por vez:

1. **Liquidante:** consome a fila `lancamento.criado` (AMQP) e marca o lançamento como `Liquidado` com ack manual — aqui se estuda redelivery, DLQ e backpressure.
2. **Outbox relay:** varre a tabela outbox e publica no broker (ponte entre "persistiu" e "publicou" — fecha a janela de falha da HTTP-002).
3. **Conciliador agendado:** job diário que confere razão vs. eventos e emite relatório de divergências.

Por isso ele nasce como placeholder: na Fase 0 só precisa existir como projeto compilável; ganha vida na Fase 3 (AMQP).

## Papel da IA

- Revisora: criticar o compose (volumes? healthcheck? versões pinadas?) e o workflow (cache? trigger correto?).
