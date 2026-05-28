# Reconectar ao Design System

Use esta referência quando a etapa exigir que o template final seja reconstruído com base em libraries oficiais conectadas ao arquivo.

## Objetivo

Classificar cada bloco observado nas referências para decidir **como** ele deve entrar no padrão novo.

As quatro categorias são:

- `already-connected`
- `exact-swap`
- `compose-from-primitives`
- `blocked`

## O que cada categoria significa

### `already-connected`

Use quando:

- o bloco já é instância oficial da library conectada;
- ou a composição atual já é aceita como canônica pela operação.

Nessa categoria:

- não reconstrua o bloco do zero sem motivo;
- registre que o bloco já está saudável;
- valide apenas se a estrutura continua íntegra.

### `exact-swap`

Use quando:

- existe um componente oficial que substitui o bloco quase 1:1;
- a troca preserva função, estrutura e intenção do bloco.

Nessa categoria:

- prefira troca direta por instância oficial;
- confirme a variant correta antes de assumir o default;
- preserve overrides úteis apenas quando fizer sentido.

### `compose-from-primitives`

Use quando:

- não existe um componente único na library para aquele bloco;
- mas existem primitivas oficiais suficientes para reconstruí-lo.

Exemplos comuns:

- headers compostos;
- resumos financeiros;
- grupos de métricas;
- seções com item default + badge + CTA;
- blocos de módulos opcionais.

Nessa categoria:

- reconstrua o bloco do zero com instâncias oficiais menores;
- use tokens oficiais;
- evite wrappers locais improvisados.

### `blocked`

Use quando:

- a library não expõe o componente necessário;
- a equivalência oficial está ambígua demais;
- a referência é bespoke demais;
- a importação ou a conexão com a library falha;
- ainda falta contexto humano para decidir com segurança.

Nessa categoria:

- não force reconstrução ruim;
- sinalize claramente o bloqueio;
- diga o que falta para destravar.

## Ordem de decisão sem Code Connect

Neste repo, assuma que **não existe Code Connect** como pré-requisito.

Use esta ordem:

1. ler a referência com `get_metadata` e `get_design_context`
2. descobrir libraries oficiais conectadas com `get_libraries`
3. usar o inventário observado para procurar equivalentes com `search_design_system`
4. se necessário, usar `use_figma` read-only para distinguir:
   - instância remota
   - componente local
   - wrapper local
   - variant
   - propriedade observada
5. classificar o bloco em uma das quatro categorias

## Estratégia operacional de reconexão

- trabalhe uma seção por vez;
- não reescreva a tela inteira em um único write;
- valide cada seção depois da reconstrução;
- só avance para a próxima seção quando a anterior estiver estruturalmente íntegra.

## Variante correta, não default cego

Antes de usar uma instância oficial:

- olhe o naming do bloco original;
- olhe o contexto semântico do uso;
- olhe cues visuais relevantes da referência;
- compare com as variants disponíveis;
- escolha a mais próxima do uso real.

Se a família estiver certa, mas a variant estiver ambígua:

- registre a ambiguidade;
- não aplique o default sem sinalizar.

## Backup em operação destrutiva

Quando a etapa for de reconexão de uma tela já existente e houver risco de substituir ou remover estrutura:

- crie backup da tela ou do frame alvo antes da troca;
- faça isso em write separado;
- nomeie o backup com clareza.

Não trate backup como regra universal de qualquer write pequeno. Use quando a operação for destrutiva.

## Regra importante

Componente local copiado de outro arquivo:

- não é padrão oficial;
- não deve ser promovido automaticamente;
- serve como pista de naming, sintaxe e organização para buscar equivalente nas libraries conectadas.

## Saída esperada por bloco

Para cada bloco relevante, registre:

- nome funcional do bloco
- categoria:
  - `already-connected`
  - `exact-swap`
  - `compose-from-primitives`
  - `blocked`
- library oficial candidata
- componente ou primitives candidatas
- risco estrutural observado
- observações para reconstrução
