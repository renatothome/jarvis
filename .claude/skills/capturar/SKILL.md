---
name: capturar
description: Captura rápida de qualquer coisa que o Renato disser (tarefa, ideia, lembrete, informação sobre alguém) e esvaziamento do Inbox, distribuindo itens para Tarefas, Projetos, Pessoas, Casa ou Referência. Use quando ele disser "anota", "lembra", "joga no inbox", ou pedir para organizar o inbox.
---

# /capturar

## Modo 1 — capturar (padrão quando vem texto junto)
1. Acrescente o texto como um item em `Inbox.md` (`- texto`), sem reescrever.
2. Responda em **uma linha**: `📥 Anotado.` (se tiver data clara, acrescente: `Coloquei pra 12/12.`)
3. Não pergunte onde colocar. Não comente. Não sugira nada.

## Modo 2 — esvaziar o Inbox
Fontes: `Inbox.md` e a lista de tarefas "Inbox" do Home Assistant, se existir
(`todo.inbox` — itens capturados por voz no iPhone; remova do HA depois de copiar).

Para cada item, decida sozinho:
| Se for… | Vai para… |
|---|---|
| Ação única | `Tarefas.md` → "Com data" (se tiver data) ou "Próximas" |
| Passo de um projeto existente | A nota do projeto, seção "Depois" |
| Algo com vários passos | Nova nota em `Projetos/` (modelo `Templates/Projeto.md`) com UM próximo passo |
| Informação sobre alguém | `Pessoas/Nome.md` (crie se não existir) |
| Sobre a casa | `Casa/` |
| Ideia vaga / "um dia" | `Tarefas.md` → "Algum dia / talvez" |
| Coisa para consultar | `Referencia/` |
| Compra | lista de compras do HA (`todo.shopping_list`) |

- Reescreva tarefas como **verbo + objeto concreto** ("Ligar para o dentista Dr. X").
- Converta datas relativas em absolutas (`📅 AAAA-MM-DD`).
- Remova do Inbox o que foi distribuído. Se algo for ambíguo, deixe no Inbox com `❓` na frente
  — não interrompa o Renato por isso.
- Ao final, uma linha: `📥 Inbox zerado: 4 tarefas, 1 projeto novo, 1 nota de pessoa.`
- Commit: `inbox: distribuído`.
