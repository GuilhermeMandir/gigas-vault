# Regras gerais de desenvolvimento

Última atualização: 2026-11-11 (Arquitetura Limpa como lei).

Valem para **todo projeto de programação** da vault. Cada projeto tem, além destas, uma nota própria de regras (`Projetos/<projeto>/regras-de-desenvolvimento.md`) só com o que é dele; nada desta nota se repete lá. Estas regras não dependem de nenhum projeto. Origem: decisões do usuário de 2026-10-22 (Arquitetura Limpa), 2026-11-11 (“Arquitetura limpa é lei”) e de 2026-11-10 (modelo de testes, versionamento e GitHub, confirmados com “Confirmo”).

## 1. Arquitetura Limpa — lei

**Prioridade acima de prazo, funcionalidade nova e economia de tokens.** Nenhum código entra fora destas regras “para corrigir depois”. O critério de aceite de toda entrega é conformidade total; uma entrega com desvio conhecido não está pronta. Origem: “Arquitetura limpa é lei” (usuário, 2026-11-11), depois de duas levas inteiras de refatoração no DGLab (auditoria, oito etapas, reauditoria e correção integral) que poderiam ter sido evitadas.

### Camadas

- **Domínio:** entidades e regras puras, sem dependência de interface, banco, arquivos, rede, relógio, aleatoriedade, geração de IDs ou bibliotecas externas.
- **Aplicação:** casos de uso e **portas**, as interfaces de repositório, arquivos, PDF, relógio, IDs e afins de que os casos de uso precisam. Toda decisão, validação, coordenação e transação de um caso de uso mora aqui.
- **Infraestrutura:** adaptadores finos que implementam as portas (banco, arquivos, bibliotecas externas). Não decidem política nem regra de negócio; aplicam o plano que recebem.
- **Composição:** um único ponto monta as implementações e os casos de uso.
- **Apresentação** (interface, linha de comando, API): desenha, coleta a intenção do usuário e chama **um** caso de uso por confirmação. Depende só da Aplicação e nunca pede serviços à composição como localizador.
- As dependências sempre apontam para o núcleo.

### Antes de escrever (em toda mudança, inclusive correção pontual)

Decida onde cada parte vai, e só então escreva:

| O que é | Onde vai |
| --- | --- |
| Regra do jogo/negócio, cálculo, elegibilidade, transição de estado, política de exclusão ou arquivamento | Domínio (função pura, testável sem portas) |
| Carregar dados, aplicar a regra, gerar ID, ler relógio, validar referências, gravar, desfazer/refazer, decidir o que publicar | Aplicação (caso de uso) |
| SQL, arquivo, zip, PDF, biblioteca externa | Infraestrutura (implementação de porta) |
| Montar objetos | Composição |
| Desenhar, rasterizar, gesto, prévia, seleção, rascunho na tela | Apresentação |

### Proibido (lições da correção do DGLab, 2026-11-11)

- Tela que coordena várias gravações, decide política, valida referência, cria ID persistente ou chama serviço técnico direto.
- Uma confirmação do usuário gravada por vários casos de uso em sequência (lote parcial). **Tudo ou nada por confirmação:** uma confirmação = um caso de uso = uma transação; exceções só por decisão registrada.
- Arquivo criado, publicado ou apagado fora da transação do caso de uso. Efeitos em arquivo participam de estágio/compensação: voltam no rollback, exclusões esperam o commit, gravação por temporário e renomeação (nunca destino parcial).
- Falha que vira sucesso: retorno `true` com erro guardado à parte, exceção engolida, navegação que descarta rascunho quando salvar falhou.
- Política (o que retirar, o que arquivar, o que é protegido) dentro do repositório/armazenamento.
- Capacidade descoberta por cast (`x is IFoo`): se o caso de uso precisa, a porta declara.
- Caso de uso montado fora da composição, por qualquer sintaxe ou por reflexão.
- Confiar em dado que a tela informa quando o estado gravado é a fonte (ex.: origem de movimento).
- Entrada pública que pula a validação aplicada pelos comandos especializados (toda entrada valida igual).

### Guardas automáticas (obrigatórias em todo projeto)

- Teste de arquitetura com **zero violações**: matriz de dependências entre camadas (incluindo arquivos de projeto, `.props`/`.targets` e `Compile`/`Import` de fora), fontes ambientes proibidas no núcleo, sem cast de capacidade, casos de uso montados só na composição — verificado no **binário compilado** quando a linguagem permitir, não só por texto.
- Cada desvio encontrado ganha uma guarda nova ou um teste de regressão, além da correção.
- Teste verde não certifica a localização das regras: a revisão continua obrigatória.

### Antes de cada commit e de cada entrega

- Revise o próprio diff contra as tabelas acima. Desvio **introduzido pela tarefa**: corrija antes de entregar. Desvio **preexistente** no código tocado: corrija na mesma leva; fora dele, vira item explícito do plano, com prioridade sobre funcionalidade nova, nunca uma refatoração escondida.
- Etapa ou módulo novo, e qualquer mudança de arquitetura: **revisão independente** (outro agente, só leitura) antes da entrega, conferindo o código atual, não o relato do autor.
- Brief de worker que escreve código leva esta seção, as camadas de cada arquivo permitido e o que fica proibido; o líder revisa o diff contra a lista antes de integrar.

## 2. Testes

- **Testes unitários** dos casos de uso e das regras, com implementações falsas das portas em memória: sem banco, arquivos reais ou rede. Testes de integração (banco, arquivos, bibliotecas externas) são separados e marcados.
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
- **Grafo do código** (como o Graphify): em teste no primeiro projeto que o adotou. Se servir, o índice passa a ser refeito a cada commit e alimenta o mapa do seletor e a conferência da Arquitetura Limpa. Se não servir, troca-se por um script próprio que extrai as dependências.

## 5. Etapas e entrega

- Classifique cada pedido antes de implementar (item 6 do [[AGENTS|AGENTS.md]]) e siga a skill `nova-etapa`, ou a do projeto quando houver.
- Telas novas só depois do visual aprovado. A aprovação estética final é sempre do usuário, depois da entrega.
- Projetos que geram executável informam a pasta exata do executável a cada entrega.
