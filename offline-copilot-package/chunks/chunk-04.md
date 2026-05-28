===== FILE: .github/skills/desenhar-template-de-etapa/SKILL.md =====
---
name: desenhar-template-de-etapa
description: Decide ou ajusta o template reutilizável de uma etapa da jornada a partir do relatório consolidado.
---

# Desenhar Template de Etapa

## Arquivos desta skill

- [Regras de template](./references/regras-de-template.md)
- [Reconectar ao design system](./references/reconectar-ao-design-system.md)
- [Checklist de descoberta antes da escrita](./references/checklist-de-descoberta-antes-da-escrita.md)
- [Tools and Prompts do Figma MCP](../operar-jornada-clusterizada/references/tools-and-prompts-oficial-figma-mcp.md)

## Objetivo

Sair do diagnóstico e chegar a um template de etapa que suporte a maior cobertura possível sem ficar parametrizado demais.

## Disciplina de construção

- construa ou ajuste o template em passos pequenos;
- depois de cada componente ou template criado, valide estrutura antes de seguir;
- confirme com leitura estrutural se altura, padding, hug/fill e bounding continuam coerentes;
- se a referência estiver quebrada, use-a como evidência de negócio, não como modelo de construção.
- antes de escrever algo novo, confirme por `get_libraries` e `search_design_system` se a library oficial já oferece o componente, token ou style necessário.
- não faça `use_figma` mutando canvas antes de passar pelo checklist de descoberta.

## Regra de reconstrução

O material de referência serve para:

- entender estrutura;
- entender variações;
- identificar componentes usados;
- detectar defeitos estruturais.

O template final não deve nascer por clone do frame analisado.

Se o mesmo arquivo for ao mesmo tempo:

- referência
- construção
- library final

então:

- leia nas páginas de referência;
- escreva apenas nas páginas de construção;
- não trate os frames colados como destino do padrão final.

Ele deve ser reconstruído do zero usando:

- instâncias das libraries oficiais conectadas ao arquivo;
- tokens da library oficial de tokens;
- inventário de componentes observado nas referências como pista de busca.
- classificação por bloco em:
  - `already-connected`
  - `exact-swap`
  - `compose-from-primitives`
  - `blocked`

## Validação mínima antes de aceitar um componente ou template

- o conteúdo cabe com respiro real dentro do container;
- a altura do container comporta `conteúdo + padding`;
- textos variáveis não ficam presos em alturas fixas frágeis;
- o `component set` engloba todas as variantes sem corte;
- a composição cresce por `HUG` quando o conteúdo cresce;
- alterações de adicionais selecionados entram primeiro nos blocos corretos da tela, antes de virar card extra genérico.

===== END FILE =====

===== FILE: .github/skills/desenhar-template-de-etapa/references/checklist-de-descoberta-antes-da-escrita.md =====
# Checklist de Descoberta Antes da Escrita

Use este checklist antes de qualquer `use_figma` que vá mutar canvas.

## Hard gates

É proibido escrever no Figma antes de confirmar:

- qual é a etapa;
- qual é o módulo;
- qual é a tela;
- qual é o conjunto comparável que está sendo tratado;
- quais são os eixos de variação relevantes:
  - cluster
  - modalidade
  - adicionais
  - estado
- quais libraries oficiais estão conectadas;
- quais componentes equivalentes já existem ou não;
- qual estratégia cada bloco pede:
  - `already-connected`
  - `exact-swap`
  - `compose-from-primitives`
  - `blocked`

## Checklist mínimo

Antes de escrever, confirme explicitamente:

- `get_metadata` foi usado para leitura leve da árvore quando necessário;
- `get_design_context` foi usado para entender a composição do que será reconstruído;
- `get_libraries` foi usado para descobrir o universo oficial disponível;
- `search_design_system` foi usado antes de recriar componente oficial do zero;
- o inventário de instâncias e componentes locais foi capturado;
- a variant correta foi decidida por semântica e contexto, não por default cego;
- o write será pequeno e localizado;
- a validação pós-write já está prevista.

