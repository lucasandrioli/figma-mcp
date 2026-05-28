# Regras de Modelagem

- `mode` é reservado para cluster.
- `variant` é reservado para estado/interação.
- `string` é reservada para conteúdo textual que mantém a mesma função.
- `boolean` é reservada para presença/ausência de bloco sem quebrar o template.
- `number` é reservada para parâmetros locais que precisem ser editáveis e reutilizáveis.
- Tokens visuais vêm da library de tokens, não da collection local de conteúdo.
- Collections locais podem ser por etapa, por módulo ou por domínio de conteúdo.
- Variables locais servem para conteúdo, regras de presença e outros parâmetros reutilizáveis.
- A implementação do boolean pode acontecer por `visible` ou por outro vínculo estrutural compatível com a library real.
- Se um módulo tem layout próprio e conteúdo próprio, ele pode ter template próprio e collection própria.
