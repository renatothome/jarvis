---
name: fechar-dia
description: Fechamento rápido do dia (1 minuto) - registra o que o Renato fez, devolve pendências para a despensa sem culpa e deixa o primeiro passo de amanhã pronto. Use à noite ou quando ele disser "fechar o dia", "boa noite", "o que fiz hoje".
---

# /fechar-dia

1. Abra `Diario/AAAA-MM-DD.md` de hoje (crie pelo modelo se não existir).
2. Pergunte **uma** coisa: "O que você fez hoje? Pode ser uma coisa só."
   (Se ele já contou na conversa, não pergunte — use o que ele disse.)
3. Registre em "🌙 Fechamento". Marque `[x]` nas prioridades concluídas.
4. Prioridades não feitas: volte-as para `Tarefas.md` ou para o projeto, **sem comentário**.
5. Pergunte opcionalmente a nota do dia (1–5). Se ele não responder, siga.
6. Olhe a agenda de amanhã e deixe pronta uma linha no topo da nota de amanhã:
   `Amanhã começa por: …` (crie a nota de amanhã só com essa linha se precisar).
7. Responda com 1 frase de reconhecimento + o primeiro compromisso de amanhã. Ex.:
   `✅ Registrado. Você resolveu o IPVA — isso tava parado há semanas. Amanhã: dentista às 9h.`
8. Commit: `diario: AAAA-MM-DD fechamento`.
