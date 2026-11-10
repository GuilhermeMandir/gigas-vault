# Organização da vault

Última atualização: 2026-10-29.

A vault reúne objetivos, contexto, decisões e próximos passos dos projetos. Comece em [[inicio|Início]]. O planejamento aprovado registra as escolhas que orientam esta primeira versão.

## Onde guardar cada informação

| Local | Uso |
| --- | --- |
| `Projetos/` | Trabalho com objetivo, resultado e término definidos. Cada projeto começa com `contexto.md`, `decisoes.md` e `plano.md`. |
| `Referências/` | Material de consulta e procedimentos úteis entre projetos: `Sistema/` (esta organização), `Desenvolvimento/` ([[Referências/Desenvolvimento/regras-gerais|regras gerais de desenvolvimento]]) e `Infraestrutura/` (índice de infraestrutura). Regras de um projeto específico ficam em `Projetos/<projeto>/regras-de-desenvolvimento.md`. |
| `Entrada/` | Capturas cujo destino ainda não está definido. Registre origem, contexto e data, quando disponíveis. |
| `Diário/` | Registros opcionais por data, em `AAAA-MM-DD.md`. Ao citar projetos, faça um resumo breve e aponte para suas notas. |
| `Modelos/` | Formatos reutilizáveis para iniciar notas sem decidir a estrutura de novo. |
| `Arquivo/` | Projetos encerrados e recursos desativados que continuam úteis para consulta. |

Na raiz ficam apenas `inicio.md`, `AGENTS.md`, `CLAUDE.md`, as seis pastas e `skills-lock.json`, que o instalador de skills mantém para a Alethe. As pastas ocultas `.obsidian`, `.claude` e `.agents` guardam configurações e skills. `.git`, `.gitignore` e `.scripts` servem ao backup no GitHub (Obsidian e vault Gigas). Scripts e arquivos de trabalho pertencem ao repositório do projeto.

Informação com destino conhecido vai diretamente à nota responsável. Encaminhe capturas pertinentes ao trabalho: mova ou incorpore seu conteúdo e retire a duplicata da Entrada. Quando a classificação depender do usuário, registre a pendência. Não crie notas diárias vazias por obrigação.

## Nomes, links e fontes principais

- Use português brasileiro, nomes de notas e pastas de projeto em kebab-case e datas em `AAAA-MM-DD`. Preserve os nomes das seis pastas da raiz e as grafias convencionais `AGENTS.md` e `CLAUDE.md`.
- Use links Markdown ou links do Obsidian com o caminho completo a partir da raiz da vault. Como vários projetos têm `contexto.md`, o nome isolado não identifica o destino com segurança.
- Crie o destino antes de adicionar um link navegável. Nos modelos, substitua as orientações por links reais; não deixe links para projetos fictícios.
- Mantenha cada informação atual em uma fonte principal: estado em `contexto.md`; decisões confirmadas em `decisoes.md`; ações, bloqueios, propostas e execução em `plano.md`. Índices e Diário apontam para essas fontes.
- Preserve instalação, testes e detalhes de implementação junto ao código, nos diretórios dos próprios repositórios. A vault registra contexto e links para essas fontes.
- Use Graphify como apoio quando configurado, sem presumir que um índice inclua alterações recentes. Preserve na vault o contexto necessário para retomar o trabalho.

## Criar e retomar um projeto

1. Crie uma pasta em `Projetos/` com nome que expresse o objetivo.
2. Crie `contexto.md`, `decisoes.md` e `plano.md` usando os modelos de [[Modelos/contexto|contexto]], [[Modelos/decisoes|decisões]] e [[Modelos/plano|plano]]. Remova orientações e seções inaplicáveis, mantendo os campos necessários para entender e retomar o projeto.
3. Preencha objetivo, resultado esperado, limites, critérios de conclusão e estado conhecido. Registre a próxima ação concreta e o que ainda depende de decisão ou verificação. Não transforme uma proposta em decisão confirmada.
4. Conecte as três notas com links qualificados, acrescente as fontes e recursos relevantes e adicione o projeto ativo a [[inicio|Início]].
5. Para retomar, leia `contexto.md` e `decisoes.md`, depois `plano.md`; consulte a documentação e o código conforme a tarefa.

### Etapas novas e entrevista

**Regra aprovada em 2026-10-29 (Claude Code).** Os agentes classificam cada pedido antes de implementar, em qualquer projeto:
- **etapa nova ou mudança de escopo**: entrevista completa, com síntese confirmada e visual aprovado quando houver tela;
- **ajuste ambíguo ou que contraria uma decisão**: entrevista curta;
- **correção clara**: executar e registrar.

O roteiro está na skill `.claude/skills/nova-etapa/SKILL.md`. Um projeto pode ter uma skill própria, mais detalhada, citada na sua nota de regras. A tabela da regra está em [[AGENTS|AGENTS.md]].

