# Agrupamento de Telas

## Regra

Agrupe por conjunto comparável.

## Heurística de nomeação

- prefira sempre links de frame com `node-id`, não links genéricos do arquivo, quando for passar contexto operacional ao agente;
- `Etapa/Tela - ClusterN` indica suspeita forte de variação por cluster.
- `Etapa/Tela - Padrao` indica suspeita forte de base canônica comum; quando o contexto mostrar mais de uma possibilidade interna da mesma tela, trate `Padrao` como versão mais completa, não como versão mínima.
- `Etapa/Tela - Modalidade X` indica suspeita de variação por modalidade.
- `Etapa/Tela - Seguro`, `Etapa/Tela - Portabilidade` e nomes equivalentes indicam suspeita de módulo ou adicional.
- A nomeação orienta a leitura inicial, mas o agente deve confirmar no chat quando houver risco de interpretação errada.

## Ordem sugerida

1. mesma etapa
2. mesmo módulo
3. mesma tela
4. mesmo estado
5. mesma modalidade quando necessário
6. mesma combinação de adicionais quando necessário
7. clusters diferentes

## Exemplos corretos

- `consentimento / base / fechado / clusters 1-5`
- `consentimento / base / aberto / clusters 1-5`
- `simulacao/base/pcon - padrao`
- `simulacao/base/refin - padrao`
- `simulacao/base/pcon - seguroselecionado`
- `simulacao / base / modalidade refinanciamento / sem adicionais`
- `simulacao / seguro-prestamista / rever-coberturas / estado aberto`
- `revisao / detalhes-do-contrato / acordeoes / modalidade portabilidade`

## Exemplos errados

- misturar telas diferentes do mesmo módulo sem objetivo claro
- misturar aberto e fechado sem separar o objetivo
- misturar modalidades diferentes quando isso afeta a estrutura ou a composição da tela
- misturar casos com e sem adicionais quando isso muda a composição
- misturar consentimento com simulação
