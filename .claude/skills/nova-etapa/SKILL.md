---
name: nova-etapa
description: Roteiro genérico para iniciar uma etapa, módulo ou projeto novo, ou uma mudança de escopo, em qualquer projeto da vault Gigas: leitura, levantamento, entrevista com síntese confirmada, visual aprovado quando houver tela, combinação de testes e entrega, e só então implementação. Use antes de codificar qualquer etapa nova; se o projeto tiver uma skill própria de etapa nova, use a dele.
---

# Nova etapa (qualquer projeto)

Cada passo só avança com a confirmação explícita do usuário. Se o projeto tiver skill própria de etapa nova (citada na sua nota de regras), siga a dele, que detalha este roteiro.

**Quando usar** (regra do `AGENTS.md` da vault):
- etapa ou módulo novo, ou mudança de escopo: este roteiro completo;
- ajuste ambíguo ou que contraria uma decisão registrada: só os passos 1 e 3, com as perguntas necessárias;
- correção clara e pontual: não use; execute e registre.

## 1. Leitura (antes de qualquer ação)
- Siga `AGENTS.md` da vault e `AGENTS.md` (“Jeito de trabalhar”). Leia `contexto.md`, `decisoes.md` e `plano.md` do projeto, nessa ordem.
- No repositório, se houver: `AGENTS.md`, README e a documentação das etapas relacionadas.
- Confirme a leitura com um resumo curto: o estado atual, as decisões que valem para a etapa e o que ainda não está definido.
- Projeto novo: crie a pasta em `Projetos/` com os modelos de `Modelos/`, conforme `Referências/Sistema/organizacao.md`.
- Siga as [[Referências/Desenvolvimento/regras-gerais|regras gerais de desenvolvimento]] (Arquitetura Limpa, testes, versionamento, GitHub) e a nota `regras-de-desenvolvimento.md` do projeto: confira se o código que a etapa vai tocar segue as regras e registre os desvios no plano.

## 2. Levantamento
- Estude as fontes do usuário (documentos, exemplos, imagens, sistemas parecidos) e o que já existe no código.
- Registre o levantamento separando **verificado** de **hipótese**: na documentação do repositório, se houver; senão, no `plano.md`. Para cada requisito, anote de onde vem (fonte, regra existente ou escolha do usuário) e o que falta para atendê-lo.

## 3. Entrevista
- Uma pergunta por vez, com a recomendação marcada como primeira opção. Pergunte só o que não dá para descobrir sozinho.
- Inclua, se ainda não estiverem decididos:
  - **como testar**: testes automáticos, capturas de tela, roteiro manual;
  - **como entregar**: executável e pasta, link, arquivo;
  - **o que fica fora** desta etapa.
- No fim, apresente uma **síntese numerada** e espere a confirmação (“Confirmo”, “Aprovado”). Propostas suas ficam identificadas como proposta.
- Ao confirmar, registre em `decisoes.md` a data, a justificativa e a citação literal da resposta. Se a etapa substituir uma decisão, diga qual e por quê.

## 4. Visual (só quando houver tela nova)
- Antes de escrever código, mostre de duas a três direções em modelos visuais, coerentes com a identidade já aprovada no projeto, se houver.
- O usuário escolhe e ajusta. A aprovação estética final é sempre dele, depois da entrega.

## 5. Implementação e entrega
- Só depois da síntese confirmada (e do visual, quando houver). Se o projeto tem repositório, preserve as alterações existentes antes de começar.
- Desvio de uma decisão confirmada fica como proposta em `plano.md` até o usuário responder.
- Teste e entregue como combinado no passo 3. Informe o que foi verificado, o que não foi e, se houver executável, a pasta exata.
- Atualize os registros e envie o backup, conforme "Antes de encerrar a tarefa" no `AGENTS.md` da vault.
- Quando o mesmo processo de teste ou entrega se repetir, proponha transformá-lo em skills próprias do projeto (prefixo com o nome do projeto) e cite-as na nota de regras dele.

## Cuidados
- Não registre como feito algo apenas proposto ou configurado sem teste.
- Com a Alethe ligada, a entrevista e a síntese ficam com o líder. Só as unidades já definidas vão para workers.
