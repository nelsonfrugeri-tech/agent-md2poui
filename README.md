# agent-md2poui

Agente para ajudar novos colaboradores a entender o [md2poui](https://github.com/nelsonfrugeri-tech/md2poui), implementar mudanças e preparar revisão com os padrões do projeto.

Este repositório guarda o pacote do assistente. O código do conversor continua no fork `nelsonfrugeri-tech/md2poui`.

## Conteúdo

| Componente | Conteúdo |
| --- | --- |
| Agent | `md2poui`: onboarding, contexto da tarefa e desenvolvimento |
| Tools remotas | GitHub, Trello e Notion pelo gateway pessoal |
| Tools locais | Graphify e deja-vu pelo runtime gerenciado do Harness |
| Skills | onboarding, opções do CLI, renderização Markdown, artefatos Angular e code review |

O agente consulta história e ADR quando fizerem parte da tarefa, navega pelo código, carrega a Skill pertinente e valida a mudança. Uma sessão que escreveu o código faz autoinspeção e entrega a revisão independente ao coordenador. Só há um Agent neste pacote.

## Validar e empacotar

Use o Harness v0.2.3 ou superior. Na raiz deste repositório:

```sh
harness validate package
harness generate package --target claude-code
harness validate package
harness pack package -o agent-md2poui-1.0.1.tar.gz
```

O diretório `package/` contém somente o conteúdo publicável. A raiz fica disponível para documentação e workflow de release. O pacote preserva os contratos Agent Plugins e a extensão de Agents do Smart Harness.

## Publicar uma versão

1. Faça a alteração em uma branch e revise o PR antes de integrar.
2. Atualize `version` em `package/plugin.json` e execute os comandos de validação, geração e empacotamento acima, ajustando o nome do arquivo.
3. Crie uma tag correspondente à versão, como `v1.0.1`, no commit revisado. Publique um GitHub Release dessa tag com o arquivo `.tar.gz` gerado como asset. Cada Release deve conter exatamente um pacote `.tar.gz`.
4. No Marketplace, use **Publicar do GitHub**, cadastre `nelsonfrugeri-tech/agent-md2poui` e sincronize a tag. Para as próximas versões, selecione o repositório já cadastrado.

O arquivo fica no GitHub. O Harness valida o pacote e registra catálogo, revisão e SHA-256 no SQLite. Publicar novamente a mesma versão com outro conteúdo é recusado; use uma nova versão. Este repositório é privado e a credencial de leitura fica no servidor.

## Instalar pelo Marketplace

Com a release publicada no GitHub e sincronizada na plataforma, use o Harness com suporte a Agents e configure o token pelo fluxo de login:

```sh
harness agents install agent-md2poui
harness agents check agent-md2poui
```

A instalação prepara também os runtimes Graphify e deja-vu incluídos no pacote. O agente aceita os namespaces dos cinco MCPs tanto deste pacote quanto das Tools instaladas separadamente, pois o Claude pode expor apenas uma cópia de cada serviço. As permissões continuam limitadas aos mesmos cinco serviços. Abra o Claude no checkout do código `md2poui`:

```sh
claude --agent agent-md2poui:md2poui
```

Para usar o provider configurado pelo Harness na mesma pasta:

```sh
harness vendor=claude --agent agent-md2poui:md2poui
```

## Testar alterações locais do pacote

Depois de `harness generate package --target claude-code`, inicie o Claude no checkout do código `md2poui`, apontando para o pacote local:

```sh
claude --plugin-dir /caminho/agent-md2poui/package --agent agent-md2poui:md2poui
```

O `--plugin-dir` é para testar conteúdo local. O pacote publicado é instalado por `harness agents install`.

Exemplos de pedido:

- “Sou novo no projeto. Explique o fluxo do CLI até os templates e indique como rodar os testes.”
- “Leia este card do Trello e a ADR vinculada. Explique o impacto no código antes de implementar.”
- “Implemente esta alteração no fork, rode os testes e prepare o contexto para uma revisão independente.”

Graphify precisa de um grafo no checkout atual. Quando útil, gere-o com `harness tools run graphify update ./src` e reinicie a sessão para reconectar o MCP. Sem grafo, o agente informa a limitação e pode ler o código diretamente. deja-vu consulta apenas o histórico pertinente ao pedido.

## Acesso e limites

GitHub, Trello e Notion precisam de permissões e credenciais configuradas no servidor. O pacote não inclui segredos nem amplia acesso. O catálogo remoto atual é de leitura; publicar PR/comentário depende de ferramenta autenticada de escrita e da autorização da tarefa. Não há merge automático.

As referências foram atualizadas a partir de `md2poui@9b65624b9b8c9e27ee73e279eeef2afffbcde269`, em 22/10/2026. Corrigir argumentos do CLI ou acrescentar o título sem H1 não são desafios novos nessa revisão: ambos já foram implementados. O agente confere o commit atual antes de recomendar mudanças.
