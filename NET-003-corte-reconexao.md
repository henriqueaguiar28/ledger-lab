# NET-003 — TCP: corte de conexão, meia-mensagem e reconexão

**Labels:** `area:redes` `fase:tcp`
**Épico:** Núcleo contábil (trilha de protocolos)

## Estudo

- Conexão semi-aberta, keep-alive, timeout de leitura; por que "mandei" ≠ "chegou" ≠ "foi processado".

## Fazer

1. No `labs/tcp-lab/`, adicionar timeout de leitura no servidor e lógica de reconexão com retry no cliente.
2. Cenários:
   - a) Cliente cai no meio do envio (fecha socket após metade dos bytes).
   - b) Servidor cai e volta; cliente reconecta e reenvia.
3. Registrar em `docs/fichas/tcp.md` (adendo): o que o TCP garante em cada cenário e o que a **aplicação** precisa garantir.

## Critério de pronto

- [ ] Cenário (a): servidor descarta a meia-mensagem sem corromper as seguintes.
- [ ] Cenário (b): após reconexão, nenhum lançamento se perde nem duplica no log do servidor.
- [ ] Adendo escrito na ficha: linha divisória entre garantia do TCP e responsabilidade da aplicação.

## Falha provocada

- Esta issue É a falha provocada. Bônus: simular rede lenta (enviar 1 byte por vez com delay) e observar o servidor montar a mensagem corretamente.

## Papel da IA

- Revisora: checar se o retry pode duplicar (spoiler: pode — e é a ponte para a chave de idempotência da LED-001/HTTP-002).
