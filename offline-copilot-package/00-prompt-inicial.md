# Prompt Inicial para Copilot no VS Code

Cole este prompt primeiro no chat do Copilot:

```text
Vou reconstruir um projeto neste workspace por meio de chunks de texto.

Regras:
1. Cada próximo bloco que eu colar terá um ou mais arquivos completos no formato `## FILE: caminho/do/arquivo` seguido de um bloco de código Markdown.
2. Para cada arquivo recebido, crie ou substitua exatamente o arquivo indicado naquele caminho.
3. Preserve o conteúdo exatamente como vier, sem resumir, sem reformatar e sem inventar nada extra.
4. Se o caminho exigir pastas novas, crie as pastas.
5. Ao final de cada chunk, apenas responda com a lista dos arquivos criados ou atualizados naquele chunk.
6. Não espere internet, terminal ou links externos. Trabalhe apenas com o texto que eu colar.
7. Quando eu disser `FIM DA INSTALACAO`, responda com um resumo final da estrutura criada.
```

Depois disso, cole os arquivos em `chunks/` na ordem numérica.
