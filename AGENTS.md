# AGENTS — regras da vault

Fonte única de regras para qualquer agente (Claude Code, Codex e outros). O `CLAUDE.md` da raiz só importa este arquivo. Regras de desenvolvimento: [[Referências/Desenvolvimento/regras-gerais|regras gerais]] (todo projeto de programação) e `Projetos/<projeto>/regras-de-desenvolvimento.md` (cada projeto).

## Jeito de trabalhar (regras do usuário)

Esta seção é preenchida pela entrevista de [[Projetos/primeiros-passos/plano|Primeiros passos]] com as preferências de quem usa a vault: idioma, como chamar a pessoa, tamanho das respostas, se os registros são atualizados sozinhos ou com pergunta antes, e a cópia de segurança. Enquanto ela não for feita, vale:

- Use o idioma em que o usuário escrever.
- Preserve os fatos que o usuário informou.
- Separe suas propostas das decisões que ele confirmou.
- Quando ele aprovar uma mudança, atualize a nota responsável e registre a decisão.
- Use nomes de arquivo em kebab-case e datas no formato AAAA-MM-DD.
- Peça confirmação antes de apagar ou reorganizar muitos arquivos.
- Entrada guarda materiais ainda não organizados; Referências, material de consulta.

## Arquitetura Limpa é lei

Em todo projeto de programação, a Arquitetura Limpa vem **antes** de prazo, funcionalidade nova e economia de tokens, inclusive em correção pontual e trabalho de worker: decida a camada de cada parte antes de escrever ([[Referências/Desenvolvimento/regras-gerais|regras gerais]], seção 1), não entregue desvio “para corrigir depois”, rode o teste de arquitetura (zero violações) e revise o próprio diff contra a lista de proibidos antes de cada commit. Etapa ou módulo novo passa por revisão independente antes da entrega. Uma entrega com desvio conhecido não está pronta.

## Antes de executar

1. Consulte [[inicio|inicio.md]] para localizar o projeto ou a referência pertinente.
2. No projeto, leia `contexto.md` e `decisoes.md`, depois `plano.md`, nessa ordem. Use caminhos completos a partir da raiz da vault para distinguir notas com o mesmo nome.
3. Confirme fatos técnicos no repositório ou na fonte correspondente. Código, instalação e testes ficam documentados junto ao código; a vault guarda o contexto e os links necessários à retomada.
4. Consulte [[Referências/Sistema/organizacao|organização da vault]] quando precisar criar, mover ou encerrar notas e projetos.
5. Use as skills em `.claude/skills/`. Projetos com skills próprias as listam na sua nota `regras-de-desenvolvimento.md` (ou no `contexto.md`); sem elas, use `nova-etapa` para etapas novas. Em ambientes que não carregam as skills automaticamente, leia o `SKILL.md` correspondente.
6. Classifique o pedido antes de implementar, em qualquer projeto:

   | Pedido | Antes de implementar |
   | --- | --- |
   | Etapa ou módulo novo, ou mudança de escopo | Entrevista completa: levantamento, perguntas uma por vez, síntese numerada e confirmação explícita. Em telas novas, também o visual aprovado. Siga a skill `nova-etapa` ou a skill de etapa nova do projeto, se houver. |
   | Ajuste ambíguo ou que contraria uma decisão registrada | Entrevista curta: só as perguntas necessárias e a confirmação do que muda. |
   | Correção clara e pontual | Execute e registre, sem entrevista. |

   Na dúvida entre duas classes, use a mais cuidadosa e diga qual escolheu.
   **Projeto novo:** antes de classificar, identifique a que projeto o pedido pertence. Trabalho com objetivo próprio, que vai durar mais de uma tarefa e não cabe no objetivo de um projeto existente, é um **projeto novo**: diga isso ao usuário e proponha criar a pasta em `Projetos/` antes de começar. Não registre esse trabalho dentro de outro projeto nem só em notas de Referências.
   Quando o usuário passar uma leva de pedidos (vários itens ditados em sequência), anote cada item e, ao fim da leva, faça uma entrevista para validar os pontos em aberto antes de implementar ou de arquivar a leva.

