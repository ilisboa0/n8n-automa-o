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
- n8n (no/low-code)
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
   ```
3. Acesse o n8n em: `http://localhost:5678`
4. Importe o fluxo: **Workflows → Import** e selecione `workflows/confirmar-pedido.json`.

## 📁 Estrutura
```
.
├─ docker-compose.yml
├─ .env.example          # NÃO commitar .env real
├─ .gitignore
├─ README.md
├─ workflows/
│  └─ confirmar-pedido.json
└─ n8n-data/             # dados locais (NÃO versionar)
```

## 🔐 Segurança
- Nunca commitar chaves/tokens: use `.env`.
- Defina `N8N_ENCRYPTION_KEY` para criptografar credenciais.
- Se publicar, ajuste `N8N_HOST` e `WEBHOOK_URL` corretamente e proteja a interface do n8n.

## 🧪 Teste rápido do fluxo
- Dispare um pedido de exemplo (via webhook do n8n).
- Veja o log de execução no painel do n8n.
- Valide a mensagem chegando no WhatsApp de teste e a atualização de status.

## 📜 Licença
MIT — use, modifique e contribua.
