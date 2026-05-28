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
