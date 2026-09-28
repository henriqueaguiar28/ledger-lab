# NET-002 — Socket cru: transmitir um lançamento com framing

**Labels:** `area:redes` `area:backend` `fase:tcp`
**Épico:** Núcleo contábil (trilha de protocolos)

## Estudo

- Framing em streams: length-prefix (4 bytes big-endian + payload) como solução para "onde termina uma mensagem?".

## Fazer

1. Criar projeto `labs/tcp-lab/` (fora dos serviços oficiais): servidor + cliente em socket TCP cru.
2. O cliente serializa um `Lancamento` em JSON, prefixa com o tamanho (length-prefix) e envia; o servidor lê exatamente N bytes e desserializa.
3. Primeiro **sem** framing (enviar 2 lançamentos colados) para ver o bug acontecer; depois **com** framing.

## Critério de pronto

- [ ] Sem framing: demonstrado o bug (mensagens coladas/fragmentadas) com log como evidência.
- [ ] Com framing: 100 lançamentos enviados em rajada, 100 recebidos íntegros e na ordem.
- [ ] Código marcado como `labs/` (descartável, fora do caminho do produto).

## Falha provocada

- Enviar payload com tamanho declarado errado (maior e menor que o real): o servidor deve detectar e descartar sem travar — registrar o comportamento.

## Papel da IA

- Revisora: procurar leitura parcial (`Receive` que assume N bytes de uma vez), endianness, falta de timeout.
- Examinadora: "por que a biblioteca AMQP/HTTP esconde isso de você? o que ela faz por baixo?"
