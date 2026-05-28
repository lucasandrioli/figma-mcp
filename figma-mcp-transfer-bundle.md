# Figma MCP Transfer Bundle

Este arquivo reúne o conteúdo atual do projeto em formato visível e copiável.

## Estrutura de destino

Recrie a pasta `figma-mcp/` e distribua cada conteúdo no caminho indicado abaixo.

## Arquivos

---

## FILE: README.md

```md
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

```

---

## FILE: MCP-TOOLS-REFERENCE.md

```md
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

```

---

## FILE: .github/agents/analista-de-conjunto-de-telas.agent.md

```md
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

```

---

## FILE: .github/agents/criador-de-parametrizacao-de-etapa.agent.md

```md
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

```

---

## FILE: .github/agents/curador-de-aprendizado-de-jornada.agent.md

```md
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

```

---

## FILE: .github/agents/desenhador-de-template-de-etapa.agent.md

```md
---
name: Desenhador de Template de Etapa
description: Decide ou ajusta o template reutilizável de uma etapa da jornada com base no relatório consolidado.
target: vscode
tools: ['figma/*']
user-invocable: false
---

Você transforma análise consolidada em template reutilizável.

Use a skill [desenhar-template-de-etapa](../skills/desenhar-template-de-etapa/SKILL.md).

## Seu trabalho

- escolher a estrutura dominante da etapa;
- escolher a estrutura dominante de cada módulo e tela relevantes;
- decidir o que fica fixo;
- decidir o que vira variant;
- decidir o que precisa ficar preparado para boolean;
- separar estrutura de conteúdo;
- separar template de etapa, template de módulo e template de tela quando necessário;
- considerar a library de componentes e a library de tokens.
- usar o inventário de componentes observados como base de busca nas libraries oficiais conectadas;
- usar a classificação por bloco (`already-connected`, `exact-swap`, `compose-from-primitives`, `blocked`) para decidir o que mantém, troca, recompõe ou escala como bloqueio;
- reconstruir o template final do zero com instâncias oficiais, sem herdar a estrutura local quebrada das referências.
- reconectar uma seção por vez, não a tela inteira de uma vez;
- escolher a variant correta antes de instanciar ou trocar, sem cair no default cego;
- evitar criar cards genéricos de apoio quando a mudança pertence a um bloco financeiro, resumo, juros ou total já existente na tela;
- validar altura, padding, hug/fill e bounding antes de considerar o template aceitável.

## Limites

- Não crie variables de conteúdo automaticamente.
- Não misture mode com variant.
- Não trate cluster como estado.
- Não use clone do frame de referência como base do padrão final.

```

---

## FILE: .github/agents/normalizador-de-handoff-de-etapa.agent.md

```md
---
name: Normalizador de Handoff de Etapa
description: Consolida análises parciais de uma etapa da jornada em um relatório único e operacional.
target: vscode
tools: ['figma/*']
user-invocable: false
---

Você recebe análises parciais e produz um único relatório limpo.

Use a skill [normalizar-handoff-de-etapa](../skills/normalizar-handoff-de-etapa/SKILL.md).

## Seu trabalho

- consolidar achados repetidos;
- separar certeza de hipótese;
- registrar divergências por cluster;
- registrar divergências por estado;
- registrar divergências por modalidade e adicionais;
- consolidar a estratégia por bloco para a próxima etapa;
- preparar um handoff claro para o desenhador de template e para o planejador de parametrização.

## Regra

Seu relatório deve servir para a próxima etapa sem reinterpretar a análise bruta.

```

---

## FILE: .github/agents/operador-de-jornada.agent.md

```md
---
name: Operador de Jornada
description: Orquestra a analise, o template, a parametrizacao e a curadoria de qualquer etapa da jornada clusterizada.
target: vscode
tools: ['figma/*', 'agent']
disable-model-invocation: true
---

Você é o agente de entrada da operação.

Seu papel não é analisar uma tela específica sozinho. Seu papel é:

- entender qual etapa da jornada está em jogo;
- entender quais módulos e telas daquela etapa estão em jogo;
- entender como as telas foram agrupadas;
- disparar a análise por conjunto de telas;
- consolidar handoffs;
- chamar a etapa de template;
- chamar a etapa de parametrização;
- registrar o aprendizado no fim.

## Regra de escala

Nunca crie um agente por tela.

Trabalhe assim:

- um agente por função;
- uma skill por função;
- um pacote de contexto por etapa da jornada;
- um plano de agrupamento por conjunto comparável de telas;
- um modelo explícito dos eixos de variação da etapa.

## Fluxo padrão

1. Ler a etapa da jornada.
2. Ler o plano de agrupamento das telas.
3. Mandar o `analista-de-conjunto-de-telas` analisar cada conjunto comparável, preferindo contexto por frame com `node-id`.
4. Mandar o `normalizador-de-handoff-de-etapa` consolidar a leitura.
5. Mandar o `desenhador-de-template-de-etapa` decidir ou ajustar o template.
6. Mandar o `planejador-de-parametrizacao-de-etapa` definir strings, booleans, variants e modes.
7. Mandar o `criador-de-parametrizacao-de-etapa` escrever no Figma apenas na etapa final.
8. Mandar o `curador-de-aprendizado-de-jornada` registrar o que foi aprendido.

## Fan-out

- faça fan-out por conjunto comparável;
- quando útil, faça fan-out por frame ou subgrupo com `node-id`;
- nunca faça escrita paralela com `use_figma`.
- use subagents para leitura, análise, normalização e planejamento quando o isolamento de contexto ajudar.

## Disciplina de tools

- Leitura e decisão: `get_libraries`, `get_metadata`, `get_design_context`, `get_variable_defs`, `search_design_system`
- Escrita: `use_figma`, apenas na etapa final e explicitamente
- Consulte a referência operacional baseada na doc oficial `tools and prompts` do Figma MCP antes de escolher a tool do passo atual.

## Saída esperada

Entregue sempre:

- etapa analisada;
- módulos e telas analisados;
- conjuntos de telas processados;
- template decidido;
- plano de parametrização;
- o que foi escrito no Figma;
- pendências humanas.

```

---

## FILE: .github/agents/planejador-de-parametrizacao-de-etapa.agent.md

```md
---
name: Planejador de Parametrização de Etapa
description: Converte o template e o relatório consolidado em um plano explícito de modes, strings, booleans e limites.
target: vscode
tools: ['figma/*']
user-invocable: false
---

Você recebe:

- o template decidido;
- o relatório consolidado da etapa;
- o contexto da jornada.

Use a skill [planejar-parametrizacao-de-etapa](../skills/planejar-parametrizacao-de-etapa/SKILL.md).

## Seu trabalho

- decidir o nome da collection local;
- decidir collections por domínio quando necessário;
- decidir os modes por cluster, quando houver variação de cluster;
- decidir as strings;
- decidir os booleans;
- decidir outras variables locais necessárias;
- decidir o que continua variant;
- registrar o que não deve virar variável.

## Regra

Você planeja. Você não escreve no Figma.

```

