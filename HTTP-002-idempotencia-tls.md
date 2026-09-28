# HTTP-002 — Idempotência fim a fim + TLS local observado

**Labels:** `area:redes` `area:backend` `fase:http`
**Épico:** Núcleo contábil (trilha de protocolos)
**Livro:** Kurose & Ross — capítulo de segurança (TLS/handshake).

## Estudo

- Header `Idempotency-Key` como contrato de API; handshake TLS (o que é negociado, onde ficam os certificados).

## Fazer

1. Aceitar `Idempotency-Key` no `POST /lancamentos` e mapear para `ChaveIdempotencia` (reenvio → 200 + recurso existente).
2. Habilitar HTTPS local (cert dev) e capturar o handshake TLS no Wireshark (filtro `tls.handshake`): identificar ClientHello/ServerHello e o ponto onde o tráfego vira indecifrável.
3. Escrever a ficha `docs/fichas/tls.md` (garantias / falhas típicas / quando observar).

## Critério de pronto

- [ ] Reenvio com a mesma chave → 200 + mesmo `Id`, sem nova linha no banco.
- [ ] Chave diferente + mesmo conteúdo → novo lançamento (conteúdo igual não é duplicata; chave igual é).
- [ ] Captura TLS anexada com os pacotes de handshake identificados.

## Falha provocada

- Simular timeout do cliente após o servidor persistir (cancelar o `HttpClient` com delay): reenviar e provar que não duplicou. Este é o cenário que mais quebra sistemas reais.

## Papel da IA

- Revisora: a janela entre "persistiu" e "respondeu" está coberta? E se o crash for exatamente ali? (ponte para outbox na Fase AMQP.)
