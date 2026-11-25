# 🥗 Alimentação

> O Jarvis usa esta nota para montar o cardápio da semana, a lista de compras e o lembrete do jantar.

## Regras da casa
- Cardápio **saudável** sempre.
- **Família toda (Luana, Renato e crianças): sem gordura, sem açúcar, sem glúten.**

## Rotina
- Renato trabalha até ~17h e busca as crianças às 18h.
- **Janela do jantar das crianças: 17h–17h40** → preparar algo rápido, ou adiantar, ou conferir se já tem pronto.
- Ideal: jantares que fiquem prontos em até ~30–40 min ou que possam ser adiantados (marmitas, forno, panela de pressão).

## 🍽️ Lembrete do jantar (automático)
- Seg–sex **17h**: `automation.jarvis_jantar_das_criancas_17h`
  - O Claude (AI Task do HA) sugere 1 prato seguindo as regras da casa, pronto em até 40 min, com primeiro passo.
  - Evita repetir os últimos pratos (guardados em `input_text.jarvis_jantares_recentes`).
  - Dispara o lembrete em camadas (2x a cada 10 min) com a sugestão.
- Ideia futura: usar a lista de compras/o que tem em casa para sugerir com o que já existe.

## Crianças
- Comem de tudo e geralmente o mesmo que os pais.
- **Seguem a mesma regra da casa** (sem gordura, sem açúcar, sem glúten).
- Catarina: teve suspeita de restrição à proteína do leite, já superada — sem restrição hoje.

## Compras
- Renato **não tem dia fixo** para planejar: compra conforme as coisas acabam.
- Rotina combinada: **acabou algo → fala na hora** e vai para a lista de compras do HA (`todo.shopping_list`).
  - Voz no app HA / Assist: "comprar …", "acabou o …", "precisa comprar …"
    (automação `automation.jarvis_comprar_voz_lista_de_compras`)
  - Pelo iPhone: Atalho "Compras Jarvis" (mesmo modelo do "Inbox Jarvis", trocando `todo.inbox` por `todo.shopping_list`)
  - Itens de compra que caírem no Inbox vão para a lista de compras no /capturar.
- O cardápio da semana (quando existir) complementa a lista com os ingredientes que faltam.

## A completar
- Pratos que já funcionam bem em casa:
