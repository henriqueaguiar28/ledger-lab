# NET-001 — TCP na teoria + handshake observado no Wireshark

**Labels:** `area:redes` `fase:tcp`
**Épico:** Núcleo contábil (trilha de protocolos)
**Livro:** Kurose & Ross — capítulo de transporte (seções TCP: handshake, transferência confiável, controle de fluxo/congestionamento).

## Estudo

- Stream vs. mensagem; handshake de 3 vias (SYN/SYN-ACK/ACK); portas; TCP vs. UDP; o que significam timeout e retransmissão.

## Fazer

1. Ler as seções indicadas e escrever a ficha do protocolo em `docs/fichas/tcp.md`:
   - Garantias / Falhas típicas / Quando usar / Quando NÃO usar.
2. No Wireshark, capturar `loopback` filtrando `tcp` enquanto roda qualquer tráfego local (ex: abrir o painel do RabbitMQ).
3. Identificar e printar: 1 handshake completo (SYN → SYN-ACK → ACK) e 1 encerramento (FIN).

## Critério de pronto

- [ ] Ficha `tcp.md` escrita com as 4 seções.
- [ ] Evidência do handshake capturado anexada à issue.
- [ ] Explicar com as próprias palavras por que "TCP garante ordem e entrega, mas não fronteira de mensagem".

## Falha provocada

- N/A nesta issue (observação pura). A quebra vem na NET-003.

## Papel da IA

- Tutora: explicar handshake e retransmissão antes da leitura.
- Examinadora: quiz de 3 perguntas após a ficha pronta.
