# HTTP-001 — Minimal API de lançamentos: socket cru vs. HttpClient

**Labels:** `area:redes` `area:backend` `fase:http`
**Épico:** Núcleo contábil (trilha de protocolos)
**Livro:** Kurose & Ross — capítulo de aplicação (HTTP, conexões persistentes).

## Estudo

- Request/response, métodos, status codes, headers essenciais (`Content-Type`, `Content-Length`, `Idempotency-Key`), keep-alive.

## Fazer

1. Criar `POST /lancamentos` e `GET /lancamentos/{id}` na `ledger-core` usando o caso de uso da LED-002.
2. Consumir o POST de dois jeitos e comparar:
   - a) Via socket TCP cru (montar o HTTP na mão: request line, headers, body).
   - b) Via `HttpClient`.
3. Capturar ambos no Wireshark e anexar: mostrar keep-alive na segunda chamada com `HttpClient`.

## Critério de pronto

- [ ] Ambos os clientes criam o lançamento (201) e o GET retorna (200).
- [ ] Evidência de conexão reutilizada (keep-alive) no caso (b).
- [ ] Nota em `docs/fichas/http.md`: o que o `HttpClient` faz por você (pool de conexões, headers, chunked...).

## Falha provocada

- Enviar `Content-Length` errado no cliente cru: observar como o servidor reage (400? timeout?) e anotar.

## Papel da IA

- Revisora: status codes corretos? (201 vs. 200, 409 vs. 400 na duplicata, ProblemDetails?)
- Examinadora: "quando retornar 200 + corpo existente vs. 409 no reenvio da mesma chave?"
