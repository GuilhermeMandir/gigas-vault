# Regras gerais de desenvolvimento

Última atualização: 2026-11-10.

Valem para **todo projeto de programação** da vault. Cada projeto tem, além destas, uma nota própria de regras (`Projetos/<projeto>/regras-de-desenvolvimento.md`) só com o que é dele; nada desta nota se repete lá. Estas regras não dependem de nenhum projeto. Origem: decisões do usuário de 2026-10-22 (Arquitetura Limpa) e de 2026-11-10 (modelo de testes, versionamento e GitHub, confirmados com “Confirmo”).

## 1. Arquitetura Limpa

- **Domínio:** entidades e regras puras, sem dependência de interface, banco, arquivos, rede ou bibliotecas externas.
- **Aplicação:** casos de uso e **portas**, as interfaces de repositório, arquivos, PDF, relógio e afins de que os casos de uso precisam.
- **Infraestrutura:** implementações das portas (banco, arquivos, bibliotecas externas). Não contém regra de negócio.
- **Apresentação** (interface, linha de comando, API): depende só da Aplicação. A montagem das implementações fica num único ponto de composição.
- As dependências sempre apontam para o núcleo. Um desvio encontrado vira item explícito do plano, nunca uma refatoração escondida dentro de outra tarefa.
- No levantamento de cada etapa, confira se o código que ela vai tocar segue estas regras.

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
