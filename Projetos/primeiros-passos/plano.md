# Primeiros passos — Plano

## Próxima ação e bloqueios

- **Próxima ação:** conduzir a entrevista abaixo, uma pergunta por vez, com 2 a 4 opções e a recomendada primeiro, sem exemplos de resposta. O usuário sempre pode responder com as próprias palavras.
- **Bloqueios:** nenhum.

## Roteiro da entrevista

Abra assim, antes da primeira pergunta:

> Boas-vindas ao **Gigas Vault**! O objetivo deste projeto é auxiliar no desenvolvimento dos seus projetos com um ambiente de trabalho inteligente e controlado, com auxílio de Inteligência Artificial. Vou fazer algumas perguntas rápidas, uma por vez, para conhecer você e ajustar as regras ao seu jeito.

Logo depois da abertura, pergunte se a pessoa quer um resumo de como a vault trabalha antes de começar (opções: “Sim, quero o resumo” e “Não, pode começar”). Se quiser, explique em poucas linhas, sem exemplos:
- cada projeto é uma pasta em `Projetos/` com `contexto.md` (estado), `decisoes.md` (o que você confirmou) e `plano.md` (próxima ação e última execução); ideias soltas vão para `Entrada/`;
- o `AGENTS.md` guarda as regras que qualquer agente segue, e projetos de programação seguem também as regras gerais de desenvolvimento;
- antes de algo novo, o agente entrevista você, uma pergunta por vez, e só implementa depois do seu “Confirmo”;
- ao terminar uma tarefa, ele atualiza os registros do projeto, diz o que ficou sem verificar e faz a cópia de segurança (backup), se houver uma configurada.

Pule perguntas que já tiverem resposta. Não pergunte o que o `AGENTS.md` já define como regra da vault (como a entrevista antes de implementar algo novo).

**Quem é você**

1. Em que idioma os agentes devem escrever?
2. Como prefere ser chamado(a)?
3. Para que vai usar a vault: trabalho, estudos, projetos pessoais, programação, escrita, outro?
4. Quais projetos você já tem em andamento? Para cada um, o objetivo em uma frase. Eles viram pastas em `Projetos/` com os modelos.

**Jeito de trabalhar**

5. Como quer as respostas: curtas e diretas, ou detalhadas com explicação?
6. O agente pode atualizar sozinho o estado e o plano dos projetos durante o trabalho (padrão), ou deve perguntar antes?

**Ferramentas**

7. Quais agentes vai usar (Claude Code, Codex, outro) e em que ambiente (terminal, aplicativo, editor)?

**Cópia de segurança**

8. Onde guardar a cópia de segurança (backup) da vault: repositório **privado** no GitHub (se escolher, diga só o nome de usuário, nunca senha ou token), outra nuvem, só no computador ou sem backup?

## Ao terminar

1. Apresente uma **síntese numerada** e espere a confirmação.
2. Grave as respostas:
   - preferências e regras pessoais → seção “Jeito de trabalhar” do `AGENTS.md`, substituindo o parágrafo e a lista que vieram com a vault (mantenha as regras de registro, confirmação e nomes de arquivo, no idioma escolhido); a escolha da pergunta 6 vale para o item de registros em “Durante o trabalho”;
   - projetos → pastas em `Projetos/` criadas com os modelos, e a lista no `inicio.md`;
   - ferramentas → nota em `Referências/Infraestrutura/` (use `Modelos/recurso.md`);
   - cópia de segurança → nota `Referências/Infraestrutura/backup.md` com onde fica e como fazer; o passo 6 do encerramento no `AGENTS.md` segue essa nota. “Sem backup” também fica registrado nela;
   - ajustes nas regras de desenvolvimento → `Referências/Desenvolvimento/regras-gerais.md`, só com confirmação explícita.
3. Registre as decisões em [[Projetos/primeiros-passos/decisoes|decisões]], com data e a frase do usuário.
4. Configure a cópia de segurança escolhida e descreva na nota `backup.md` como fazê-la ao fim de cada tarefa. Logins, instalações e senhas são sempre do usuário; o agente nunca pede nem digita senha ou token.
   - **GitHub privado:** o usuário cria o repositório privado e faz o login. Com permissão, o agente inicia o Git na vault (se ainda não houver), configura o `git remote` e faz o primeiro envio. Ao fim de cada tarefa: `git add -A`, `git commit` e `git push`, conferindo que o envio deu certo.
   - **Outra nuvem** (Google Drive, OneDrive, Dropbox e afins): o usuário instala o aplicativo de sincronização da nuvem e entra na conta. Depois escolhe entre mover a vault para dentro da pasta sincronizada (o mais simples) ou sincronizar a pasta onde ela está. Ao fim de cada tarefa, o agente só confere que a pasta está sincronizada, quando o aplicativo mostrar isso. Avise quando a conta puder expirar (por exemplo, conta de escola ou de trabalho).
   - **Só no computador:** o usuário escolhe o destino (outro disco, disco externo ou pen drive). Com permissão, o agente cria um script que copia a vault para uma pasta datada nesse destino e guarda só as cópias mais recentes. Ao fim de cada tarefa, o agente roda o script e informa se deu certo. Lembre que uma cópia no mesmo disco não protege contra a perda dele.
   - **Sem backup:** registre a escolha e a data na nota. O passo de cópia no encerramento passa a só dizer “sem cópia de segurança configurada”.
5. Mova esta pasta para `Arquivo/Projetos/primeiros-passos/` e informe o resultado.

## Última execução

Nenhuma.
