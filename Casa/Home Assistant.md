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
| Notificação iPhone | ação `notify.mobile_app_iphone_de_renato` (urgente: `interruption-level: time-sensitive`) | Lembretes, briefing |
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

## Automações do Jarvis
- `automation.jarvis_anota_no_inbox_voz` — "anota …" → `todo.inbox`
- `script.jarvis_lembrete_em_camadas` — **lembrete em camadas** (usar para tudo que é importante):
  campos `titulo`, `mensagem`, `id` (curto, sem espaço), `repeticoes` (padrão 3), `intervalo_min` (padrão 5).
  1. Notificação urgente no iPhone com botão "OK, vi ✅" (a nova substitui a anterior pela tag)
  2. Se Renato em casa: luz piscando nos cômodos com movimento nos últimos 15 min
  3. Repete até ele tocar em "OK, vi" ou acabar as repetições
  - 🔇 Sem voz por enquanto. **Não usar TV da sala nem caixa Bose para avisos** (decisão do Renato, 2026-11-25).
    Ele vai comprar/definir outro equipamento para voz depois.
- `automation.jarvis_lembrete_buscar_as_criancas_17h40` — seg–sex 17h40 → chama o lembrete em camadas
  ("🚗 Buscar as crianças", 3 repetições a cada 5 min)

- `automation.jarvis_roupa_terminou_na_maquina` — fim do ciclo da máquina de lavar → lembrete em camadas
  "🧺 A roupa terminou" (4x a cada 15 min). Se terminar entre 22h e 7h, avisa às 7h.
  - Detecção: `sensor.area_de_servico_maquina_de_lavar_running_status` sai de `start` para `end`/`standby`,
    ou para `unavailable` depois de 30+ min (a máquina se desliga ~2 min após terminar).

- `automation.jarvis_comprar_voz_lista_de_compras` — "comprar …"/"acabou o …" → `todo.shopping_list`
- `automation.jarvis_jantar_das_criancas_17h` — seg–sex 17h: sugestão de jantar pela IA → lembrete em camadas
  (detalhes em [[Alimentação]])

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
- Avisos no tablet da casa

**Nunca (decisão do Renato, 2026-11-25):**
- Envolver a Luana ou outras pessoas nos lembretes/notificações do Renato

**Nunca:**
- Desbloquear câmeras do tablet, mexer em alarme
- Reiniciar o HA, apagar backups, atualizar sistema
