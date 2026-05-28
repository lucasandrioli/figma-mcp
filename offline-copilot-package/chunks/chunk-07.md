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

