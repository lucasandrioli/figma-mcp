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

===== FILE: .github/skills/planejar-parametrizacao-de-etapa/SKILL.md =====
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

===== END FILE =====

===== FILE: .github/skills/planejar-parametrizacao-de-etapa/artefatos/exemplos/consentimento-poc-001.md =====
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

===== END FILE =====

