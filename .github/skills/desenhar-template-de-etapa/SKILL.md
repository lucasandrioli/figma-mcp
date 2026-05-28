---
name: desenhar-template-de-etapa
description: Decide ou ajusta o template reutilizável de uma etapa da jornada a partir do relatório consolidado.
---

# Desenhar Template de Etapa

## Arquivos desta skill

- [Regras de template](./references/regras-de-template.md)
- [Reconectar ao design system](./references/reconectar-ao-design-system.md)
- [Checklist de descoberta antes da escrita](./references/checklist-de-descoberta-antes-da-escrita.md)
- [Tools and Prompts do Figma MCP](../operar-jornada-clusterizada/references/tools-and-prompts-oficial-figma-mcp.md)

## Objetivo

Sair do diagnóstico e chegar a um template de etapa que suporte a maior cobertura possível sem ficar parametrizado demais.

## Disciplina de construção

- construa ou ajuste o template em passos pequenos;
- depois de cada componente ou template criado, valide estrutura antes de seguir;
- confirme com leitura estrutural se altura, padding, hug/fill e bounding continuam coerentes;
- se a referência estiver quebrada, use-a como evidência de negócio, não como modelo de construção.
- antes de escrever algo novo, confirme por `get_libraries` e `search_design_system` se a library oficial já oferece o componente, token ou style necessário.
- não faça `use_figma` mutando canvas antes de passar pelo checklist de descoberta.

## Regra de reconstrução

O material de referência serve para:

- entender estrutura;
- entender variações;
- identificar componentes usados;
- detectar defeitos estruturais.

O template final não deve nascer por clone do frame analisado.

Ele deve ser reconstruído do zero usando:

- instâncias das libraries oficiais conectadas ao arquivo;
- tokens da library oficial de tokens;
- inventário de componentes observado nas referências como pista de busca.
- classificação por bloco em:
  - `already-connected`
  - `exact-swap`
  - `compose-from-primitives`
  - `blocked`

## Validação mínima antes de aceitar um componente ou template

- o conteúdo cabe com respiro real dentro do container;
- a altura do container comporta `conteúdo + padding`;
- textos variáveis não ficam presos em alturas fixas frágeis;
- o `component set` engloba todas as variantes sem corte;
- a composição cresce por `HUG` quando o conteúdo cresce;
- alterações de adicionais selecionados entram primeiro nos blocos corretos da tela, antes de virar card extra genérico.
