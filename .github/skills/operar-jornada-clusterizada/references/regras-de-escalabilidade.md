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
