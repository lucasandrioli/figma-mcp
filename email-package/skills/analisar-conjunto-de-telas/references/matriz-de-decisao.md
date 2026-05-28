# Matriz de Decisão

| Situação | Decisão |
|---|---|
| Mesmo bloco, mesmo papel, só muda texto | `string` |
| Mesmo bloco, aparece em alguns clusters e em outros não | `boolean` |
| Mesmo bloco, aparece só quando um adicional foi contratado | `boolean` do domínio |
| Mesmo bloco, muda por modalidade sem mudar a função | `variable` do domínio ou `mode` específico se houver alta recorrência |
| Mesmo bloco, muda por aberto/fechado ou estado de interação | `variant` |
| Mesma tela-base, mas a composição cresce quando um adicional é selecionado | `boolean`, `variant` ou composição parametrizada da mesma tela |
| Adicional selecionado altera juros, totais, resumos ou informações já existentes na tela | manter no mesmo bloco estrutural e parametrizar conteúdo/estado antes de criar novo card |
| Mudança abre outra composição com layout próprio | `tela` do mesmo módulo |
| Mudança quebra a arquitetura ou troca a função do bloco | `estrutural` |

## Regra fixa

`mode` representa cluster.  
`variant` representa estado/interação.
