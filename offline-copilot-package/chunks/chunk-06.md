===== FILE: .github/skills/operar-jornada-clusterizada/references/orquestracao-multi-agent-vscode.md =====
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

===== END FILE =====

===== FILE: .github/skills/operar-jornada-clusterizada/references/regras-de-escalabilidade.md =====
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

===== END FILE =====

===== FILE: .github/skills/operar-jornada-clusterizada/references/tools-and-prompts-oficial-figma-mcp.md =====
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

===== END FILE =====

