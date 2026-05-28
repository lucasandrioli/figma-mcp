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

