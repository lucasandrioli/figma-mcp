===== FILE: .github/skills/jornada-consignado-clusterizado/etapas/simulacao.md =====
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

===== END FILE =====

===== FILE: .github/skills/jornada-consignado-clusterizado/templates/briefing-de-etapa.md =====
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

===== END FILE =====

===== FILE: .github/skills/jornada-consignado-clusterizado/templates/plano-de-agrupamento.md =====
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

===== END FILE =====

===== FILE: .github/skills/normalizar-handoff-de-etapa/SKILL.md =====
---
name: normalizar-handoff-de-etapa
description: Consolida análises de uma etapa em um relatório único pronto para template, parametrização e curadoria.
---

# Normalizar Handoff de Etapa

## Arquivos desta skill

- [Estrutura de relatório](./references/estrutura-de-relatorio.md)

## Objetivo

Transformar análises parciais em um handoff único, sem contradição e sem duplicação.

===== END FILE =====

===== FILE: .github/skills/normalizar-handoff-de-etapa/references/estrutura-de-relatorio.md =====
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

===== END FILE =====

===== FILE: .github/skills/operar-jornada-clusterizada/SKILL.md =====
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

===== END FILE =====

===== FILE: .github/skills/operar-jornada-clusterizada/references/disciplina-de-tools-mcp.md =====
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

===== END FILE =====

===== FILE: .github/skills/operar-jornada-clusterizada/references/eixos-de-variacao.md =====
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

===== END FILE =====

===== FILE: .github/skills/operar-jornada-clusterizada/references/modelo-operacional.md =====
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

===== END FILE =====