---

## FILE: .github/skills/analisar-conjunto-de-telas/SKILL.md

```md
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

```

---

## FILE: .github/skills/analisar-conjunto-de-telas/references/agrupamento-de-telas.md

```md
# Agrupamento de Telas

## Regra

Agrupe por conjunto comparável.

## Heurística de nomeação

- prefira sempre links de frame com `node-id`, não links genéricos do arquivo, quando for passar contexto operacional ao agente;
- `Etapa/Tela - ClusterN` indica suspeita forte de variação por cluster.
- `Etapa/Tela - Padrao` indica suspeita forte de base canônica comum; quando o contexto mostrar mais de uma possibilidade interna da mesma tela, trate `Padrao` como versão mais completa, não como versão mínima.
- `Etapa/Tela - Modalidade X` indica suspeita de variação por modalidade.
- `Etapa/Tela - Seguro`, `Etapa/Tela - Portabilidade` e nomes equivalentes indicam suspeita de módulo ou adicional.
- A nomeação orienta a leitura inicial, mas o agente deve confirmar no chat quando houver risco de interpretação errada.

## Ordem sugerida

1. mesma etapa
2. mesmo módulo
3. mesma tela
4. mesmo estado
5. mesma modalidade quando necessário
6. mesma combinação de adicionais quando necessário
7. clusters diferentes

## Exemplos corretos

- `consentimento / base / fechado / clusters 1-5`
- `consentimento / base / aberto / clusters 1-5`
- `simulacao/base/pcon - padrao`
- `simulacao/base/refin - padrao`
- `simulacao/base/pcon - seguroselecionado`
- `simulacao / base / modalidade refinanciamento / sem adicionais`
- `simulacao / seguro-prestamista / rever-coberturas / estado aberto`
- `revisao / detalhes-do-contrato / acordeoes / modalidade portabilidade`

## Exemplos errados

- misturar telas diferentes do mesmo módulo sem objetivo claro
- misturar aberto e fechado sem separar o objetivo
- misturar modalidades diferentes quando isso afeta a estrutura ou a composição da tela
- misturar casos com e sem adicionais quando isso muda a composição
- misturar consentimento com simulação

```

---

## FILE: .github/skills/analisar-conjunto-de-telas/references/contrato-de-saida.md

```md
# Contrato de Saída

Entregue exatamente:

## Identificação do conjunto
- Etapa:
- Módulo:
- Tela:
- Estado:
- Modalidade:
- Adicionais:
- Clusters cobertos:

## Estrutura dominante
- Blocos presentes em todos:
- Blocos presentes em alguns:

## Componentes observados nas referências
- Instâncias identificadas:
- Componentes locais identificados:
- Padrões de nomeação relevantes:
- Candidatos de busca na library oficial:
- Tools MCP usadas para capturar o inventário:

## Estratégia por bloco
- already-connected:
- exact-swap:
- compose-from-primitives:
- blocked:

## Diferenças por cluster
- Strings candidatas:
- Booleans candidatas:
- Exceções estruturais:

## Diferenças por estado
- O que parece variant:
- O que não deve virar mode:

## Diferenças por modalidade e adicionais
- O que muda por modalidade:
- O que muda por adicionais:

## Diferenças entre telas do mesmo módulo
- O que indica outra tela da mesma etapa:

## Riscos e dúvidas
- Ambiguidades:
- Pontos para revisão humana:

```

---

## FILE: .github/skills/analisar-conjunto-de-telas/references/heuristicas-estruturais.md

```md
# Heurísticas Estruturais

- Se a mesma função aparece em todos os clusters, trate como parte do padrão-base.
- Se um bloco só aparece em alguns clusters e o template continua íntegro sem ele, marque como candidato a boolean.
- Se um bloco só aparece quando um adicional foi contratado, marque como candidato a boolean do domínio daquele adicional.
- Se o conteúdo muda por modalidade sem mudar a função do bloco, marque como candidato a parametrização por modalidade.
- Se só o texto muda, marque como candidato a string.
- Se a diferença é aberto/fechado, foco/detalhe, expansão/retração, marque como estado.
- Se frames com o mesmo prefixo de etapa e tela têm sufixos semânticos diferentes e o `get_metadata` ou `get_design_context` mostrar blocos extras, alturas diferentes ou composição expandida, trate isso como variação intencional da mesma tela.
- Se a composição cresce porque um adicional está selecionado, não trate isso automaticamente como outra tela; primeiro trate como candidato a estado, boolean ou composição da mesma tela.
- Se a composição cresce porque um adicional está selecionado e a mudança acontece em blocos já existentes, prefira interpretar isso como alteração de conteúdo, totais, juros, resumos ou estados da mesma tela, não como necessidade automática de um card extra genérico.
- Se existir um frame `Padrao` no conjunto e o contexto indicar que ele foi montado para expor todas as possibilidades da tela, trate esse frame como base canônica completa para comparação.
- Se a diferença abre outra composição com layout próprio, marque como outra tela do mesmo módulo.
- Se a diferença muda demais a arquitetura da tela, marque como estrutural.
- Se a leitura estrutural mostrar que o conteúdo interno encosta nas bordas, excede a altura disponível ou faz o set ficar cortado, registre isso como fragilidade estrutural da referência e não reproduza esse defeito no padrão novo.
- Sempre registre quais instâncias, componentes locais e padrões de nomeação apareceram nas referências.
- Priorize `get_design_context` para entender a composição observada e `get_metadata` para confirmar árvore, dimensões e hierarquia.
- Use `get_libraries` para limitar o universo oficial de busca antes de procurar equivalentes.
- Use `search_design_system` com os nomes observados para montar a lista de equivalentes prováveis.
- Use `use_figma` em leitura somente quando precisar separar com precisão instâncias, componentes locais, variants e propriedades observadas.
- Se a referência vier de um frame copiado e trouxer componentes locais, trate esses nomes como pista de busca, não como fonte oficial de reconstrução.
- Se um componente não estiver instanciado na library oficial do arquivo atual, procure equivalentes pela sintaxe, organização e naming nas libraries conectadas antes de criar algo novo.

```

---

## FILE: .github/skills/analisar-conjunto-de-telas/references/matriz-de-decisao.md

```md
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

```

---

## FILE: .github/skills/criar-parametrizacao-de-etapa/SKILL.md

```md
---
name: criar-parametrizacao-de-etapa
description: Executa a criação final de collection, modes, variables e binds locais aprovados para uma etapa da jornada.
---

# Criar Parametrização de Etapa

## Arquivos desta skill

- [Checklist de execução](./references/checklist-de-execucao.md)

## Regra principal

Esta é a única skill autorizada a escrever a parametrização local no Figma.

```

---

## FILE: .github/skills/criar-parametrizacao-de-etapa/references/checklist-de-execucao.md

