# Referência de Tools MCP do Figma

Este arquivo existe para deixar **visível na raiz** a referência mais importante de operação do projeto:

- quando usar cada tool MCP do Figma
- qual ordem preferir
- quando ler
- quando decidir
- quando escrever

Fonte principal no projeto:

- [.github/skills/operar-jornada-clusterizada/references/tools-and-prompts-oficial-figma-mcp.md](./.github/skills/operar-jornada-clusterizada/references/tools-and-prompts-oficial-figma-mcp.md)

Use esse arquivo da `.github` como fonte operacional completa.

## Resumo rápido

### Leitura principal

- `get_design_context`
- `get_metadata`
- `get_libraries`
- `get_variable_defs`
- `search_design_system`

### Escrita

- `use_figma`

## Regra de ouro

- não misture análise com escrita;
- não use `use_figma` para mutar canvas antes de fechar descoberta mínima;
- não recrie design system antes de procurar nas libraries oficiais;
- não trate `get_metadata` como substituto de `get_design_context`.

## Ordem preferida

### Analisar telas comparáveis

1. `get_metadata`
2. `get_design_context`
3. `get_libraries`
4. `search_design_system`
5. `use_figma` read-only, se necessário

### Reconstruir template com design system oficial

1. `get_libraries`
2. `search_design_system`
3. `get_design_context`
4. `get_variable_defs`, se necessário
5. `use_figma`

### Planejar parametrização

1. `get_design_context`
2. `get_variable_defs`
3. `get_libraries`
4. `search_design_system`, se necessário

### Criar parametrização

1. análise e plano fechados
2. `use_figma` para escrita final
