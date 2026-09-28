# LAB-001 — Instalar e validar as ferramentas do lab

**Labels:** `area:infra` `fase:fundacao`
**Épico:** Fundação

## Estudo

- O que cada ferramenta faz no lab: Docker (runtime), Kubernetes embutido no Docker Desktop (k8s local sem cluster extra), k6 (carga HTTP), Wireshark (observar protocolos), Tailscale (acesso privado multi-dispositivo).

## Fazer

1. Instalar: Docker Desktop, k6, Wireshark, Tailscale.
2. Habilitar o Kubernetes no Docker Desktop: Settings → Kubernetes → Enable Kubernetes (aguardar status "running").
3. Validar cada um:
   - `docker run hello-world`
   - `kubectl cluster-info` e `kubectl get nodes` (contexto `docker-desktop`)
   - `k6 version`
   - Wireshark capturando `loopback` com filtro `tcp`
   - Tailscale com ao menos 1 segundo dispositivo (ou celular) na mesma tailnet.

## Critério de pronto

- [ ] Todos os comandos de validação executam sem erro.
- [ ] Print/evidência dos 5 checks salva na issue (ou no repo em `docs/evidencias/LAB-001.md`).

## Falha provocada

- N/A (issue de setup). Registrar na issue qualquer erro de instalação encontrado e como foi resolvido — vira runbook futuro.

## Papel da IA

- Tutora: explicar o que cada ferramenta resolve antes de instalar.
- Examinadora: 3 perguntas sobre quando usar cada uma.
