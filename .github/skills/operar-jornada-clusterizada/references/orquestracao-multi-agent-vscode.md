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
