# Plataforma de Extensão Universitária — UFRGS

Protótipo de alta fidelidade de uma plataforma que centraliza a divulgação, a candidatura e a seleção em atividades de extensão universitária. O projeto foi desenvolvido em grupo para a disciplina INF01127 (Engenharia de Software) da UFRGS.

**[Acessar o protótipo](https://SEU-USUARIO.github.io/SEU-REPOSITORIO/)**

> Protótipo acadêmico. O login com cartão UFRGS, o sistema de registro de extensão e o envio de e-mails são simulados. Não use credenciais reais.

---

## O problema

A curricularização da extensão (Resolução CNE/CES nº 7/2018) exige que pelo menos 10% da carga horária da graduação seja cumprida em atividades de extensão. Hoje as informações sobre essas atividades estão dispersas:

- **Estudantes** não têm um lugar único para encontrar atividades compatíveis com seu curso, horário e interesse.
- **Coordenadores** divulgam ações e recebem candidaturas por e-mail, formulários e redes sociais, sem controle de vagas nem histórico.
- **A comunidade externa**, que é o público atendido por muitas ações, raramente sabe o que está aberto ao público.

## O que o protótipo propõe

Uma plataforma única com três perfis:

| Perfil | O que faz |
|---|---|
| Visitante / comunidade externa | Busca e filtra atividades sem login, cria conta e se inscreve como beneficiário |
| Estudante | Entra com o cartão UFRGS, candidata-se como voluntário ou beneficiário, acompanha o resultado e emite o certificado |
| Coordenador | Cadastra atividades a partir do código de registro oficial, define turmas e vagas e seleciona os candidatos |

A principal decisão de projeto foi trocar a inscrição por ordem de chegada pela **candidatura com seleção pelo coordenador**. As vagas limitam quantos candidatos podem ser aceitos, não quantos podem se candidatar. Isso elimina a disputa por vagas em tempo real e reflete como os projetos de extensão funcionam na prática.

## Como testar

Na tela de login há cartões de teste (senha `ufrgs123`). A barra "Modo Demo", no topo, também troca de perfil com um clique.

| Para ver | Use |
|---|---|
| Candidatura, cancelamento e certificado | Estudante `00000001` → Minhas Inscrições |
| Regras de elegibilidade | Cartões `00000002` a `00000007` |
| Cadastro com verificação do registro oficial | Coordenador `00000008` → Nova Atividade → código `64020` |
| Seleção de candidatos | Coordenador → Minhas Atividades → "cand." |

Os dados ficam em memória: ao recarregar a página, o protótipo volta ao estado inicial.

## Requisitos

A especificação tem 26 requisitos funcionais (RF), 28 regras de negócio (RN) e 4 requisitos não funcionais (RNF). Os principais:

**Funcionais**
- **Busca e catálogo (RF01, RF02):** busca por texto e filtros por área, formato, carga horária, forma de participação e status, sem login.
- **Cadastro de atividades (RF06, RF16, RF22–RF26):** turmas com horário próprio por dia da semana, inscrição por período fixo, fluxo contínuo ou só divulgação, e modalidades e termos do catálogo oficial da PROREXT.
- **Candidatura e seleção (RF03, RF08, RF14, RF17):** escolha de turma, cancelamento até o prazo e aceite ou rejeição pelo coordenador.
- **Formas de participação (RF19–RF21):** voluntário e beneficiário, com vagas, formulário, carga horária e certificado próprios.
- **Notificações e certificado (RF05, RF15):** e-mail e notificação na plataforma; certificado em PDF.

**Regras de negócio** (exemplos)
- Seleção só entre o encerramento das inscrições e o início da execução (RN12).
- Prorrogação de prazo limitada a 2 vezes de até 7 dias, com notificação (RN10).
- Candidaturas sem decisão são encerradas como não selecionadas; não há aceite automático (RN20).
- Voluntário só com vínculo ativo de aluno; elegibilidade validada por vínculo, idade e escolaridade (RN22, RN25).
- Dados pessoais conforme a LGPD, inclusive para menores de idade (RN23, RN24).
- Publicação só com código de ação aprovado no sistema oficial de extensão (RN05).

**Não funcionais**
- Layout responsivo, verificado em 360, 414 e 768 px (RNF01).
- Consulta pública sem login (RNF02).

Fora do escopo do protótipo: limite de atividades por estudante (RN03), atividades pagas (RN06), metas de desempenho (RNF03) e auditoria de acessibilidade (RNF04).

## Processo

O desenvolvimento foi **iterativo e incremental, com prototipagem evolutiva**, em 15 iterações. Cada iteração seguiu o mesmo ciclo:

1. **Análise:** testar o protótipo ou compará-lo com fontes reais, como cinco atividades do catálogo oficial da PROREXT.
2. **Decisão:** registrar a questão em aberto, discutir alternativas e decidir como RF ou RN.
3. **Especificação:** atualizar o documento de requisitos, que foi a fonte única da verdade.
4. **Implementação:** aplicar a decisão no protótipo.
5. **Verificação:** rodar testes automatizados (Playwright) da nova regra e de regressão, em desktop e celular.
6. **Registro:** publicar a versão e registrar a iteração no histórico de mudanças.

Exemplos de decisões que surgiram durante o processo:
- A comparação com o catálogo real mostrou atividades de **fluxo contínuo** e de **divulgação apenas**, que a especificação inicial não previa.
- O teste do formulário revelou que turmas precisavam de **horários diferentes por dia**, inclusive aos domingos, e de datas dentro do período de execução.
- A análise dos perfis separou **voluntário** (equipe executora, exige vínculo ativo) de **beneficiário** (público atendido, interno ou externo).

## Tecnologia e uso de IA

- Aplicação de página única em HTML, CSS e JavaScript, sem dependências externas, publicada no GitHub Pages.
- Organização em camadas: interface, regras de negócio e dados, com serviços externos simulados (API da UFRGS, registro de extensão, e-mail).
- Testes automatizados de ponta a ponta com Playwright.

A implementação foi feita com apoio de IA generativa (Claude, da Anthropic), a partir dos requisitos e das decisões do grupo. O foco do trabalho humano foi a engenharia de requisitos: levantar o problema, tomar e registrar as decisões de produto, comparar com o sistema real, revisar o comportamento do protótipo e validar cada iteração.

## Equipe

Projeto do grupo da disciplina INF01127 — Engenharia de Software, Instituto de Informática, UFRGS, 2026.
<!-- Adicione aqui os nomes e links (GitHub/LinkedIn) dos integrantes -->
