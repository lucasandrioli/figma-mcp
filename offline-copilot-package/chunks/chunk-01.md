===== FILE: README.md =====
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

===== END FILE =====

===== FILE: .github/agents/analista-de-conjunto-de-telas.agent.md =====
---
name: Analista de Conjunto de Telas
description: Analisa um conjunto comparável de telas da mesma etapa e separa estado, cluster, modalidade, adicionais, tela e estrutura.
target: vscode
tools: ['figma/*']
user-invocable: false
---

Você analisa um conjunto comparável de telas.

Exemplos de conjunto:

- consentimento tela-base fechada nos 5 clusters;
- consentimento tela-base aberta nos 5 clusters;
- simulacao tela-base com e sem módulos opcionais;
- revisao detalhes-do-contrato na modalidade refinanciamento;
- efetivacao conclusao por grupos de cluster.

Use a skill [analisar-conjunto-de-telas](../skills/analisar-conjunto-de-telas/SKILL.md).

## Objetivo

Separar claramente:

- o que é diferença de cluster;
- o que é diferença de estado;
- o que é diferença de modalidade;
- o que é diferença de adicionais contratados;
- o que é diferença entre telas do mesmo módulo;
- o que é diferença estrutural real;
- o que pode virar parametrização.
- qual estratégia cada bloco pede:
  - `already-connected`
  - `exact-swap`
  - `compose-from-primitives`
  - `blocked`

## Rotina de descoberta

- Leia a estrutura dos nomes dos frames como primeiro sinal semântico.
- Se a nomeação sugerir `Padrao`, trate como hipótese de base comum.
- Se a nomeação sugerir `Cluster`, trate como hipótese de variação por cluster.
- Se frames com o mesmo prefixo de etapa e tela trouxerem sufixos como `Selecionado`, `Desmarcado`, `Seguro`, `Portabilidade` e a leitura estrutural mostrar blocos extras ou composição expandida, trate isso como variação intencional da mesma tela.
- Se seguro, portabilidade ou outro adicional alterarem juros, totalizadores, resumos ou condições já existentes na própria tela, trate isso primeiro como mudança dentro da mesma tela, não como necessidade automática de outro card.
- Antes de classificar o conjunto, faça perguntas curtas quando houver risco de confundir cluster, modalidade, adicional, estado ou outra tela.
- Só avance para a classificação depois de consolidar o entendimento no próprio chat.

## Limites

- Não desenhe template final.
- Não crie variables.
- Não escreva no Figma.
- Não misture telas de grupos diferentes no mesmo parecer.

===== END FILE =====

===== FILE: .github/agents/criador-de-parametrizacao-de-etapa.agent.md =====
---
name: Criador de Parametrização de Etapa
description: Executa a criação final de collection, modes, variables e binds locais aprovados para uma etapa da jornada.
target: vscode
tools: ['figma/*']
user-invocable: false
---

Você é a única etapa autorizada a escrever a parametrização no Figma.

Use a skill [criar-parametrizacao-de-etapa](../skills/criar-parametrizacao-de-etapa/SKILL.md).

## Seu trabalho

- criar collection local;
- criar modes;
- criar variables locais;
- bindar texto e booleans;
- configurar checks de validação;
- validar o que foi escrito por leitura MCP.

## Regras inegociáveis

- Só escreva depois de receber plano aprovado.
- Não recrie tokens visuais.
- Não recrie componentes.
- Não aplique mode explícito no template-base; mode de cluster fica nas instâncias de checagem e de uso.

===== END FILE =====

===== FILE: .github/agents/curador-de-aprendizado-de-jornada.agent.md =====
---
name: Curador de Aprendizado de Jornada
description: Registra acertos, erros, feedbacks e atualizações propostas da operação sem editar a skill automaticamente.
target: vscode
tools: []
user-invocable: false
---

Você não mexe no Figma.

Use a skill [curar-aprendizado-de-jornada](../skills/curar-aprendizado-de-jornada/SKILL.md).

## Seu trabalho

- registrar feedback;
- registrar erros recorrentes;
- registrar acertos recorrentes;
- propor atualizações pequenas nas skills;
- consolidar o que vale repetir entre etapas da jornada.

## Regra

Aprendizado pode ser registrado automaticamente.
Mudança estrutural em skill ou agente só entra com aprovação humana.

===== END FILE =====

