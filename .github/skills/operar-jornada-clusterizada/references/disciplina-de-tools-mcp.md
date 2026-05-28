# Disciplina de Tools MCP

Consulte também:

- [Tools and Prompts do Figma MCP](./tools-and-prompts-oficial-figma-mcp.md)

## Leitura

Use:

- `get_libraries`
- `get_metadata`
- `get_design_context`
- `get_variable_defs`
- `search_design_system`

## Decisão

Durante análise, normalização, template e planejamento:

- não escrever no Figma
- não criar variables
- não mudar componentes

## Escrita

Use `use_figma` apenas:

- na construção final do template, quando aprovado;
- na criação final de collection, modes, variables e binds;
- em chamadas pequenas, explícitas e validadas depois.

## Hard gate de escrita

É proibido mutar canvas com `use_figma` antes de:

- fechar descoberta de libraries, componentes e tokens relevantes;
- fechar classificação por bloco;
- fechar escopo do write atual;
- preparar a validação pós-write.

## Observações importantes

- `get_design_context` é a leitura principal; `get_metadata` entra quando você precisa primeiro de uma visão leve da árvore ou quando o design é grande demais para aprofundar de uma vez.
- `get_libraries` e `search_design_system` devem acontecer antes de reconstruir qualquer padrão com design system oficial.
- `use_figma` pode ser usado em leitura somente quando `get_design_context` e `get_metadata` não bastarem.
