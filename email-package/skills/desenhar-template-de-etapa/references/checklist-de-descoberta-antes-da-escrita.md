# Checklist de Descoberta Antes da Escrita

Use este checklist antes de qualquer `use_figma` que vá mutar canvas.

## Hard gates

É proibido escrever no Figma antes de confirmar:

- qual é a etapa;
- qual é o módulo;
- qual é a tela;
- qual é o conjunto comparável que está sendo tratado;
- quais são os eixos de variação relevantes:
  - cluster
  - modalidade
  - adicionais
  - estado
- quais libraries oficiais estão conectadas;
- quais componentes equivalentes já existem ou não;
- qual estratégia cada bloco pede:
  - `already-connected`
  - `exact-swap`
  - `compose-from-primitives`
  - `blocked`

## Checklist mínimo

Antes de escrever, confirme explicitamente:

- `get_metadata` foi usado para leitura leve da árvore quando necessário;
- `get_design_context` foi usado para entender a composição do que será reconstruído;
- `get_libraries` foi usado para descobrir o universo oficial disponível;
- `search_design_system` foi usado antes de recriar componente oficial do zero;
- o inventário de instâncias e componentes locais foi capturado;
- a variant correta foi decidida por semântica e contexto, não por default cego;
- o write será pequeno e localizado;
- a validação pós-write já está prevista.

## Regra de bloqueio

Se algum desses itens estiver em aberto:

- não escreva;
- registre a pendência;
- continue a descoberta ou peça confirmação humana curta no chat.
