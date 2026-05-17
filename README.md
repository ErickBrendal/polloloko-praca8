# Pollo Loko Praça 8 — Sistema Multi-Canal

Sistema completo de pedidos da unidade **Pollo Loko Praça 8** em Guarulhos/SP. Stack: landing cinematográfica (Vercel) + agente WhatsApp Polly (n8n) + Sheets CRM.

[Site ao vivo](https://polloloko-praca8.vercel.app) • [Instagram](https://instagram.com/pollolokopraca8_oficial)

---

## Visão geral

A Pollo Loko Praça 8 é unidade franqueada da rede **Pollo Loko** (O Frango Frito Mais Loko da Sua Vizinhança), com mais de 80 unidades em São Paulo.

- **Endereço:** Av. Vila Matias, 205 — Guarulhos/SP
- **Horário:** 18h às 23h30 — todos os dias
- **WhatsApp/Tel:** (11) 99710-0012
- **Rating iFood:** 4.7 estrelas (71 avaliações Google)

O sistema centraliza pedidos vindos de **canal próprio (site + WhatsApp), iFood e 99Food** em um único CRM em Google Sheets.

---

## Componentes

### Site — `index.html`

Landing page cinematográfica com paleta oficial Pollo Loko (vermelho #ED2024 + amarelo + creme):

- Hero com tipografia massiva ("O FRANGO MAIS LOKO DE GUARULHOS")
- Banner de promoções rotativas (Mega Combo R$ 142, PIX 5% OFF)
- Stats bar (4.7 estrelas, +80 unidades, 25min, R$ 40 mínimo)
- Cardápio interativo com filtros (Combos, Meio Combos, Porções, Molhos, Bebidas)
- Mega Combo destaque (Combo 1 + Combo 2 = 32 peças por R$ 142, economia R$ 10)
- Carrinho lateral com wizard 3 passos (Itens → Seus Dados → Confirmar)
- Upsell automático (Coca 2L R$ 19,90)
- Google Maps + WhatsApp + Instagram
- Mobile-responsive

Deploy: [polloloko-praca8.vercel.app](https://polloloko-praca8.vercel.app)

### Polly — `polly-workflow-n8n.json`

Agente de atendimento digital no WhatsApp baseado em **n8n + WAHA + OpenAI GPT-4 Tools Agent**.

- Tom caloroso, direto, paulistano
- Máximo 4 linhas por mensagem, 1 pergunta por vez
- Tools: ler_cardapio, status_pedido, calcular_preco, gerar_link_pix, criar_pedido, transferir_humano
- Memória: Redis (sessão por número)
- Fallback humano via Telegram
- NPS embutido após confirmação de pedido

Workflow em produção como EBL Multinegocio v3.1 (roteamento por negocio: pizzaria).

### Sheets CRM — 4 abas

- **cardapio**: 21 itens (5 combos, 3 meio combos, 1 porção, 7 molhos, 5 bebidas)
- **pedidos**: histórico por canal (whatsapp, ifood, 99food, site)
- **clientes**: base com ticket médio, frequência e NPS
- **fidelidade**: sistema de pontos (em planejamento)

CSVs versão git: sheets-cardapio.csv, sheets-pedidos.csv, sheets-clientes.csv, sheets-fidelidade.csv.

---

## Cardápio oficial (preços iFood/99Food)

### Combos completos · 16 peças · serve até 3 pessoas

- Combo 1 · Pollo Loko (sortido) — R$ 76,00
- Combo 2 · Filé de Peito (Sassami empanado) — R$ 76,00
- Combo 3 · Asinha e Coxinha — R$ 76,00
- Combo 4 · Especial (24 peças, serve 4-5) — R$ 86,50

### Mega Combo Loko · exclusivo site/WhatsApp

- Combo 1 + Combo 2 = 32 peças (serve 6) — R$ 142,00 (economia R$ 10)

### Meio combos · 9 peças — todos R$ 56,50

- 1/2 Pollo Loko / 1/2 Filé / 1/2 Asinha e Coxinha

### Porções e bebidas

- Batata Rústica Grande + molho — R$ 21,00
- Coca-Cola 2L — R$ 19,90 · Lata 350ml — R$ 9,00
- Sukita 2L (Uva/Laranja/Limão) — R$ 14,00
- Molhos extras (combo já inclui 4) — R$ 7,00 cada

---

## Como rodar

### Site

```bash
git clone https://github.com/ErickBrendal/polloloko-praca8.git
cd polloloko-praca8
open index.html
```

Deploy automático na Vercel a cada push.

### Workflow n8n

1. Importe polly-workflow-n8n.json
2. Configure credenciais (WAHA, OpenAI, Redis, Google Sheets, Telegram)
3. Aponte webhook WAHA para https://SEU_N8N/webhook/multi-canal
4. No Redis, mapeie número WhatsApp para negocio: pizzaria

---

## Tecnologias

- **Frontend:** HTML/CSS/JS vanilla (sem build)
- **Deploy:** Vercel (static hosting, auto-deploy via GitHub)
- **Agente WhatsApp:** n8n Cloud + WAHA + OpenAI GPT-4 (Tools Agent)
- **Memória:** Redis (Upstash)
- **CRM:** Google Sheets
- **Notificação equipe:** Telegram Bot

---

## Status

- Site v5 publicado (paleta oficial Pollo Loko)
- Polly publicada em produção (n8n v3.2.1)
- Cardápio 21 itens validado contra iFood/99Food
- Google Sheets database criado com 4 abas
- Sistema de fidelidade (planejado)

---

## Licença e marca

Receita oficial Pollo Loko Franquias LTDA. Unidade Praça 8 é operação independente sob a marca **Pollo Loko**. Marca, identidade visual e cardápio são propriedade da Pollo Loko Franquias LTDA.

---

© 2026 Pollo Loko Praça 8 · Av. Vila Matias, 205 — Guarulhos/SP
