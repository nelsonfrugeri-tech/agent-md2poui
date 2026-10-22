# Agent md2poui

Pacote Agent Plugins para onboarding e desenvolvimento no fork [nelsonfrugeri-tech/md2poui](https://github.com/nelsonfrugeri-tech/md2poui).

Inclui um agente `md2poui`, cinco Skills (onboarding, CLI, renderização Markdown, geração Angular e code review) e cinco MCPs: GitHub, Trello, Notion, Graphify e deja-vu.

GitHub/Trello/Notion passam pelo gateway pessoal do Smart Harness. Graphify/deja-vu usam os runtimes locais gerenciados pelo Harness. O pacote não contém credenciais nem concede acesso adicional. As permissões permanecem na plataforma.

As referências do projeto foram conferidas no commit `9b65624b9b8c9e27ee73e279eeef2afffbcde269`, em 22/10/2026. O agente deve revalidar o checkout atual. A correção do CLI e o título automático sem H1 já existem nessa revisão.

Os arquivos em `dev.smartharness/agents/` e `skills/` são a fonte editável. `harness generate . --target claude-code` cria a camada de execução do Claude Code. A extensão `local_connectors` requer a versão do Harness que oferece pacotes mistos.

Veja o README da raiz do repositório para validação e teste local. Uma instalação bem-sucedida não comprova autenticação dos MCPs ou execução de uma feature.
