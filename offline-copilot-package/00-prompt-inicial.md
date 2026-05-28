# Prompt Inicial para Copilot no VS Code

Cole este prompt primeiro no chat do Copilot:

```text
Ignore a instalação anterior deste projeto.

Quero reinstalar tudo do zero neste workspace, substituindo o que já existir pelos novos arquivos que eu vou colar em sequência.

Regras:
1. Cada próximo bloco que eu colar terá um ou mais arquivos completos no formato `===== FILE: caminho =====` e terminará com `===== END FILE =====`.
2. Para cada arquivo recebido, crie ou substitua exatamente o arquivo indicado naquele caminho.
3. Preserve o conteúdo exatamente como vier, sem resumir, sem reformatar e sem inventar nada extra.
4. Se o caminho exigir pastas novas, crie as pastas.
5. Ao final de cada chunk, apenas responda com a lista dos arquivos criados ou atualizados naquele chunk.
6. Não espere internet, terminal ou links externos. Trabalhe apenas com o texto que eu colar.
7. Ignore qualquer conteúdo de explicação fora dos delimitadores dos arquivos.
8. Quando eu disser `FIM DA INSTALACAO`, responda com um resumo final da estrutura criada.
```

Depois disso, cole os arquivos em `chunks/` na ordem numérica, do `chunk-01.md` ao `chunk-08.md`.