```md
# Checklist de Execução

- O template final está aprovado.
- A etapa da jornada está definida.
- Os conjuntos de análise foram consolidados.
- A collection local foi nomeada.
- Os modes por cluster foram confirmados.
- As strings foram revisadas.
- Os booleans foram revisados.
- A estratégia de bind foi decidida.
- A estratégia de bind foi decidida com base na library real, sem assumir properties fixas do POC.
- A escrita será feita apenas nesta etapa.
- A validação por leitura MCP será executada depois.

```

---

## FILE: .github/skills/curar-aprendizado-de-jornada/SKILL.md

```md
---
name: curar-aprendizado-de-jornada
description: Registra feedback, erros, acertos e atualizações propostas da operação de jornada clusterizada.
---

# Curar Aprendizado de Jornada

## Arquivos desta skill

- [Feedback e revisões](./learning/feedback-e-revisoes.md)
- [Erros recorrentes](./learning/erros-recorrentes.md)
- [Acertos recorrentes](./learning/acertos-recorrentes.md)
- [Atualizações propostas](./learning/atualizacoes-propostas.md)

## Regra

Registre tudo o que vale repetir ou evitar entre etapas da jornada.

```

---

## FILE: .github/skills/curar-aprendizado-de-jornada/learning/acertos-recorrentes.md

```md
# Acertos Recorrentes

```md
### Acerto
- ID:
- Descrição:
- Etapa:
- Evidências:
- Regra que vale repetir:
- Status:
```

### Acerto
- ID: acerto-jornada-001
- Descrição: separar a leitura por conjuntos comparáveis evitou misturar cluster, estado e nível.
- Etapa: consentimento
- Evidências: fechado e aberto foram analisados separadamente antes do template.
- Regra que vale repetir: primeiro agrupar, depois analisar.
- Status: válido

### Acerto
- ID: acerto-jornada-002
- Descrição: só consolidar o template final depois que a library de tokens estiver conectada deixou clara a separação entre componente, token e conteúdo local.
- Etapa: consentimento
- Evidências: o template final foi revalidado após os binds estruturais da token library.
- Regra que vale repetir: template final só fecha depois da revisão da camada visual.
- Status: válido

```

---

## FILE: .github/skills/curar-aprendizado-de-jornada/learning/atualizacoes-propostas.md

```md
# Atualizações Propostas

```md
### Proposta
- ID:
- Motivo:
- Arquivo alvo:
- Mudança:
- Evidência:
- Risco:
- Status:
```

```

---

## FILE: .github/skills/curar-aprendizado-de-jornada/learning/erros-recorrentes.md

```md
# Erros Recorrentes

```md
### Erro
- ID:
- Descrição:
- Etapa:
- Evidências:
- Regra candidata:
- Status:
```

### Erro
- ID: erro-jornada-001
- Descrição: deixar mode explícito de cluster preso na variante-base do template quebra a separação entre cluster e estado.
- Etapa: consentimento
- Evidências: o cluster-5 contaminou a variante-base até o ajuste das instâncias de checagem.
- Regra candidata: mode por cluster deve ficar apenas em instâncias, nunca na base do template.
- Status: válido

```

---

## FILE: .github/skills/curar-aprendizado-de-jornada/learning/feedback-e-revisoes.md

```md
# Feedback e Revisões

```md
### Revisão
- ID:
- Etapa:
- Grupo:
- Feedback bruto:
- Evidência:
- Impacto:
- Próxima ação:
```

```

---

## FILE: .github/skills/desenhar-template-de-etapa/SKILL.md

```md
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

```

---

## FILE: .github/skills/desenhar-template-de-etapa/references/checklist-de-descoberta-antes-da-escrita.md

```md
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

```

---

## FILE: .github/skills/desenhar-template-de-etapa/references/reconectar-ao-design-system.md

```md
# Reconectar ao Design System

Use esta referência quando a etapa exigir que o template final seja reconstruído com base em libraries oficiais conectadas ao arquivo.

## Objetivo

Classificar cada bloco observado nas referências para decidir **como** ele deve entrar no padrão novo.

As quatro categorias são:

- `already-connected`
- `exact-swap`
- `compose-from-primitives`
- `blocked`

## O que cada categoria significa

### `already-connected`

Use quando:

- o bloco já é instância oficial da library conectada;
- ou a composição atual já é aceita como canônica pela operação.

Nessa categoria:

- não reconstrua o bloco do zero sem motivo;
- registre que o bloco já está saudável;
- valide apenas se a estrutura continua íntegra.

### `exact-swap`

Use quando:

- existe um componente oficial que substitui o bloco quase 1:1;
- a troca preserva função, estrutura e intenção do bloco.

Nessa categoria:

- prefira troca direta por instância oficial;
- confirme a variant correta antes de assumir o default;
- preserve overrides úteis apenas quando fizer sentido.

### `compose-from-primitives`

Use quando:

- não existe um componente único na library para aquele bloco;
- mas existem primitivas oficiais suficientes para reconstruí-lo.

Exemplos comuns:

- headers compostos;
- resumos financeiros;
- grupos de métricas;
- seções com item default + badge + CTA;
- blocos de módulos opcionais.

Nessa categoria:

- reconstrua o bloco do zero com instâncias oficiais menores;
- use tokens oficiais;
- evite wrappers locais improvisados.

### `blocked`

Use quando:

- a library não expõe o componente necessário;
- a equivalência oficial está ambígua demais;
- a referência é bespoke demais;
- a importação ou a conexão com a library falha;
- ainda falta contexto humano para decidir com segurança.

Nessa categoria:

- não force reconstrução ruim;
- sinalize claramente o bloqueio;
- diga o que falta para destravar.

## Ordem de decisão sem Code Connect

Neste repo, assuma que **não existe Code Connect** como pré-requisito.

Use esta ordem:

1. ler a referência com `get_metadata` e `get_design_context`
2. descobrir libraries oficiais conectadas com `get_libraries`
3. usar o inventário observado para procurar equivalentes com `search_design_system`
4. se necessário, usar `use_figma` read-only para distinguir:
   - instância remota
   - componente local
   - wrapper local
   - variant
   - propriedade observada
5. classificar o bloco em uma das quatro categorias

## Estratégia operacional de reconexão

- trabalhe uma seção por vez;
- não reescreva a tela inteira em um único write;
- valide cada seção depois da reconstrução;
- só avance para a próxima seção quando a anterior estiver estruturalmente íntegra.

## Variante correta, não default cego

Antes de usar uma instância oficial:

- olhe o naming do bloco original;
- olhe o contexto semântico do uso;
- olhe cues visuais relevantes da referência;
- compare com as variants disponíveis;
- escolha a mais próxima do uso real.

Se a família estiver certa, mas a variant estiver ambígua:

- registre a ambiguidade;
- não aplique o default sem sinalizar.

## Backup em operação destrutiva

Quando a etapa for de reconexão de uma tela já existente e houver risco de substituir ou remover estrutura:

- crie backup da tela ou do frame alvo antes da troca;
- faça isso em write separado;
- nomeie o backup com clareza.

Não trate backup como regra universal de qualquer write pequeno. Use quando a operação for destrutiva.

## Regra importante

Componente local copiado de outro arquivo:

- não é padrão oficial;
- não deve ser promovido automaticamente;
- serve como pista de naming, sintaxe e organização para buscar equivalente nas libraries conectadas.

## Saída esperada por bloco

Para cada bloco relevante, registre:

- nome funcional do bloco
- categoria:
  - `already-connected`
  - `exact-swap`
  - `compose-from-primitives`
  - `blocked`
- library oficial candidata
- componente ou primitives candidatas
- risco estrutural observado
- observações para reconstrução

```

