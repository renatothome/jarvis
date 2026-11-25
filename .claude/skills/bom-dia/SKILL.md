---
name: bom-dia
description: Briefing da manhã do Renato. Monta a nota do dia em Diario/ com no máximo 3 prioridades (cada uma com primeiro passo), agenda, avisos da casa e e-mails importantes. Use quando ele disser bom dia, pedir o plano do dia ou em execução agendada de manhã.
---

# /bom-dia

Objetivo: em **2 minutos de leitura**, o Renato sabe o que importa hoje e por onde começar.

## Passos
1. Data de hoje (America/Sao_Paulo). Arquivo: `Diario/AAAA-MM-DD.md`.
   Se não existir, crie a partir de `Templates/Diario.md` (substitua `{{date:...}}` pelo dia por extenso).
2. Leia rapidamente: `Eu.md`, `Inbox.md`, `Tarefas.md`, os projetos ativos em `Projetos/`
   e a nota de ontem em `Diario/` (o que ficou aberto).
3. Contexto externo (pule em silêncio o que não estiver disponível):
   - **Agenda**: eventos de hoje e amanhã cedo no Google Calendar — "Agenda Principal"
     (`renato.thome@gmail.com`) e **"Contas Renato"** (contas a pagar: avise de vencimentos de hoje
     até os próximos 3 dias) — e nos calendários do Home Assistant.
   - **Casa** (Home Assistant): clima de hoje (`weather.forecast_home`; se estiver indisponível, avise em uma linha), quem está em casa,
     alertas/reparos críticos, bateria baixa de algo importante.
   - **Gmail**: só e-mails das últimas 24h que pedem ação dele (banco, governo, escola, trabalho).
     Ignore promoções e newsletters.
   - **Escolas** (ver `Areas/Escolas.md`): procure no Gmail comunicados das últimas 24h de
     `clipescola@clipemail.net` (Lumière/Gabriel), `domboscosantoandre.com.br` (Catarina) e `informes@mail.arbos.com.br` / `@arbos.com.br` (Colégio
     **Arbos**, Pedro). O e-mail do ClipEscola só traz o título; se houver link do Google Drive
     (circular em PDF), leia o arquivo. O Arbos manda a circular como **PDF anexo**: baixe e leia.
     Para cada atividade nova que exija algo da família (levar algo, fantasia, evento, reunião),
     crie um evento na agenda **`calendar.lembretes_jarvis`** do Home Assistant na noite anterior
     (19h30, 15 min, título curto com emoji, descrição com o primeiro passo) — ele vira lembrete em camadas. Atualize `Areas/Escolas.md` (comunicados recentes e **Próximas datas**).
     No resumo, mencione eventos escolares de **hoje e amanhã** e qualquer ocorrência com um dos filhos.
4. Se o Inbox tiver itens, distribua-os (ver skill `/capturar`, modo "esvaziar") antes de escolher prioridades.
5. Escolha **no máximo 3 prioridades** para hoje:
   - Primeiro o que tem data hoje/amanhã ou compromisso com outra pessoa.
   - Depois o próximo passo de algum projeto ativo.
   - Considere o tamanho da agenda: dia cheio de reuniões = 1 prioridade só.
   - Para cada uma, escreva um **primeiro passo de ≤ 5 min**.
6. Preencha a nota do dia (seções 🎯 Hoje, 📅 Agenda com horários, 🏠 Casa / avisos).
7. Responda no chat com um resumo **curto** (no máximo ~8 linhas):
   ```
   Bom dia, Renato ☀️  {clima em 1 frase}
   📅 {próximo compromisso — horário e quanto falta}
   🎯 1. … → comece por: …
      2. …
      3. …
   ⚠️ {só se houver algo urgente}
   ```
8. **Execução agendada** (sem o Renato no chat): mande também esse resumo como notificação
   para o iPhone: ação `notify.mobile_app_iphone_de_renato`, `title: "Bom dia ☀️"`, `message:` o resumo.
   (Agendado na nuvem: rotina "Jarvis — Bom dia (seg-sex 08:15)" em claude.ai/code/routines —
   roda sem PC ligado e dá push direto na `main`. A tarefa local no Dell G15 está pausada.)
   No chat interativo, só notifique se ele pedir.
9. **Contas vencendo (execução agendada e interativa):** para cada evento da agenda "Contas Renato"
   que vence **hoje ou amanhã** e ainda não tem "PAGO" no título, dispare o lembrete em camadas do
   Home Assistant (uma chamada por conta):
   - ação `script.jarvis_lembrete_em_camadas` com
     `titulo: "💸 Pagar <nome da conta>"`,
     `mensagem: "Vence <hoje|amanhã, DD/MM>. Primeiro passo: abrir o app do banco e achar o boleto."`,
     `id: "conta_<nome-curto-sem-espaço>"`, `repeticoes: 4`, `intervalo_min: 15`.
   - Conta que vence em 2–3 dias: só mencione no resumo, sem lembrete em camadas.
   - Quando o Renato disser que pagou, adicione "PAGO ✅" ao título do evento no Google Calendar.
10. Commit no git: `diario: AAAA-MM-DD bom dia`.

## Não fazer
- Não listar todas as tarefas. Não mencionar atrasos. Não sugerir mais de 3 coisas.
