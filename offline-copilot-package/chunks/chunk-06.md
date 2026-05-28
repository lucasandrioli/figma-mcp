===== FILE: .github/skills/operar-jornada-clusterizada/references/modelo-operacional.md =====
# Modelo Operacional

## Estrutura

- `agentes por função`
- `skills por função`
- `documentação por etapa da jornada`
- `contexto por módulo`
- `agrupamento de telas por conjunto comparável`
- `um mesmo arquivo pode servir como referência, construção e library final`

## Fluxo

1. Escolher a etapa da jornada.
2. Confirmar se o mesmo arquivo será usado como:
   - referência
   - construção
   - library final
3. Mapear páginas de referência e páginas de escrita dentro desse arquivo.
4. Mapear módulos, telas e eixos de variação.
5. Montar os conjuntos comparáveis de telas, de preferência com links de frame e `node-id`.
6. Analisar cada conjunto.
7. Consolidar o handoff.
8. Decidir o template.
9. Planejar parametrização.
10. Escrever no Figma.
11. Curar o aprendizado.

## Regra de páginas

- páginas de referência servem como evidência visual e estrutural;
- páginas de referência não são o destino do padrão final;
- páginas de escrita devem ser explicitadas, por exemplo:
  - `Components`
  - `Templates`
  - `Checks`
  - ou outra página de trabalho indicada pelo usuário;
- o template final, as variables e os checks podem nascer no mesmo arquivo que contém as referências, desde que em páginas separadas.

## Fan-out recomendado

- um worker por conjunto comparável;
- se o conjunto for grande demais, um worker por frame ou subgrupo com o mesmo recorte semântico;
- consolidação sempre volta para um handoff único antes de qualquer escrita.

## Exemplos de conjunto comparável

- etapa `consentimento`, tela `base`, estado `fechado`, clusters `1-5`
- etapa `consentimento`, tela `base`, estado `aberto`, clusters `1-5`
- etapa `simulacao`, tela `base`, modalidade `refinanciamento`, com e sem adicionais
- etapa `revisao`, módulo `detalhes do contrato`, tela `acordeoes`, estado `aberto`

===== END FILE =====

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

