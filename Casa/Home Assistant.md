# 🏠 Home Assistant

> Manual da casa em linguagem humana. O Jarvis consulta isto antes de mexer em qualquer coisa.
> Levantamento inicial feito pelo Jarvis em 2026-11-25 (só leitura).

## Sistema
- Home Assistant **2026.11.2** num Raspberry Pi, local "Cidade Viva", fuso America/Sao_Paulo
- Zigbee2MQTT, Mosquitto, Music Assistant, AppDaemon, UniFi
- ⚠️ **Alerta crítico de subtensão no Raspberry Pi desde 20/11/2026** — trocar a fonte por uma oficial

## Cômodos
Sala · Cozinha · Suíte Casal · Lavabo · Quarto Meninos · Quarto Catarina · Varanda · Área de Serviço · Escritório

## Pessoas e presença
- `person.renato_thome_dias_lucente`, Luana, Marli
- Presença via iPhone, Apple Watch e carro (Tiggo 8)

## Como falar com o Renato pela casa
| Canal | Como | Quando usar |
|---|---|---|
| Notificação iPhone | `notify.send_message` → `notify.iphone_de_renato` | Lembretes, briefing |
| Tablet da parede | `notify.sm_x200` (Fully Kiosk) | Avisos para a casa |
| Luz do escritório | `light.escritorio_luz_do_escritorio`, `light.escritorio_led_do_escritorio` | Lembrete visual / modo foco |
| Voz | Assist / agente `conversation.claude_conversation` ("Jarvis") | Conversa |

## Listas e agenda no HA
- `todo.inbox` — **Inbox do Jarvis** (captura por voz). Criada em 2026-11-25.
  - Voz: "anota …", "jarvis anota …", "joga no inbox …" → automação `automation.jarvis_anota_no_inbox_voz`
  - O agente "Jarvis" do HA também entende "anota …" (chama a lista de "Lista do Jarvis")
  - O /capturar (modo esvaziar) copia os itens para o vault e remove do HA
- `todo.shopping_list` — lista de compras
- Calendário: só "Rodízio - suspensões" (falta conectar a agenda pessoal)

## Automações existentes (resumo)
- Apagar luzes sem movimento (por cômodo)
- Casa vazia → apagar tudo (com pergunta no iPhone)
- "Renato não está em casa"
- Botões de cena (corredor, escritório)
- Correções de comando dos ares (Sala, Meninos)

## 🚦 Regras de permissão do Jarvis
**Pode fazer sem perguntar:**
- Ler qualquer estado, histórico, câmera só se pedido
- Ligar/desligar/mudar cor de luzes
- Mandar notificação para o iPhone do Renato
- Adicionar itens em listas de tarefas/compras

**Precisa confirmar antes:**
- Ar-condicionado, TV, aspirador
- Criar, alterar ou apagar automações/scripts
- Notificar outras pessoas (Luana, tablet da casa)

**Nunca:**
- Desbloquear câmeras do tablet, mexer em alarme
- Reiniciar o HA, apagar backups, atualizar sistema
