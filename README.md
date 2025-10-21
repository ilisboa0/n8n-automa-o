# Automação de Confirmação de Pedidos (n8n + Docker)

Confirme pedidos via **WhatsApp** antes do envio usando **n8n** dentro de **Docker**.  
Este repositório traz o `docker-compose.yml`, um `.env.example` e o blueprint do workflow para importar no n8n.

## ✨ O que faz
- Lê pedidos (webhook/API/planilha)
- Dispara mensagem de confirmação no WhatsApp (template)
- Aguarda resposta (Sim/Não), registra status e segue a regra:
  - **Sim:** confirma e notifica envio (atualiza planilha/ERP)
  - **Não/sem resposta:** cria follow-up e agenda recontato
- Gera logs/métricas para acompanhamento

## 🧱 Stack
- [n8n](https://n8n.io/) (no/low-code)
- Docker + docker compose

## 🚀 Como subir
1. Copie `.env.example` para `.env` e ajuste:
   - `N8N_HOST`, `N8N_PORT`, `N8N_PROTOCOL`
   - `WEBHOOK_URL` (se for expor webhooks)
   - `GENERIC_TIMEZONE` e `TZ` (ex.: `America/Sao_Paulo`)
   - **`N8N_ENCRYPTION_KEY`** (coloque uma chave forte!)
2. Suba o serviço:
   ```bash
   docker compose up -d