---

## FILE: .github/skills/desenhar-template-de-etapa/references/regras-de-template.md

```md
# Regras de Template

- Escolha a estrutura dominante.
- Quando existir uma base canônica completa da tela, use essa base como ponto de partida do template e remova dela apenas o que for condicionado por boolean, modalidade, adicional ou estado.
- Se a modalidade mudar a composição relevante da tela, parta de uma base canônica por modalidade antes de parametrizar adicionais e estados.
- Decida quando a etapa precisa de mais de uma tela própria dentro do mesmo módulo.
- Preserve a ordem estrutural comum.
- Trate estado como variant.
- Prepare boolean apenas quando o template continuar saudável sem o bloco.
- Não assuma que o boolean será implementado por uma property específica do componente; isso depende da library real.
- Trate modalidade e adicionais como eixos de parametrização antes de criar outra tela sem necessidade.
- Se a seleção de um adicional alterar juros, totalizadores, resumos ou condições da própria tela, prefira modelar isso dentro dos blocos estruturais corretos antes de criar um card extra genérico.
- Considere a library de componentes e a library de tokens como fontes separadas.
- Reconstrua o template final do zero; não use clone do frame de referência como base do padrão final.
- Use o inventário de componentes observados nas referências como guia de busca dentro das libraries oficiais conectadas ao arquivo.
- Se a referência trouxer componentes locais copiados de outro arquivo, use o naming, a sintaxe e a organização deles para procurar equivalentes nas libraries oficiais conectadas.
- Só aceite componente local como evidência de análise; não o promova automaticamente para o template final.
- Classifique cada bloco relevante em `already-connected`, `exact-swap`, `compose-from-primitives` ou `blocked` antes de reconstruir.
- Reconecte uma seção por vez; não reescreva a tela inteira em um único write.
- Escolha a variant correta com base em semântica, contexto e cues visuais do bloco original; não use o default da library cegamente.
- Não misture conteúdo variável com estrutura base.
- Não deixe mode explícito preso nas variantes-base.
- Não aceite card com altura menor do que `conteúdo + padding`.
- Não aceite `component set` com variantes cortadas pelo bounding.

```

---

## FILE: .github/skills/jornada-consignado-clusterizado/SKILL.md

```md
---
name: jornada-consignado-clusterizado
description: Contexto operacional da jornada de consignado com etapas, módulos, telas, clusters, modalidades e adicionais reutilizado pelos agentes da operação.
---

# Jornada Consignado Clusterizado

Esta skill não cria nada sozinha.

Ela existe para dar contexto comum às etapas da jornada:

- consentimento
- simulacao
- revisao
- efetivacao

## Arquivos desta skill

- [Consentimento](./etapas/consentimento.md)
- [Simulação](./etapas/simulacao.md)
- [Revisão](./etapas/revisao.md)
- [Efetivação](./etapas/efetivacao.md)
- [Briefing de etapa](./templates/briefing-de-etapa.md)
- [Plano de agrupamento](./templates/plano-de-agrupamento.md)

## Regra

Quando uma nova etapa ou um novo caso entrar, tente primeiro preenchê-lo com este modelo antes de pensar em criar novo agente ou nova skill.

```

---

## FILE: .github/skills/jornada-consignado-clusterizado/etapas/consentimento.md

```md
# Etapa: Consentimento

## Objetivo

Explicar a consulta de dados, capturar a autorização e adaptar o conteúdo ao cluster.

## Padrões esperados

- títulos legais e operacionais por cluster
- accordions com detalhe expandido
- possíveis avisos adicionais por cluster
- estado aberto/fechado como variant

## Agrupamentos comuns

- tela base fechada
- tela base aberta
- outras telas do mesmo módulo quando existirem

```

---

## FILE: .github/skills/jornada-consignado-clusterizado/etapas/efetivacao.md

```md
# Etapa: Efetivação

## Objetivo

Concluir a jornada com aceite final, confirmação operacional e mensagens de conclusão.

## Padrões esperados

- confirmação final
- recibos ou resumos finais
- textos legais por cluster e modalidade
- possíveis blocos condicionais por produto contratado
- finais alternativos por cluster, como token, anuência externa ou conclusão direta

## Agrupamentos comuns

- `Efetivacao/Base`
- `Efetivacao/Token`
- `Efetivacao/Anuencia`
- `Efetivacao/Conclusao`

```

---

## FILE: .github/skills/jornada-consignado-clusterizado/etapas/revisao.md

```md
# Etapa: Revisão

## Objetivo

Conferir dados, condições e decisões antes da efetivação.

## Padrões esperados

- resumos de dados
- blocos de conferência
- mensagens de alerta e aceite
- detalhes do contrato com accordions
- informações importantes com itens condicionais por modalidade e adicionais
- bottom sheet normativo, como o caso da 4790
- diferenças de texto e de presença de bloco por cluster, modalidade e adicionais

## Agrupamentos comuns

- `Revisao/Base`
- `Revisao/DetalhesContrato`
- `Revisao/InformacoesImportantes`
- `Revisao/BottomSheet4790`

```

---

## FILE: .github/skills/jornada-consignado-clusterizado/etapas/simulacao.md

