# Offline Copilot Package

Formato offline sem code fences externas, para evitar ambiguidade com arquivos Markdown que já contêm blocos cercados por crases.

O arquivo `MCP-TOOLS-REFERENCE.md` foi promovido para a raiz para deixar a referência de tools MCP visível logo no início da instalação.

Este pacote já inclui a regra de que o mesmo arquivo Figma pode servir como referência, construção e library final, com páginas de referência separadas das páginas de escrita.

## Ordem de uso

1. Abra `00-prompt-inicial.md` e cole o prompt no chat do Copilot.
   Esse prompt já instrui o Copilot a ignorar qualquer instalação anterior e reinstalar tudo do zero no workspace.
2. Depois, cole os arquivos de `chunks/` em ordem: `chunk-01.md`, `chunk-02.md`, etc.
3. Ao final, envie: `FIM DA INSTALACAO`.

## Chunks gerados

- `chunk-01.md`: 3 arquivos
  - `README.md`
  - `MCP-TOOLS-REFERENCE.md`
  - `.github/agents/analista-de-conjunto-de-telas.agent.md`
- `chunk-02.md`: 7 arquivos
  - `.github/agents/criador-de-parametrizacao-de-etapa.agent.md`
  - `.github/agents/curador-de-aprendizado-de-jornada.agent.md`
  - `.github/agents/desenhador-de-template-de-etapa.agent.md`
  - `.github/agents/normalizador-de-handoff-de-etapa.agent.md`
  - `.github/agents/operador-de-jornada.agent.md`
  - `.github/agents/planejador-de-parametrizacao-de-etapa.agent.md`
  - `.github/skills/analisar-conjunto-de-telas/SKILL.md`
- `chunk-03.md`: 11 arquivos
  - `.github/skills/analisar-conjunto-de-telas/references/agrupamento-de-telas.md`
  - `.github/skills/analisar-conjunto-de-telas/references/contrato-de-saida.md`
  - `.github/skills/analisar-conjunto-de-telas/references/heuristicas-estruturais.md`
  - `.github/skills/analisar-conjunto-de-telas/references/matriz-de-decisao.md`
  - `.github/skills/criar-parametrizacao-de-etapa/SKILL.md`
  - `.github/skills/criar-parametrizacao-de-etapa/references/checklist-de-execucao.md`
  - `.github/skills/curar-aprendizado-de-jornada/SKILL.md`
  - `.github/skills/curar-aprendizado-de-jornada/learning/acertos-recorrentes.md`
  - `.github/skills/curar-aprendizado-de-jornada/learning/atualizacoes-propostas.md`
  - `.github/skills/curar-aprendizado-de-jornada/learning/erros-recorrentes.md`
  - `.github/skills/curar-aprendizado-de-jornada/learning/feedback-e-revisoes.md`
- `chunk-04.md`: 5 arquivos
  - `.github/skills/desenhar-template-de-etapa/SKILL.md`
  - `.github/skills/desenhar-template-de-etapa/references/checklist-de-descoberta-antes-da-escrita.md`
  - `.github/skills/desenhar-template-de-etapa/references/reconectar-ao-design-system.md`
  - `.github/skills/desenhar-template-de-etapa/references/regras-de-template.md`
  - `.github/skills/jornada-consignado-clusterizado/SKILL.md`
- `chunk-05.md`: 11 arquivos
  - `.github/skills/jornada-consignado-clusterizado/etapas/consentimento.md`
  - `.github/skills/jornada-consignado-clusterizado/etapas/efetivacao.md`
  - `.github/skills/jornada-consignado-clusterizado/etapas/revisao.md`
  - `.github/skills/jornada-consignado-clusterizado/etapas/simulacao.md`
  - `.github/skills/jornada-consignado-clusterizado/templates/briefing-de-etapa.md`
  - `.github/skills/jornada-consignado-clusterizado/templates/plano-de-agrupamento.md`
  - `.github/skills/normalizar-handoff-de-etapa/SKILL.md`
  - `.github/skills/normalizar-handoff-de-etapa/references/estrutura-de-relatorio.md`
  - `.github/skills/operar-jornada-clusterizada/SKILL.md`
  - `.github/skills/operar-jornada-clusterizada/references/disciplina-de-tools-mcp.md`
  - `.github/skills/operar-jornada-clusterizada/references/eixos-de-variacao.md`
- `chunk-06.md`: 3 arquivos
  - `.github/skills/operar-jornada-clusterizada/references/modelo-operacional.md`
  - `.github/skills/operar-jornada-clusterizada/references/orquestracao-multi-agent-vscode.md`
  - `.github/skills/operar-jornada-clusterizada/references/regras-de-escalabilidade.md`
- `chunk-07.md`: 3 arquivos
  - `.github/skills/operar-jornada-clusterizada/references/tools-and-prompts-oficial-figma-mcp.md`
  - `.github/skills/planejar-parametrizacao-de-etapa/SKILL.md`
  - `.github/skills/planejar-parametrizacao-de-etapa/artefatos/exemplos/consentimento-poc-001.md`
- `chunk-08.md`: 3 arquivos
  - `.github/skills/planejar-parametrizacao-de-etapa/artefatos/exemplos/simulacao-base-poc-001.md`
  - `.github/skills/planejar-parametrizacao-de-etapa/references/contrato-de-saida.md`
  - `.github/skills/planejar-parametrizacao-de-etapa/references/regras-de-modelagem.md`