7. **Regras de desenvolvimento:** todo projeto de programação segue [[Referências/Desenvolvimento/regras-gerais|as regras gerais de desenvolvimento]] (Arquitetura Limpa, testes unitários e seleção pelo que mudou, versionamento semântico, Git, com GitHub opcional) e a nota `Projetos/<projeto>/regras-de-desenvolvimento.md` do próprio projeto. Projeto novo herda as gerais e cria só a sua nota, sem repetir o texto delas. Projetos que geram executável informam a pasta do executável a cada entrega.

## Durante o trabalho

- Execute o objetivo autorizado e preserve a distinção entre fatos verificados, hipóteses, propostas e decisões confirmadas.
- Mantenha os registros do projeto (fatos verificados, progresso, bloqueios e próximos passos) como o usuário escolheu em “Jeito de trabalhar”: atualizando sozinho ou perguntando antes. Sem escolha registrada, atualize sozinho; essa manutenção faz parte da tarefa.
- Mudanças de objetivo, prioridade ou decisões ficam como propostas em `plano.md` até a manifestação do usuário. Quando aprovadas, atualize a nota responsável e registre data, justificativa e referência da confirmação em `decisoes.md`.
- Registre ferramentas, dependências e procedimentos compartilhados em `Referências/Infraestrutura/`, uma nota por recurso (modelo em `Modelos/recurso.md`).
- Encaminhe capturas da Entrada pertinentes à tarefa para sua fonte principal. Quando o destino depender do usuário, deixe essa pendência explícita. O Diário é opcional e aponta para o projeto sem duplicar seu histórico.
- Antes de alterar uma nota compartilhada, releia sua versão atual e preserve as mudanças de outros agentes. Identifique o ambiente responsável, como Codex ou Claude Code, nas novas entradas de execução.
- Em tarefas paralelas, coordene quem atualiza cada nota e evite duas gravações simultâneas no mesmo arquivo. Sinalize conflitos entre fatos ou decisões antes de substituir informações divergentes.

## Antes de encerrar a tarefa

1. Atualize `contexto.md` com o estado, as entregas verificadas, a data e as fontes.
2. Atualize `plano.md` com próxima ação, bloqueios, propostas e uma entrada curta de execução: trabalho, resultado, verificações e o que continua sem verificação.
3. Registre novas decisões confirmadas em `decisoes.md` e atualize as referências afetadas. Ao substituir uma decisão, indique qual foi substituída e o motivo.
4. Verifique links e navegação. Mudanças feitas fora do Obsidian também exigem atualizar os links manualmente.
5. Quando o projeto terminar, registre resultado, data e motivo do encerramento; mova sua pasta inteira para `Arquivo/Projetos/<nome-do-projeto>/` e atualize os caminhos. Observe a regra de confirmação para apagar ou reorganizar muitos arquivos; um plano já aprovado vale como autorização para os movimentos que ele especifica.
6. Faça a cópia de segurança (backup) como estiver configurada na nota de backup em `Referências/Infraestrutura/`. Sem cópia configurada, pule este passo e diga isso ao usuário.
7. Informe ao usuário o resultado, os limites da verificação e as decisões ainda pendentes. Não marque como realizado um procedimento apenas proposto ou configurado sem teste.

## Entrada em outros ambientes de agentes

Claude Code e Codex abertos na pasta da vault carregam estas instruções sozinhos (o `CLAUDE.md` importa este `AGENTS.md`; o Codex lê o `AGENTS.md` da pasta). Nesses casos, basta pedir a tarefa, sem repetir o protocolo.

Quando o ambiente não carregar a vault sozinho (chat comum, outra ferramenta) ou o agente for aberto fora da vault, como na pasta de um repositório, inclua no pedido:

> Leia o `AGENTS.md` da vault e, para o projeto escolhido, leia `contexto.md`, `decisoes.md` e `plano.md` antes de agir. Atualize os registros ao concluir o trabalho.

Em qualquer caso, verifique no início que o agente citou o `contexto.md` e o `plano.md` do projeto; acesso ao diretório por si só não garante a leitura.
