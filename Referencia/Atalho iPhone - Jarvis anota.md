# 📱 Atalho do iPhone: "Jarvis anota"

Objetivo: dizer **"E aí Siri, Jarvis anota"**, falar a coisa, e ela cair no `todo.inbox` do Home Assistant.

Pré-requisito: app **Home Assistant** (Companion) instalado e logado no iPhone.

## Criar o Atalho (2 minutos)
1. Abra o app **Atalhos** → **+** (novo atalho).
2. Toque no nome no topo → renomeie para **Jarvis anota** (é a frase que a Siri vai ouvir).
3. **Adicionar ação** → busque **Ditar Texto**. Idioma: Português (Brasil). Parar de ouvir: "Após pausa".
4. **Adicionar ação** → busque **Home Assistant** → escolha **Executar Ação** (em versões antigas: "Chamar Serviço").
   - Ação: `todo.add_item`
   - Dados (modo YAML/JSON):
     ```
     entity_id: todo.inbox
     item: [Texto Ditado]
     ```
     (para inserir *Texto Ditado*, toque na variável mágica que aparece acima do teclado)
5. (Opcional) **Adicionar ação** → **Mostrar Notificação** com texto `📥 Anotado: [Texto Ditado]`.
6. Concluir.

## Usar
- "E aí Siri, **Jarvis anota**" → fale → pronto.
- Também dá para colocar o Atalho na **tela inicial**, no **botão de Ação** do iPhone ou como **complicação no Apple Watch**.

## Alternativa sem Atalho
- No app Home Assistant → **Assist** → digite ou fale: `anota comprar pilha`.

## ⚠️ Nome do atalho
A Siri entende "anota" como comando do app **Notas** e ignora o atalho.
Por isso o atalho se chama **Inbox Jarvis** (sem a palavra "anota").
Fale só o nome, espere o sinal de escuta e aí diga o conteúdo.

## Se der erro
- "Ação não encontrada": confira se é `todo.add_item` (com ponto) e se o app HA está atualizado.
- Item chega vazio: a variável *Texto Ditado* não foi inserida no campo `item`.