## Regra de bloqueio

Se algum desses itens estiver em aberto:

- não escreva;
- registre a pendência;
- continue a descoberta ou peça confirmação humana curta no chat.

===== END FILE =====

===== FILE: .github/skills/desenhar-template-de-etapa/references/reconectar-ao-design-system.md =====
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

===== END FILE =====

===== FILE: .github/skills/desenhar-template-de-etapa/references/regras-de-template.md =====
# Regras de Template

- Escolha a estrutura dominante.
- Quando existir uma base canônica completa da tela, use essa base como ponto de partida do template e remova dela apenas o que for condicionado por boolean, modalidade, adicional ou estado.
- Se a modalidade mudar a composição relevante da tela, parta de uma base canônica por modalidade antes de parametrizar adicionais e estados.
- Decida quando a etapa precisa de mais de uma tela própria dentro do mesmo módulo.
- Preserve a ordem estrutural comum.
- Trate estado como variant.
- Prepare boolean apenas quando o template continuar saudável sem o bloco.
- Não assuma que o boolean será implementado por uma property específica do componente; isso depende da library real.
- Trate modalidade e adicionais como eixos de parametrização antes de criar outra tela sem necessidade.
- Se a seleção de um adicional alterar juros, totalizadores, resumos ou condições da própria tela, prefira modelar isso dentro dos blocos estruturais corretos antes de criar um card extra genérico.
- Considere a library de componentes e a library de tokens como fontes separadas.
- Reconstrua o template final do zero; não use clone do frame de referência como base do padrão final.
- Se o arquivo atual também for a library final do domínio, mantenha a leitura nas páginas de referência e a escrita nas páginas de `Components`, `Templates`, `Checks` ou equivalentes indicadas pelo usuário.
- Use o inventário de componentes observados nas referências como guia de busca dentro das libraries oficiais conectadas ao arquivo.
- Se a referência trouxer componentes locais copiados de outro arquivo, use o naming, a sintaxe e a organização deles para procurar equivalentes nas libraries oficiais conectadas.
- Só aceite componente local como evidência de análise; não o promova automaticamente para o template final.
- Classifique cada bloco relevante em `already-connected`, `exact-swap`, `compose-from-primitives` ou `blocked` antes de reconstruir.
- Reconecte uma seção por vez; não reescreva a tela inteira em um único write.
- Escolha a variant correta com base em semântica, contexto e cues visuais do bloco original; não use o default da library cegamente.
- Não misture conteúdo variável com estrutura base.
- Não deixe mode explícito preso nas variantes-base.
- Não aceite card com altura menor do que `conteúdo + padding`.
- Não aceite `component set` com variantes cortadas pelo bounding.

===== END FILE =====

===== FILE: .github/skills/jornada-consignado-clusterizado/SKILL.md =====
---
name: jornada-consignado-clusterizado
description: Contexto operacional da jornada de consignado com etapas, módulos, telas, clusters, modalidades e adicionais reutilizado pelos agentes da operação.
---

# Jornada Consignado Clusterizado

Esta skill não cria nada sozinha.

Ela existe para dar contexto comum às etapas da jornada:

- consentimento
- simulacao
- revisao
- efetivacao

## Arquivos desta skill

- [Consentimento](./etapas/consentimento.md)
- [Simulação](./etapas/simulacao.md)
- [Revisão](./etapas/revisao.md)
- [Efetivação](./etapas/efetivacao.md)
- [Briefing de etapa](./templates/briefing-de-etapa.md)
- [Plano de agrupamento](./templates/plano-de-agrupamento.md)

## Regra

Quando uma nova etapa ou um novo caso entrar, tente primeiro preenchê-lo com este modelo antes de pensar em criar novo agente ou nova skill.

===== END FILE =====