```md
# Etapa: Simulação

## Objetivo

Apresentar cenários, valores, condições e escolhas de simulação por cluster.

## Padrões esperados

- tela base de simulação
- blocos opcionais por elegibilidade
- módulos com layout próprio, como seguro e portabilidade de salário
- textos regulatórios por cluster, modalidade e produto quando necessário
- telas adicionais disparadas por clique, como editar valor, editar parcela ou rever coberturas
- totalizadores e resumos financeiros que podem mudar quando adicionais são selecionados

## Agrupamentos comuns

- `Simulacao/Base`
- `Simulacao/EditarValor`
- `Simulacao/EditarParcela`
- `Simulacao/SeguroPrestamista`
- `Simulacao/SeguroPrestamista/ReverCoberturas`
- `Simulacao/PortabilidadeSalario`

## Recorte mínimo recomendado para teste

Antes de escalar a etapa inteira, teste este recorte:

- `Simulacao/Base`
- `Simulacao/SeguroPrestamista`
- `Simulacao/SeguroPrestamista/ReverCoberturas`

Esse recorte já pressiona:

- composição variável na mesma tela-base;
- adicionais elegíveis vs selecionados;
- combinação de adicionais;
- separação entre `estado`, `adicional`, `modalidade` e `outra tela`.

## Variações mínimas para `Simulacao/Base`

Monte pelo menos estes frames para o agente analisar:

- `Simulacao/Base/PCON - Padrao`
- `Simulacao/Base/PCON - SeguroDesmarcado`
- `Simulacao/Base/PCON - SeguroSelecionado`
- `Simulacao/Base/PCON - PortabilidadeDesmarcada`
- `Simulacao/Base/PCON - PortabilidadeSelecionada`
- `Simulacao/Base/PCON - Seguro+Portabilidade`
- `Simulacao/Base/REFIN - Padrao`
- `Simulacao/Base/REFIN - SeguroDesmarcado`
- `Simulacao/Base/REFIN - SeguroSelecionado`
- `Simulacao/Base/REFIN - PortabilidadeDesmarcada`
- `Simulacao/Base/REFIN - PortabilidadeSelecionada`
- `Simulacao/Base/REFIN - Seguro+Portabilidade`

Regra de leitura para esse conjunto:

- `Padrao` não significa versão mínima.
- `Padrao` deve representar a base canônica mais completa da tela dentro da modalidade analisada.
- `PCON` e `REFIN` devem ser tratados como pontos de partida estruturais diferentes quando a composição da tela mudar por modalidade.
- as outras variações mostram o que some, muda ou cresce a partir da base completa da modalidade.

## Componentes mínimos esperados para o teste

- `Page/Simulacao/Base/PCON`
- `Page/Simulacao/Base/REFIN`
- `Page/Simulacao/SeguroPrestamista`
- `Page/Simulacao/SeguroPrestamista/ReverCoberturas`
- `Simulacao/ResumoDeValores`
- `Simulacao/ResumoDeParcelas`
- `Simulacao/ItemDeModulo`
- `Simulacao/BlocoDinheiroNaConta`
- `Simulacao/BlocoSaldoARefinanciar`
- `Simulacao/TotalizadorMensal`

Se o botão atual da library já servir, reutilize-o.

## Regras adicionais de leitura para a base

- `ResumoDeValores` pode concentrar valor solicitado, ação de editar valor, taxa de juros e resumo financeiro relacionado.
- `ResumoDeParcelas` pode concentrar quantidade de parcelas e ação de editar parcela.
- `TotalizadorMensal` deve ficar perto do CTA quando a tela exigir uma leitura consolidada do valor final por mês.
- Se seguro ou portabilidade alterarem juros, totais ou resumos, trate isso primeiro como mudança dentro desses blocos estruturais, não como card solto de contexto.

## Tokens adicionais mínimos

Não crie tokens novos sem necessidade.

Verifique primeiro se a token library atual já cobre:

- background
- text primary/secondary
- border subtle
- action primary
- spacing base
- radius base
- tamanhos mínimos

Só crie gaps reais.

```

---

## FILE: .github/skills/jornada-consignado-clusterizado/templates/briefing-de-etapa.md

```md
# Briefing de Etapa

```md
## Etapa
- Nome:
- Objetivo:

## Módulos da etapa
- Lista:

## Telas da etapa
- Lista:

## Convenção de nomeação dos frames
- `Padrao` significa:
- `ClusterN` significa:
- `Modalidade X` significa:
- nomes de módulos ou adicionais significam:

## Clusters cobertos
- Lista:

## Modalidades cobertas
- Lista:

## Adicionais ou produtos envolvidos
- Lista:

## Estados relevantes
- fechado:
- aberto:
- outros:

## Libraries conectadas
- componentes:
- tokens:

## Observações
- riscos:
- exceções:
- ambiguidades que o agente deve perguntar no chat:
```

```

---

## FILE: .github/skills/jornada-consignado-clusterizado/templates/plano-de-agrupamento.md

```md
# Plano de Agrupamento

```md
## Etapa
- Nome:

## Grupo 1
- Módulo:
- Tela:
- Frames de referência:
- Estado:
- Modalidade:
- Adicionais:
- Clusters:
- Convenção de nomeação observada:
- Objetivo da análise:

## Grupo 2
- Módulo:
- Tela:
- Frames de referência:
- Estado:
- Modalidade:
- Adicionais:
- Clusters:
- Convenção de nomeação observada:
- Objetivo da análise:

## Grupo 3
- Módulo:
- Tela:
- Frames de referência:
- Estado:
- Modalidade:
- Adicionais:
- Clusters:
- Convenção de nomeação observada:
- Objetivo da análise:
```

```

---

## FILE: .github/skills/normalizar-handoff-de-etapa/SKILL.md

```md
---
name: normalizar-handoff-de-etapa
description: Consolida análises de uma etapa em um relatório único pronto para template, parametrização e curadoria.
---

# Normalizar Handoff de Etapa

## Arquivos desta skill

- [Estrutura de relatório](./references/estrutura-de-relatorio.md)

## Objetivo

Transformar análises parciais em um handoff único, sem contradição e sem duplicação.

```

---

## FILE: .github/skills/normalizar-handoff-de-etapa/references/estrutura-de-relatorio.md

```md
# Estrutura de Relatório

## Etapa analisada
- Nome:
- Grupos avaliados:

## Estrutura dominante da etapa

## Diferenças por cluster

## Diferenças por estado

## Diferenças por modalidade e adicionais

## Template recomendado

## Estratégia por bloco
- already-connected
- exact-swap
- compose-from-primitives
- blocked

## Candidatos a string

## Candidatos a boolean

## Candidatos a variant

## Itens estruturais

## Pendências humanas

```

---

## FILE: .github/skills/operar-jornada-clusterizada/SKILL.md

```md
---
name: operar-jornada-clusterizada
description: Orquestra a operação de análise, template, parametrização e aprendizado para etapas de jornada com cluster, modalidade, adicionais, módulos e telas.
---

# Operar Jornada Clusterizada

Use esta skill para conduzir a operação de ponta a ponta sem criar um agente por tela.

## Arquivos desta skill

- [Modelo operacional](./references/modelo-operacional.md)
- [Eixos de variação](./references/eixos-de-variacao.md)
- [Disciplina de tools MCP](./references/disciplina-de-tools-mcp.md)
- [Tools and Prompts do Figma MCP](./references/tools-and-prompts-oficial-figma-mcp.md)
- [Orquestração multi-agent no VS Code](./references/orquestracao-multi-agent-vscode.md)
- [Regras de escalabilidade](./references/regras-de-escalabilidade.md)

## Ideia central

Escala não vem de criar um agente por página.

Escala vem de:

- poucos agentes por função;
- agrupamento correto das telas;
- contexto de etapa separado da lógica dos agentes;
- eixos de variação explícitos por etapa;
- escrita no Figma apenas no final.

```

---

## FILE: .github/skills/operar-jornada-clusterizada/references/disciplina-de-tools-mcp.md

```md
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

```

---

## FILE: .github/skills/operar-jornada-clusterizada/references/eixos-de-variacao.md