- **Confirmação:** o usuário propôs manter a entrevista em qualquer projeto (“A parte da entrevista eu acho que seria interessante manter em qualquer projeto”) e aprovou o formato proporcional apresentado (“Aprovo”).
- **Justificativa:** no primeiro projeto em que foi usada, a entrevista evitou retrabalho e deixou decisões retomáveis. Ser proporcional evita burocracia em correções pequenas.
- **Teste e entrega:** em projetos sem skills próprias, são combinados na entrevista. Quando o processo se repetir, pode virar skills do projeto.

### Estado vigente e histórico

As notas principais mostram primeiro o que vale agora. Os títulos fixos permitem links estáveis: `contexto.md` começa por **Objetivo e limites** e **Estado atual**, e `plano.md` por **Próxima ação e bloqueios** e **Última execução**. Ao atualizar, reescreva essas seções em vez de acrescentar uma nova seção datada no topo.

Quando o registro crescer, mova as entradas anteriores sem alterar o texto para `historico-do-contexto.md` e `historico-do-plano.md`, na pasta do projeto, com a mais recente no topo. O histórico preserva as evidências; termos como "vigente" ou "aguardando" valem para a data de cada registro. Atualize os links para títulos movidos.

Melhorias de infraestrutura com resultado e término definidos também são projetos. Seus procedimentos permanentes e inventário ficam em `Referências/Infraestrutura/`; use [[Modelos/recurso|o modelo de recurso]] quando necessário e atualize o índice.

## Manter os registros durante o trabalho

Os agentes começam por [[AGENTS|AGENTS.md da raiz]], fonte única de regras, e pelas [[Referências/Desenvolvimento/regras-gerais|regras gerais de desenvolvimento]] quando o projeto é de programação. Oriente cada ambiente de agente a fazer essa leitura; o acesso à pasta não garante que as instruções sejam carregadas.

O `CLAUDE.md` da raiz tem só `@AGENTS.md`, para o Claude Code carregar as mesmas instruções. O acesso pelo Claude e a verificação estão documentados em Agentes de IA. Antes de gravar uma nota compartilhada, releia sua versão atual, preserve alterações anteriores e identifique o ambiente nas entradas de execução. Em trabalho paralelo, coordene quem atualiza cada nota.

Dentro do objetivo autorizado, o agente pode atualizar automaticamente fatos verificados, progresso, bloqueios e próximos passos. Alterações de objetivo, prioridade e decisões permanecem propostas até a confirmação do usuário. Preserve os fatos informados e diferencie evidência, hipótese, proposta e decisão.

Após mudanças relevantes e antes de encerrar uma tarefa:

1. Atualize o estado e as evidências em `contexto.md`, e a próxima ação, as pendências e os bloqueios em `plano.md`.
2. Acrescente ao registro de execução somente acontecimentos úteis: data, trabalho, resultado, verificações e referências. Explicite o que ainda não foi verificado.
3. Registre decisões aprovadas em `decisoes.md` e atualize as notas responsáveis. Se uma decisão substituir outra, preserve o histórico e registre o motivo.
4. Atualize referências afetadas, encaminhe capturas pertinentes e confira os links. Informe ao usuário o resultado e as decisões pendentes.

Essa manutenção faz parte da tarefa; não estabelece monitoramento permanente.

## Encerrar e arquivar

Antes de encerrar, confira os critérios de conclusão e registre resultado, data e motivo do encerramento. Uma pendência não resolvida deve continuar explícita, com seu destino ou adiamento aprovado; não apresente verificações ausentes como concluídas. Registre também cancelamentos e suas razões.

Mova o projeto como uma unidade de `Projetos/` para `Arquivo/Projetos/`, preservando o nome da pasta e um único histórico. Atualize os links para as três notas e demais arquivos movidos, retire o projeto da lista de ativos e mantenha uma referência ao encerramento na navegação quando útil. Verifique os destinos após a mudança. Recursos desativados podem ir para `Arquivo/Infraestrutura/` quando houver necessidade.

Peça confirmação antes de apagar ou reorganizar muitos arquivos. Atualizações pontuais dos registros continuam a cargo do agente, dentro do trabalho autorizado.

## Operação da vault

As instruções, configurações e verificações operacionais têm como fonte principal Obsidian e a vault Gigas. Consulte essa nota para localização, acesso, uso dos modelos, recuperação e estado do backup.

Em 2026-10-22, o usuário decidiu usar a vault somente neste computador por enquanto e preparar uma proposta de backup, deixando sua implementação pendente. A proposta e seu estado são mantidos na nota operacional. Comece com os recursos nativos do Obsidian; plugins adicionais devem responder a uma necessidade concreta.
