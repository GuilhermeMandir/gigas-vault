# Gigas Vault

Uma vault do [Obsidian](https://obsidian.md) pronta para trabalhar com agentes de IA (Claude Code, Codex e outros). Ela organiza seus projetos com objetivo, contexto, decisões e próximos passos. Os agentes leem e atualizam essas notas a cada tarefa, então dá para parar e retomar qualquer projeto sem perder o fio.

Esta é a versão limpa: só a estrutura, as regras e os modelos, sem projetos de ninguém.

## Como começar

1. **Copie a vault.** Use “Use this template” ou clone o repositório numa pasta sua:
   ```
   git clone https://github.com/GuilhermeMandir/gigas-vault.git minha-vault
   ```
2. **Abra no Obsidian:** “Abrir pasta como vault” e escolha a pasta.
3. **Abra um agente na mesma pasta** (Claude Code ou Codex). Eles carregam as regras sozinhos: o Codex lê o `AGENTS.md`, e o Claude Code lê o `CLAUDE.md`, que importa o `AGENTS.md`.
4. **Faça a entrevista de primeiros passos.** Peça ao agente:
   > Inicie o projeto Primeiros passos.

   O agente conduz uma entrevista curta, uma pergunta por vez, para conhecer você e configurar as regras básicas: idioma, como chamar você, projetos, jeito de trabalhar, ferramentas e cópia de segurança. No fim, ele grava as respostas nas notas certas e arquiva o projeto.

## Como a vault funciona

| Pasta | Para quê |
| --- | --- |
| `Projetos/` | Um projeto por pasta, com `contexto.md` (estado), `decisoes.md` (o que você confirmou) e `plano.md` (próxima ação e última execução). |
| `Entrada/` | Ideias e capturas que ainda não têm destino. |
| `Referências/` | Material de consulta: organização da vault (`Sistema/`), regras de desenvolvimento (`Desenvolvimento/`) e ferramentas (`Infraestrutura/`). |
| `Modelos/` | Modelos para criar projetos e recursos. |
| `Arquivo/` | Projetos encerrados. |
| `Diário/` | Registros por data, opcionais. |

- **`AGENTS.md`** é a fonte única de regras para qualquer agente: como ler os projetos, quando entrevistar você antes de implementar, como registrar decisões e como encerrar uma tarefa.
- **`Referências/Desenvolvimento/regras-gerais.md`** vale para todo projeto de programação: arquitetura definida e seguida por projeto, execução incremental, testes unitários com seleção pelo que mudou, versão semântica e Git (GitHub é opcional).
- Cada projeto pode ter a sua `regras-de-desenvolvimento.md`, só com o que é dele.

## No dia a dia

- Peça a tarefa em linguagem natural, por exemplo: “Retome o projeto X”, “Comece uma etapa nova no projeto Y” ou “Guarde esta ideia na Entrada”.
- Em etapas novas, o agente entrevista você (uma pergunta por vez), apresenta uma síntese numerada e só implementa depois do seu “Confirmo”.
- Quando um pedido não cabe em nenhum projeto, o agente propõe criar um projeto novo antes de começar.
- Quando você passa vários pedidos em sequência, ele anota cada um e faz uma entrevista no fim da leva.
- Ao terminar, o agente atualiza o contexto, o plano e as decisões do projeto, e informa o que ficou sem verificação.

## Cópia de segurança (backup)

A entrevista de primeiros passos combina com você onde guardar a cópia de segurança, e o agente a faz ao fim de cada tarefa: um repositório **privado** no GitHub, outra nuvem, só no computador ou nenhum.
