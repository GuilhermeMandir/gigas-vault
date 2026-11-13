# Regras gerais de desenvolvimento

Última atualização: 2026-11-13 (arquitetura por projeto e execução incremental aprovadas).

Valem para **todo projeto de programação** da vault. Cada projeto tem, além destas, uma nota própria de regras (`Projetos/<projeto>/regras-de-desenvolvimento.md`) só com o que é dele; nada desta nota se repete lá. Estas regras não dependem de nenhum projeto. Origem: decisões de 2026-11-10 (testes, versionamento e GitHub) e 2026-11-13 (arquitetura por projeto e fluxo incremental). A obrigação universal anterior de Arquitetura Limpa foi substituída; sua regra completa foi transferida para o DGLab.

## 1. Arquitetura definida por projeto

Todo projeto de programação deve **definir bem sua arquitetura, documentá-la e segui-la fielmente**. A escolha deve atender ao objetivo, à complexidade, aos riscos e à manutenção esperada; Arquitetura Limpa é uma opção, não uma obrigação geral.

- Antes da primeira implementação, definir na nota `regras-de-desenvolvimento.md` do projeto a arquitetura adotada, responsabilidades dos módulos ou camadas, dependências permitidas, fronteiras de dados/efeitos externos e como conferir a conformidade. Detalhes técnicos ficam junto ao código, com link na vault.
- Em projeto existente, consultar a arquitetura registrada antes de escrever. Se faltar definição ou houver conflito, esclarecer e registrar antes da alteração dependente; não inventar uma nova arquitetura silenciosamente.
- Em cada mudança, localizar as responsabilidades e os arquivos na arquitetura escolhida. Não criar camadas, portas ou serviços sem necessidade dessa arquitetura e do comportamento pedido.
- Revisar o próprio diff antes de cada commit; aplicar as verificações de arquitetura definidas pelo projeto e corrigir desvios introduzidos antes da entrega. Desvios preexistentes encontrados devem ser registrados e tratados conforme as regras do projeto, sem refatoração ampla escondida.
- Etapa ou módulo novo e mudança de arquitetura passam por revisão independente antes da entrega. Mudança da arquitetura acordada exige proposta e confirmação; prazo ou economia de tokens não autorizam descumpri-la.
- Brief de worker escritor informa a arquitetura vigente, responsabilidade de cada arquivo permitido e dependências/alterações proibidas. O líder confere o diff antes de integrar.
- No **DGLab**, a Arquitetura Limpa e seus portões continuam obrigatórios: regra específica.

**Decisão de 2026-11-13:** substitui a obrigação universal de Arquitetura Limpa de 2026-11-11. Confirmação: “passar a regra para o projeto e deixar a regra geral como sempre definir bem uma arquitetura e seguila fielmente”. O DGLab conserva a escolha anterior.

## 2. Testes

- **Testes unitários** das regras e unidades definidas pela arquitetura do projeto, com dependências substituídas em memória quando necessárias: sem banco, arquivos reais ou rede. Testes de integração (banco, arquivos, bibliotecas externas) são separados e marcados.
- **Seleção pelo que mudou:** antes de testar, um seletor lê o `git diff` e consulta um **mapa versionado** (arquivo → testes e percursos), mostra o plano com os motivos e roda só o necessário.
  - Mudança só em documentação não roda nada.
  - Arquivo fora do mapa amplia a seleção: na dúvida, roda mais.
- **Arquivos compartilhados** (inicialização, ponto de composição, navegação, estilo global, apoio aos testes, arquivos de projeto e de versão do SDK) disparam a verificação ampla. A lista concreta fica na nota de cada projeto.
- **Verificação completa** só quando o usuário pedir e antes de cada **versão completa**. O dia a dia e as entregas intermediárias usam a seleção.
- **Testes de interface esperam por condição** (elemento visível, arquivo gravado), nunca por tempo fixo.
- **Modo comparar:** nas primeiras entregas de cada projeto com o seletor, rode também a completa e registre o que só ela pegou. Cada divergência corrige o mapa, e a comparação sai depois de algumas entregas sem divergência.
- Um retorno zero sem contagem explícita de testes não conta como aprovação.
- Relate as contagens, o que foi inspecionado e o que **não** foi verificado.