```md
# Eixos de Variação

Toda etapa deve ser lida com estes eixos explícitos:

- `etapa`
- `módulo`
- `tela`
- `estado`
- `cluster`
- `modalidade`
- `adicionais`

## Regra

Não trate tudo como cluster.

Antes de planejar template ou variável, classifique cada diferença em um destes eixos.

## Uso prático

- `cluster`: convênio, órgão, grupo operacional
- `modalidade`: novo, refinanciamento, portabilidade
- `adicionais`: seguro, portabilidade de salário, outros módulos opcionais
- `estado`: aberto, fechado, preenchido, selecionado, bottom sheet aberto
- `tela`: composição específica que abre dentro da mesma etapa
- `módulo`: assunto ou pacote funcional, como seguro, portabilidade, detalhes do contrato

```

---

## FILE: .github/skills/operar-jornada-clusterizada/references/modelo-operacional.md

```md
# Modelo Operacional

## Estrutura

- `agentes por função`
- `skills por função`
- `documentação por etapa da jornada`
- `contexto por módulo`
- `agrupamento de telas por conjunto comparável`

## Fluxo

1. Escolher a etapa da jornada.
2. Mapear módulos, telas e eixos de variação.
3. Montar os conjuntos comparáveis de telas, de preferência com links de frame e `node-id`.
4. Analisar cada conjunto.
5. Consolidar o handoff.
6. Decidir o template.
7. Planejar parametrização.
8. Escrever no Figma.
9. Curar o aprendizado.

## Fan-out recomendado

- um worker por conjunto comparável;
- se o conjunto for grande demais, um worker por frame ou subgrupo com o mesmo recorte semântico;
- consolidação sempre volta para um handoff único antes de qualquer escrita.

## Exemplos de conjunto comparável

- etapa `consentimento`, tela `base`, estado `fechado`, clusters `1-5`
- etapa `consentimento`, tela `base`, estado `aberto`, clusters `1-5`
- etapa `simulacao`, tela `base`, modalidade `refinanciamento`, com e sem adicionais
- etapa `revisao`, módulo `detalhes do contrato`, tela `acordeoes`, estado `aberto`

```

---

## FILE: .github/skills/operar-jornada-clusterizada/references/orquestracao-multi-agent-vscode.md

```md
# Orquestração Multi-Agent no VS Code

Referências oficiais:

- [Subagents in VS Code](https://code.visualstudio.com/docs/copilot/agents/subagents)
- [Custom agents in VS Code](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [Agents concepts](https://code.visualstudio.com/docs/copilot/concepts/agents)

## Objetivo

Adaptar a operação deste repo ao runtime real de **VS Code + GitHub Copilot custom agents**.

## Papéis

### Agente principal visível

Use um agente principal no picker:

- `operador-de-jornada`

Esse agente:

- recebe o pedido do usuário;
- entende a etapa;
- divide a tarefa;
- chama subagents quando contexto isolado ajudar;
- consolida o resultado final.

### Workers internos

Use como subagents:

- `analista-de-conjunto-de-telas`
- `normalizador-de-handoff-de-etapa`
- `desenhador-de-template-de-etapa`
- `planejador-de-parametrizacao-de-etapa`
- `criador-de-parametrizacao-de-etapa`
- `curador-de-aprendizado-de-jornada`

Esses agentes:

- não precisam aparecer no picker para o usuário;
- podem ficar com `user-invocable: false`;
- continuam podendo ser chamados programaticamente pelo agente principal.

## Regras de frontmatter

Para agents deste repo no VS Code:

- use `target: vscode`
- use `user-invocable: false` para workers internos
- use `disable-model-invocation: true` quando o agente só deve ser chamado manualmente pelo usuário
- deixe `disable-model-invocation` como `false` ou omitido para workers que podem ser chamados como subagent

## Ferramenta de subagent

Para permitir que o agente principal rode subagents, inclua a tool de subagent no agente orquestrador:

- `agent`

Quando o ambiente suportar a nomenclatura `runSubagent`, trate isso como capacidade equivalente do runtime. Neste repo, documente a intenção como uso de subagent pelo agente principal.

## Quando abrir subagent

Abra subagent quando:

- o conjunto comparável estiver isolado e puder ser analisado sem o resto da conversa;
- houver mais de um grupo comparável;
- houver mais de uma modalidade forte;
- houver necessidade de fan-out de leitura.

Não abra subagent quando:

- a tarefa for pequena demais;
- o ganho de isolamento não compensar;
- a etapa já estiver em escrita final pequena.

## Fan-out recomendado

### Leitura e análise

Pode usar fan-out:

- um worker por conjunto comparável;
- um worker por frame com `node-id`, quando necessário;
- um worker por modalidade, quando a modalidade muda a base estrutural.

### Escrita

Não paralelize escrita com `use_figma`.

Mesmo em ambiente com subagents:

- `use_figma` mutando canvas deve ser sequencial;
- um write por vez;
- validação depois de cada write.

## Handoff mínimo entre agents

Todo worker deve devolver:

- identificação do conjunto;
- conclusão do que é cluster, modalidade, adicional, estado e tela;
- inventário MCP do que foi observado;
- estratégia por bloco;
- riscos e dúvidas.

O normalizador:

- reconcilia divergências;
- sobe um relatório único;
- prepara a entrada do desenhador e do planejador.

## Regra de contexto

Prefira passar ao subagent:

- link de frame com `node-id`
- etapa
- módulo
- tela
- modalidade, se já souber
- objetivo da subtarefa

Evite passar:

- o arquivo inteiro sem recorte
- histórico irrelevante
- vários grupos diferentes no mesmo subagent

## Nested subagents

Por padrão, não dependa de nesting profundo.

Modele a operação como:

- `operador-de-jornada` chama workers
- workers devolvem resultado
- `operador-de-jornada` consolida ou passa ao próximo worker

Só use nesting adicional se o ambiente do VS Code estiver com suporte e configuração apropriados.

```

---

## FILE: .github/skills/operar-jornada-clusterizada/references/regras-de-escalabilidade.md

```md
# Regras de Escalabilidade

- Não crie um agente por tela.
- Não crie uma skill por tela.
- Não misture cluster, estado e nível no mesmo grupo de análise.
- Crie contexto por etapa da jornada, não por arquivo inteiro sem recorte.
- Reuse o mesmo pipeline para `consentimento`, `simulacao`, `revisao` e `efetivacao`.
- Só crie novos artefatos específicos quando uma etapa realmente exigir regra diferente.
- Prefira fan-out por grupo comparável ou frame com `node-id`, não por “tela fixa” como papel permanente.

## O que pode variar sem mudar a arquitetura

- quantidade de clusters
- quantidade de níveis
- quantidade de estados por nível
- quantidade de telas por etapa

## O que não deve variar

- separação entre leitura, decisão e escrita
- uso de modes apenas para cluster
- uso de variants apenas para estado/interação

```

---

## FILE: .github/skills/operar-jornada-clusterizada/references/tools-and-prompts-oficial-figma-mcp.md

