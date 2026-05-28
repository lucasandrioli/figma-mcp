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
