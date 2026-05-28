---
name: analisar-conjunto-de-telas
description: Analisa um conjunto comparável de telas da mesma etapa para separar estrutura, cluster, estado, modalidade, adicionais, módulo e tela.
---

# Analisar Conjunto de Telas

## Use esta skill quando

- você tiver um conjunto claro de telas comparáveis;
- todas pertencerem à mesma etapa da jornada;
- a meta for decidir o que muda por cluster, por estado, por modalidade, por adicionais e por tela.

## Arquivos desta skill

- [Contrato de saída](./references/contrato-de-saida.md)
- [Heurísticas estruturais](./references/heuristicas-estruturais.md)
- [Agrupamento de telas](./references/agrupamento-de-telas.md)
- [Matriz de decisão](./references/matriz-de-decisao.md)
- [Tools and Prompts do Figma MCP](../operar-jornada-clusterizada/references/tools-and-prompts-oficial-figma-mcp.md)

## Regras

- analise um grupo por vez;
- prefira trabalhar com link de frame ou node-id específico, não só com link genérico do arquivo;
- use a nomenclatura dos frames como pista inicial, não como verdade absoluta;
- se encontrar nomes como `Cluster`, `Padrao`, `Modalidade`, `Seguro` ou `Portabilidade`, trate isso como hipótese de leitura;
- quando frames com o mesmo prefixo tiverem sufixos semânticos diferentes e a leitura estrutural mostrar composição diferente, trate isso como variação deliberada da mesma tela;
- antes de concluir a análise, faça perguntas curtas no chat para confirmar ambiguidades relevantes;
- consolide o entendimento confirmado antes de classificar template, boolean, variant ou outra tela;
- não desenhe template;
- não crie variables;
- não escreva no Figma.

## Rotina de captura do inventário

Antes de concluir a análise, capture o inventário dos componentes observados nas referências com esta ordem:

1. `get_metadata`
   - use para visão rápida da árvore, nomes, tipos, tamanhos e hierarquia.
2. `get_design_context`
   - use para entender melhor composição, instâncias, blocos, textos e relações estruturais.
3. `get_libraries`
   - use para descobrir quais libraries oficiais estão conectadas no arquivo atual.
4. `search_design_system`
   - use os nomes e padrões encontrados nas referências para procurar equivalentes nas libraries oficiais conectadas.
5. `use_figma` em modo somente leitura
   - use apenas quando precisar de inventário mais preciso, por exemplo para separar instâncias, componentes locais, nomes de variants e outros detalhes programáticos.

Siga a referência `Tools and Prompts do Figma MCP` para decidir quando parar no `get_metadata`, quando aprofundar com `get_design_context` e quando vale escalar para `use_figma` read-only.

## Resultado esperado da captura

O analista deve sair dessa etapa com:

- instâncias observadas nas referências;
- componentes locais observados nas referências;
- padrões de naming úteis para busca;
- candidatos prováveis de equivalência nas libraries oficiais conectadas.