## 3. Versionamento e código

- **Versão semântica** `MAIOR.MENOR.CORREÇÃO`:
  - MENOR sobe a cada versão completa com funcionalidade nova;
  - MAIOR sobe quando algo deixa de ser compatível (arquivos, dados, comportamento esperado);
  - CORREÇÃO sobe nas correções;
  - entregas intermediárias levam sufixo, como `0.4.0-pre.3`.
- A versão aparece no aplicativo e no nome do pacote, ganha **tag** no Git (`v0.4.0`) e uma lista do que mudou.
- **Git em todo projeto**, com commit antes de cada etapa e ao fim de cada entrega. **GitHub é opcional** (decisão de 2026-11-10: “O Github não vai ser obrigatório mais”): se o usuário usar, o código fica num repositório **privado** dele, com `git push` nos mesmos momentos, conferindo que `origin/main` ficou igual ao `HEAD`. Cada projeto diz na sua nota de regras onde fica o código.
- Commits pequenos e descritivos. Não use `--no-verify` nem pule assinaturas.

## 4. Ferramentas de apoio

Valem quando a vault tiver a ferramenta configurada, com nota própria em `Referências/Infraestrutura/`.

- **Orquestração de workers** (como a Alethe): o trabalho divisível vai para workers, conforme a regra da ferramenta no `AGENTS.md`.
- **Grafo do código** (como o Graphify): em teste no primeiro projeto que o adotou. Se servir, o índice passa a ser refeito a cada commit e alimenta o mapa do seletor e a conferência da arquitetura adotada. Se não servir, troca-se por um script próprio que extrai as dependências.

## 5. Etapas e entrega

- Classifique cada pedido antes de implementar (item 6 do [[AGENTS|AGENTS.md]]) e siga a skill `nova-etapa`, ou a do projeto quando houver.
- Telas novas só depois do visual aprovado. A aprovação estética final é sempre do usuário, depois da entrega.
- Projetos que geram executável informam a pasta exata do executável a cada entrega.

## 6. Execução incremental e contexto curto

Regra aprovada em 2026-11-13 (“Pode atualizar a vault”), a partir do estudo do DGLab. O usuário pode pedir uma leva grande; o agente organiza a execução sem exigir que ele faça a divisão técnica.

- Dividir o escopo aprovado em fluxos pequenos e verificáveis. Quando houver contratos novos compartilhados, concluir primeiro uma fatia ponta a ponta para estabilizá-los antes de paralelizar unidades dependentes.
- Definir dono dos dados, intenção, responsabilidades, fronteira transacional e falhas esperadas num contrato curto, proporcional à tarefa; reaproveitar a arquitetura e padrões existentes.
- Integrar cada unidade pronta e verificar o que ela afeta, antes de acumular a próxima. Antecipar revisão das fronteiras de migração, importação e dados persistidos.
- Usar Alethe nas unidades independentes conforme `AGENTS.md`; trabalho pequeno ou acoplado permanece com o líder. Evitar workers que precisam continuamente do resultado inacabado uns dos outros.
- Após as leituras obrigatórias, carregar só os trechos relevantes. Briefs e relatórios são curtos e apontam para fontes. Antes de pausa, registrar revisão atual, pendências, evidências válidas e próximo passo; retomar só os agentes necessários com esse checkpoint.
- Associar evidências à revisão, dependências, testes, ferramentas e dados utilizados. Reaproveitar apenas resultados comprovadamente válidos; alterações relevantes invalidam os dependentes. Se não houver rastreabilidade suficiente, verificar novamente. Isso não dispensa portões por commit, gatilhos amplos ou a verificação de versão completa.
- Acompanhar processos por resumo final ou falha, evitando consultas frequentes que apenas repetem o mesmo estado. Registrar separadamente tempo de execução, espera e consumo do líder/workers quando disponível; cache, saída e entrada nova ficam separados. Não estimar preço ou cota sem fonte.
- Ajustes dos seletores, cache automático de resultados e novas ferramentas precisam de implementação e validação próprias; esta regra não afirma que já existem. Não alterar o conjunto obrigatório de testes sem decisão específica.
