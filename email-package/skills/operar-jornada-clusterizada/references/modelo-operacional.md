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
