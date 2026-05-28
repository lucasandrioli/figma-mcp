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