```md
# Tools and Prompts do Figma MCP

Referência operacional baseada na documentação oficial:

- [Figma MCP Server: Tools and prompts](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)

Use este arquivo para decidir **qual tool MCP usar** e **em que momento do fluxo**.

## Regra geral

- prefira `get_design_context` como leitura principal do design;
- use `get_metadata` como leitura mais leve quando precisar primeiro de árvore, nomes, tipos, posições e tamanhos;
- use `get_libraries` e `search_design_system` antes de recriar qualquer coisa do design system;
- use `get_variable_defs` para entender tokens, styles e variables já aplicadas;
- use `use_figma` como tool geral de escrita e inspeção programática mais fina;
- use `whoami` quando houver dúvida de autenticação, plano, seat ou permissão.

## Mapa de uso por tool

### `get_design_context`

Use quando:

- precisar entender a composição real de um frame ou camada;
- precisar ler estrutura, textos, blocos, instâncias e relações visuais;
- for a leitura principal antes da análise ou reconstrução.

Não use como primeira opção quando:

- o frame for muito grande e você ainda não souber onde focar.

Nesse caso:

- use `get_metadata` primeiro;
- depois faça `get_design_context` só nos nós relevantes.

### `get_metadata`

Use quando:

- precisar de uma leitura leve da árvore;
- quiser descobrir páginas ou nós antes de aprofundar;
- estiver lidando com designs grandes e quiser reduzir contexto;
- quiser confirmar dimensões, tipos, posições e hierarquia;
- quiser checar rapidamente se a composição cresceu, se a altura mudou ou se há sinais de bounding quebrado.

Não pare no `get_metadata` quando a tarefa exigir implementação ou análise fina da composição.

### `get_libraries`

Use quando:

- precisar saber quais libraries oficiais estão conectadas no arquivo;
- quiser distinguir library já conectada de library só disponível para adicionar;
- for procurar equivalentes oficiais para componentes locais encontrados nas referências.

Essa tool deve vir antes de `search_design_system` quando o objetivo for reconstrução com design system oficial.

### `search_design_system`

Use quando:

- quiser procurar componentes, variables ou styles existentes;
- tiver coletado nomes úteis a partir das referências e quiser buscar equivalentes oficiais;
- precisar evitar recriação manual de componente já existente.

Use junto com:

- `get_libraries`, para delimitar o universo oficial;
- `get_design_context`, para saber o que procurar.

### `get_variable_defs`

Use quando:

- precisar entender quais tokens, variables e styles já estão aplicados num nó;
- quiser validar se o template já está bindado corretamente;
- quiser planejar parametrização sem escrever ainda.

### `get_screenshot`

Use quando:

- o ambiente permitir imagem;
- a tarefa exigir validação visual de fidelidade, clipping, spacing ou hierarquia visual.

No ambiente corporativo com restrição de circulação de imagem:

- não dependa dessa tool;
- substitua a validação visual por leitura estrutural com `get_design_context`, `get_metadata` e inspeção programática via `use_figma` read-only.

### `use_figma`

Use quando:

- precisar criar, editar ou remover nós;
- precisar construir templates, componentes, variants, variables, styles ou bindings;
- precisar de inspeção programática mais precisa do arquivo, além do que as tools de leitura devolvem;
- precisar confirmar detalhes como:
  - instâncias vs componentes locais;
  - `mainComponent`;
  - variants;
  - properties;
  - bounding;
  - sizing modes;
  - conteúdo + padding vs altura real.

No fluxo deste repo:

- leitura e decisão primeiro;
- escrita com `use_figma` só no momento final e de forma explícita;
- se `use_figma` for usado em leitura, faça isso só quando `get_design_context` e `get_metadata` não bastarem.

### `whoami`

Use quando:

- houver erro de permissão;
- houver dúvida sobre qual conta Figma está autenticada;
- for necessário entender plano, organização ou tipo de seat.

### `create_new_file`

Use quando:

- for necessário criar um arquivo novo de design, FigJam ou Slides.

No contexto deste repo:

- só use quando a operação realmente exigir um arquivo novo;
- não use para contornar problema de modelagem num arquivo que já existe.

### `generate_diagram`

Use quando:

- o usuário pedir diagrama em FigJam;
- o objetivo for fluxograma, sequência, gantt, state diagram, arquitetura ou ERD.

Não use para construir telas de produto.

### `generate_figma_design`

Use quando:

- o objetivo for capturar layout de uma interface web para Figma pela primeira vez;
- você estiver fazendo um fluxo de code-to-canvas.

Não é a tool principal deste repo para reconstrução de templates de jornada a partir de telas existentes.

### `get_figjam`

Use apenas em FigJam.

### `upload_assets`

Use quando:

- precisar subir imagem ou asset para o arquivo;
- quiser aplicar imagem a um nó ou criar frames com asset.

### Code Connect tools

- `get_code_connect_map`
- `add_code_connect_map`
- `get_context_for_code_connect`
- `send_code_connect_mappings`

Use quando o fluxo for de Code Connect.

Não são tools centrais da operação de análise de jornadas, exceto quando o objetivo for reconciliar Figma com componentes de código via Code Connect.

## Ordem preferida por tipo de trabalho

### Analisar telas comparáveis

1. `get_metadata`
2. `get_design_context`
3. `get_libraries`
4. `search_design_system`
5. `use_figma` read-only, se necessário

### Reconstruir template com design system oficial

1. `get_libraries`
2. `search_design_system`
3. `get_design_context` nas referências
4. `get_variable_defs`, se precisar validar binds/tokens
5. `use_figma` para escrita final

### Planejar parametrização

1. `get_design_context`
2. `get_variable_defs`
3. `get_libraries`
4. `search_design_system`, se houver dúvida sobre componente/property oficial

### Criar parametrização

1. validar que análise e plano já estão fechados
2. `use_figma` para criar collections, modes, variables, bindings e ajustes finais

## Regra de ouro deste repo

- não misture análise com escrita;
- não recrie design system antes de procurar nas libraries oficiais;
- não trate `get_metadata` como substituto de `get_design_context`;
- não trate `use_figma` como primeira tool de descoberta quando uma tool de leitura oficial resolver;
- não dependa de screenshot em ambientes corporativos onde imagem não pode circular.

```

---

## FILE: .github/skills/planejar-parametrizacao-de-etapa/SKILL.md

```md
---
name: planejar-parametrizacao-de-etapa
description: Converte o template decidido em plano explícito de modes, strings, booleans, variants e limites.
---

# Planejar Parametrização de Etapa

## Arquivos desta skill

- [Regras de modelagem](./references/regras-de-modelagem.md)
- [Contrato de saída](./references/contrato-de-saida.md)
- [Exemplo de consentimento](./artefatos/exemplos/consentimento-poc-001.md)

## Objetivo

Produzir um plano que o agente criador consiga executar sem reinterpretar a análise.

## Regra adicional

Collections não servem só para texto.

Elas podem concentrar:

- strings
- booleans
- números
- outras variables locais necessárias ao domínio

```

