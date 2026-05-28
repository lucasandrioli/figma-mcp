# Figma MCP para Jornada Clusterizada

Este repositório prepara uma operação de design agêntica para jornadas com:

- várias etapas;
- vários módulos e telas por etapa;
- estados de interação;
- variações por cluster;
- variações por modalidade;
- variações por adicionais e produtos opcionais.

O caso de `consentimento` foi usado como prova de conceito, mas a arquitetura agora está desenhada para escalar para:

- `consentimento`
- `simulacao`
- `revisao`
- `efetivacao`

## Princípio de escala

Não crie um agente por tela.

Também não crie uma skill por tela.

Escala aqui significa:

- poucos agentes por função;
- skills reutilizáveis por função;
- contexto específico por etapa da jornada;
- agrupamento de telas por conjunto comparável;
- classificação explícita dos eixos de variação.

## Estrutura

```txt
figma-mcp/
  .github/
    agents/
      operador-de-jornada.agent.md
      analista-de-conjunto-de-telas.agent.md
      normalizador-de-handoff-de-etapa.agent.md
      desenhador-de-template-de-etapa.agent.md
      planejador-de-parametrizacao-de-etapa.agent.md
      criador-de-parametrizacao-de-etapa.agent.md
      curador-de-aprendizado-de-jornada.agent.md

    skills/
      operar-jornada-clusterizada/
      analisar-conjunto-de-telas/
      normalizar-handoff-de-etapa/
      desenhar-template-de-etapa/
      planejar-parametrizacao-de-etapa/
      criar-parametrizacao-de-etapa/
      curar-aprendizado-de-jornada/
      jornada-consignado-clusterizado/
```

## Agentes

- `operador-de-jornada`
  Orquestra a operação ponta a ponta e é o agente principal visível no VS Code.

- `analista-de-conjunto-de-telas`
  Lê um grupo comparável de telas da mesma etapa. Preferencialmente usado como worker/subagent.

- `normalizador-de-handoff-de-etapa`
  Consolida as análises parciais. Preferencialmente usado como worker/subagent.

- `desenhador-de-template-de-etapa`
  Decide ou ajusta o template reutilizável da etapa. Preferencialmente usado como worker/subagent.

- `planejador-de-parametrizacao-de-etapa`
  Define modes, strings, booleans, variants e limites. Preferencialmente usado como worker/subagent.

- `criador-de-parametrizacao-de-etapa`
  Escreve collection, modes, variables e binds no Figma. Preferencialmente usado como worker/subagent.

- `curador-de-aprendizado-de-jornada`
  Registra feedback, erros, acertos e melhorias propostas. Preferencialmente usado como worker/subagent.

## Skills

- `operar-jornada-clusterizada`
  Modelo operacional e disciplina de execução.

- `analisar-conjunto-de-telas`
  Método de leitura e classificação estrutural.

- `normalizar-handoff-de-etapa`
  Contrato de consolidação.

- `desenhar-template-de-etapa`
  Regras para decidir template.

- `planejar-parametrizacao-de-etapa`
  Regras para decidir o que vira mode, string, boolean e variant.

- `criar-parametrizacao-de-etapa`
  Etapa final de escrita.

- `curar-aprendizado-de-jornada`
  Memória operacional da jornada.

- `jornada-consignado-clusterizado`
  Contexto das etapas `consentimento`, `simulacao`, `revisao` e `efetivacao`.

## Fluxo operacional

1. Escolher a etapa da jornada.
2. Preencher o `briefing de etapa`.
3. Mapear módulos, telas, estados, modalidades, adicionais e clusters.
4. Montar o `plano de agrupamento`.
5. Rodar o `analista-de-conjunto-de-telas` em cada grupo.
6. Consolidar com o `normalizador-de-handoff-de-etapa`.
7. Decidir o template com o `desenhador-de-template-de-etapa`.
8. Planejar a parametrização com o `planejador-de-parametrizacao-de-etapa`.
9. Escrever no Figma com o `criador-de-parametrizacao-de-etapa`.
10. Registrar aprendizado com o `curador-de-aprendizado-de-jornada`.

## Modelo de execução no VS Code

- `operador-de-jornada` é o agente principal do picker;
- os demais agents podem operar como workers/subagents internos;
- leitura e análise podem usar fan-out por conjunto, frame ou modalidade;
- escrita com `use_figma` continua sempre sequencial.

## Como isso escala no Itaú

Você não vai precisar criar um agente novo para cada tela.

Na prática, para uma nova etapa:

1. preencha o contexto da etapa;
2. descreva os módulos e telas da etapa;
3. descreva os grupos de telas comparáveis e a convenção de nomeação dos frames;
4. classifique o que varia por cluster, modalidade, adicionais e estado;
5. rode o mesmo pipeline;
6. só crie nova skill ou novo agente se a etapa exigir uma lógica realmente diferente.

## Convenção útil de nomeação

Use a nomeação dos frames como sinal semântico para o agente:

- `Etapa/Tela - Padrao`
- `Etapa/Tela - Cluster1`
- `Etapa/Tela - Cluster2`
- `Etapa/Tela - Modalidade Refinanciamento`
- `Etapa/Tela - Seguro`

Essa convenção não substitui o chat, mas reduz ambiguidade. O agente deve ler esses nomes como hipótese inicial e confirmar no chat quando houver risco de interpretação errada.

## Operação com links

Prefira sempre trabalhar com:

- links de frame específicos com `node-id`

em vez de:

- links genéricos do arquivo inteiro sem recorte.

Isso melhora:

- precisão da análise;
- fan-out por grupo ou frame;
- rastreabilidade do handoff;
- redução de ambiguidade na reconstrução.

## Quando criar algo novo

Crie um novo artefato apenas se uma destas condições acontecer:

- a etapa exigir outra lógica de template;
- a etapa exigir outro tipo de parametrização;
- a etapa exigir outra governança;
- a etapa tiver um padrão que não cabe no pipeline atual.

Se não houver isso, reuse a arquitetura existente.

## Disciplina de tools MCP

### Leitura

- `get_libraries`
- `get_metadata`
- `get_design_context`
- `get_variable_defs`
- `search_design_system`

### Escrita

- `use_figma`

Regra:

- leitura e decisão não escrevem;
- escrita acontece explicitamente e só na etapa final.
- `use_figma` não deve mutar canvas antes da descoberta mínima de libraries, componentes, tokens e estratégia por bloco.

Referência recomendada:

- [Tools and Prompts do Figma MCP](./.github/skills/operar-jornada-clusterizada/references/tools-and-prompts-oficial-figma-mcp.md)

## Aprendizados já incorporados

- separar cluster, modalidade, adicionais, estado, módulo e tela evita erro de modelagem;
- a library de tokens deve ser tratada separadamente da library de componentes;
- referências copiadas de outros arquivos podem carregar componentes locais; esses componentes devem virar pista de busca, não base oficial de reconstrução;
- o template-base não deve receber mode explícito de cluster;
- cluster vive em `mode`;
- aberto/fechado vive em `variant`;
- collections não servem só para texto; podem concentrar strings, booleans e outros parâmetros locais de domínio;
- a POC de consentimento já está registrada como exemplo em `planejar-parametrizacao-de-etapa/artefatos/exemplos/`.
