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
   - **Agenda**: eventos de hoje e amanhã cedo (calendários do Home Assistant e, se houver, Google Calendar).
   - **Casa** (Home Assistant): clima de hoje (`weather.cidade_viva`), quem está em casa,
     alertas/reparos críticos, bateria baixa de algo importante.
   - **Gmail**: só e-mails das últimas 24h que pedem ação dele (banco, governo, escola, trabalho).
     Ignore promoções e newsletters.
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
   para o iPhone: `notify.send_message`, `entity_id: notify.iphone_de_renato`, título "Bom dia ☀️".
   No chat interativo, só notifique se ele pedir.
9. Commit no git: `diario: AAAA-MM-DD bom dia`.

## Não fazer
- Não listar todas as tarefas. Não mencionar atrasos. Não sugerir mais de 3 coisas.