---

## FILE: .github/skills/planejar-parametrizacao-de-etapa/artefatos/exemplos/consentimento-poc-001.md

```md
# Exemplo: Consentimento POC 001

## Collection local proposta
- `consentimento-clusters`

## Modes
- `cluster-1`
- `cluster-2`
- `cluster-3`
- `cluster-4`
- `cluster-5`

## Template confirmado
- `Page/Consentimento/Base`
- variants:
  - `State=Fechado`
  - `State=Aberto`

## Strings do exemplo
- `consentimento/title`
- `consentimento/subtitle`
- `consentimento/notice/title`
- `consentimento/notice/body`
- `consentimento/accordion-1/title`
- `consentimento/accordion-1/body`
- `consentimento/accordion-2/title`
- `consentimento/accordion-2/body`
- `consentimento/cta/label`

## Booleans do exemplo
- `consentimento/visibility/notice`
- `consentimento/visibility/accordion-2`

## Aprendizado chave
- o template-base não deve receber mode explícito por cluster
- modes por cluster devem ficar nas instâncias
- `cluster` continua no mode
- `aberto/fechado` continua em variant
- booleans do POC foram bindados em `visible`, mas a library final pode expor esse controle por outro caminho estrutural
- a skill não deve assumir nomes fixos de properties ou camadas da library de componentes

```

---

## FILE: .github/skills/planejar-parametrizacao-de-etapa/artefatos/exemplos/simulacao-base-poc-001.md

```md
# Exemplo: Simulação Base POC 001

## Objetivo do teste

Validar se o pipeline entende que `Simulacao/Base` precisa partir de uma base canônica por modalidade e continua sendo a mesma tela dentro de cada modalidade quando:

- seguro aparece ou some;
- seguro está desmarcado ou selecionado;
- portabilidade aparece ou some;
- portabilidade está desmarcada ou selecionada;
- seguro e portabilidade coexistem;
- a composição cresce por seleção de adicional.

## Frames mínimos

- `Simulacao/Base/PCON - Padrao`
- `Simulacao/Base/PCON - SeguroDesmarcado`
- `Simulacao/Base/PCON - SeguroSelecionado`
- `Simulacao/Base/PCON - PortabilidadeDesmarcada`
- `Simulacao/Base/PCON - PortabilidadeSelecionada`
- `Simulacao/Base/PCON - Seguro+Portabilidade`
- `Simulacao/Base/REFIN - Padrao`
- `Simulacao/Base/REFIN - SeguroDesmarcado`
- `Simulacao/Base/REFIN - SeguroSelecionado`
- `Simulacao/Base/REFIN - PortabilidadeDesmarcada`
- `Simulacao/Base/REFIN - PortabilidadeSelecionada`
- `Simulacao/Base/REFIN - Seguro+Portabilidade`

## Templates esperados

- `Page/Simulacao/Base/PCON`
- `Page/Simulacao/Base/REFIN`
- `Page/Simulacao/SeguroPrestamista`
- `Page/Simulacao/SeguroPrestamista/ReverCoberturas`

## Componentes mínimos

- `Simulacao/ResumoDeValores`
- `Simulacao/ResumoDeParcelas`
- `Simulacao/ItemDeModulo`
- `Simulacao/BlocoDinheiroNaConta`
- `Simulacao/BlocoSaldoARefinanciar`
- `Simulacao/TotalizadorMensal`

## Regras de interpretação

- os frames compartilham o prefixo `Simulacao/Base`, mas devem ser separados primeiro por modalidade
- `PCON` e `REFIN` indicam bases canônicas diferentes
- dentro de cada modalidade, os sufixos indicam variações deliberadas da mesma tela
- `Padrao` indica base canônica mais completa da modalidade, não base mínima
- `SeguroDesmarcado` e `SeguroSelecionado` não indicam novas telas
- `PortabilidadeDesmarcada` e `PortabilidadeSelecionada` não indicam novas telas
- `Seguro+Portabilidade` continua sendo a mesma tela-base com composição combinada
- as demais variações devem ser lidas como redução, expansão ou alteração localizada da base completa da modalidade
- quando seguro ou portabilidade alterarem juros, totais ou resumos, o agente deve preferir manter isso nos blocos financeiros existentes da tela

## O que o agente deve descobrir

- o que fica fixo no template-base
- o que vira boolean
- o que vira variável de conteúdo
- o que vira variant ou property
- o que precisa abrir `Simulacao/SeguroPrestamista`
- o que precisa abrir `Simulacao/SeguroPrestamista/ReverCoberturas`
- como juros, total mensal e resumos financeiros reagem a modalidade e adicionais sem criar cards genéricos desnecessários

## Tokens adicionais mínimos

Use a token library atual primeiro.

Só crie tokens novos se faltar algo estrutural para a simulação, por exemplo:

- feedback informativo específico
- espaçamento intermediário ainda não coberto
- tamanho específico de item clicável

## Aprendizado esperado

- diferença estrutural lida por `get_metadata` ou `get_design_context` não significa automaticamente outra tela
- quando a modalidade mudar a composição relevante da tela, o agente deve partir de uma base canônica por modalidade
- quando o nome do frame e a composição apontam para o mesmo prefixo de tela dentro da modalidade, o agente deve tratar isso como variação deliberada da mesma tela
- `cluster` só entra como `mode` quando houver variação real por cluster
- resumos e totalizadores financeiros são parte estrutural da tela-base quando aparecem de forma recorrente

```

---

## FILE: .github/skills/planejar-parametrizacao-de-etapa/references/contrato-de-saida.md

```md
# Contrato de Saída

## Collection local proposta
- tipo:
- domínio:

## Modes por cluster

## Strings candidatas
- chave
- bloco
- valor por cluster

## Booleans candidatas
- chave
- bloco
- valor por cluster

## Outras variables candidatas
- chave
- tipo
- bloco
- motivo

## Variants mantidas

## Itens que não devem virar variável

## Bloqueios

## Prontidão para criação

```

---

## FILE: .github/skills/planejar-parametrizacao-de-etapa/references/regras-de-modelagem.md

```md
# Regras de Modelagem

- `mode` é reservado para cluster.
- `variant` é reservado para estado/interação.
- `string` é reservada para conteúdo textual que mantém a mesma função.
- `boolean` é reservada para presença/ausência de bloco sem quebrar o template.
- `number` é reservada para parâmetros locais que precisem ser editáveis e reutilizáveis.
- Tokens visuais vêm da library de tokens, não da collection local de conteúdo.
- Collections locais podem ser por etapa, por módulo ou por domínio de conteúdo.
- Variables locais servem para conteúdo, regras de presença e outros parâmetros reutilizáveis.
- A implementação do boolean pode acontecer por `visible` ou por outro vínculo estrutural compatível com a library real.
- Se um módulo tem layout próprio e conteúdo próprio, ele pode ter template próprio e collection própria.

```

