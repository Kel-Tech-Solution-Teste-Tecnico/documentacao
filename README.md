# Projeto Name

Descrição

## Escopo

O escopo define os limites e objetivos do projeto, estabelecendo o que será ou não implementado. No Âmago, ele orienta o desenvolvimento conforme as necessidades dos vendedores e consumidores envolvidos na construção do projeto. Dessa forma, cada iteração representa uma fase com evoluções específicas no sistema. Veja a seguir o escopo de cada interação:

### Interação I


## Processo

O projeto segue um processo de software inspirado no Processo Unificado Racional ([RUP – Rational Unified Process](https://www.facom.ufu.br/~william/Disciplinas%202018-2/BSI-GSI030-EngenhariaSoftware/Livro/engenhariaSoftwareSommerville.pdf)), aplicando um ciclo de vida interativo e incremental. A seguir, apresenta-se uma matriz de atividades que relaciona algumas fases adotadas do RUP com os principais artefatos de entrada e saída, ações executadas e os papéis responsáveis por cada etapa. Essa estrutura contribui para a rastreabilidade do processo de desenvolvimento de software, tornando mais claro quem faz o quê, quando e com base em quais artefatos.

| **Fase**   | **Artefato de Entrada**    | **Ação**    | **Artefato de Saída**         | **Papel Responsável**        |
| ---------- | -------------------------- | ----------- | ----------------------------- | ---------------------------- |
| Concepção  | Contexto                   | Definir     | Escopo                        | Product Owner(P.O)           |
| Concepção  | Escopo                     | Especificar | Documento de Requisitos (PRD) | P.O e Engenheiro de Software |
| Elaboração | PRD                        | Escrever    | Histórias de Usuário          | P.O                          |
| Elaboração | Histórias de Usuário e PRD | Planejar    | Backlog do Produto            | P.O e Engenheiro de Software |
| Construção | Backlog do Produto         | Desenvolver | Produto Incrementado          | Engenheiro de Software       |
| Construção | Produto Incrementado       | Testar      | Produto Ajustado              | Engenheiro de Software       |
| Tansição   | Produto Ajustado           | Avaliar     | Produto Finalizado            | P.O                          |

## Atividades 

As atividades representam as tarefas realizadas durante o desenvolvimento do sistema, como correções, melhorias ou novas funcionalidades. Neste contexto, a classificação das atividades permite controlar e rastrear as mudanças feitas no código, relacionando cada uma aos requisitos do projeto. Dessa forma, a categorização evolutiva em conjunto com a padronização de issues e rastreabilidade commits, torna possível a garantia entre o que foi planejado e o que foi implementado, promovendo qualidade e transparência no processo.

### Classificação das Atividade Conforme a Evolução de Código

Cada atividade do projeto é classificada conforme sua natureza, o que ajuda a identificar o tipo de evolução do sistema e manter a rastreabilidade com os requisitos. Os tipos são:

| **Tipo de Evolução** | **Descrição**                                                                      | **Momento**                                                                          | **Prefixo do Commit** | **Rastreabilidade**                                                                                                    |
| -------------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | --------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Evolutiva            | Adiciona funcionalidades novas ou melhorias planejadas                             | Quando a funcionalidade já estava prevista na interação                              | feat                  | Sempre referenciando o commit com o prefixo feat e a identificação da issue. Exemplo: "feat #01: ..."         |
| Corretiva            | Corrige erros, falhas de lógica ou validações que impedem o funcionamento adequado | Quando é necessário consertar algo que foi implementado incorretamente ou contém bug | fix                   | Sempre referenciando o commit com o prefixo fix e a identificação da issue. Exemplo: "fix #02: ..."            |
| Adaptativa           | Altera o sistema para se adaptar a mudanças externas                               | Quando há necessidade de ajustes técnicos que não alteram a lógica funcional         | refactor              | Sempre referenciando o commit com o prefixo refactor e a identificação da issue. Exemplo: "refactor #03: ..." |

### Estrutura Padrão das Atividades/Issues

As issues são usadas para planejar, distribuir e acompanhar as atividades do projeto. Elas estão localizadas no **[_Project (projeto)_](https://github.com/orgs/Kel-Tech-Solution-Teste-Tecnico/projects/1)** desta organização e cada uma deve conter informações completas para garantir entendimento e rastreabilidade. Neste contexto, o modelo adotado de issue/atividade segue o consecutivo padrão abaixo:

- **Identificador:** número de identificação de cada issue. É gerado automaticamente;
- **Título:** curto, descrevendo o que deve ser feito e referenciando o repositório para a sua construção;
- **Descrição:** estruturada com:
    - **História de Usuário**:  uma história de usuário, no formato **Como** [papel] **Quero** [ação], **Para** [finalidade];
    - **Requisitos Associados**: associação de requisitos na atividade, que podem ser **Requisitos Funcionais (RF)**, **Requisitos Não Funcioanis (RNF)** e **Regras de Negócio**;
    - **Complemento:** campo opcional com informações extras e/ou links de outros artefatos para orientar o realizador da tarefa.
- **Rótulos (Labels)**: Marcadores utilizados para classificar ou agrupar as atividades;
- **Prioridade (Priority)**: nível de urgência classificadas em:
    - **P0:** crítica e bloqueia outras funcionalidades;
    - **P1:** importante, mas não bloqueia outras funcionalidades;
    - **P2:** pode ser feita depois, sem impacto imediato.
- **Responsável (Assignees)**: membro(s) atribuídos para executar a tarefa;
- **Repositório (Repository)**: repositório associado à issue;
- **Iteração (Iteration):** a qual iteração a tarefa pertence.


## Controle de Mudanças de Código

O controle de mudanças é um processo estruturado para gerenciar modificações no código-fonte de um projeto, garantindo estabilidade, rastreabilidade e qualidade. Ele define como as alterações são desenvolvidas, testadas e promovidas até a produção, minimizando riscos e falhas. Dessa forma, utilizamos Git como sistema de controle de versão distribuído e GitHub como plataforma para gerenciamento de repositórios, revisão de código e colaboração entre desenvolvedores.

### Fluxo de linhas:

- **Branches das issues**:
    - Linhas responsáveis pelo de desenvolvimento, criada a partir da branch "dev";
    - A branch deve começar com o prefixo "feat/", depois o nome da funcionalidade que será tratada. Exemplo: feat/store;
    - Cada issue terá sua própria branch para desenvolvimento;
    - Após a implementação, deve-se abrir um Pull Request para a branch "dev";
    
- **Homologação**:
    - Linha chamada "dev" responsável por validar as branches criadas antes de ser envida para a produção;
    - Linha criada a partir da branch "main";
    - Caso todas as branches criadas sejam validadas com sucesso nesta linha, haverá um Pull Request para a linha de produção (main);
    - Caso exista algum erro ao realizar a validação de alguma branch enviada para essa linha, deverá ser criada branches de correção (hotfix) até que tudo esteja validado com sucesso.

- **Produção**:
    - Linha responsável por receber códigos validados pela branch de homologação (dev) e por subir o sistema para o servidor de produção automaticamente, quando houver um ambiete preparado;
    - Se trata da linha chamada "main";
    - Caso exista algum erro no sistema em produção, será feita a restauração do "commit" anterior, caso exista versões antigas, e deverá ser criadas branches de correção (hotfix).
    
- **Branches das correções de erro:**
    - Linha responsável pela correção de erros verificada na branch de homologação ou produção;
    - A branch deve começar com o prefixo "hotfix/", depois o nome da funcionalidade que será tratada. Exemplo: hotfix/fix-login-authorization;
    - Se um erro for identificado nas validações da linha "dev" ou na "main", uma nova branch de hotfix será criada a partir dela;
    - Cada correção será implementada, testada e, se aprovada, integrada novamente à dev, assim como nas branches de issues.

### Diagrama de Fluxo:

O fluxo ilustrado abaixo demonstrando as linhas de desenvolvimento (branches das issues, representadas por "feat"), homologação ("dev"), produção ("main") e correções ("hotfix"). Esse diagrama reforça a importância de seguir o processo para garantir a qualidade e integridade do código.

[![Fluxo de Mudanças](https://i.postimg.cc/26zB50dN/Fluxo-de-mudan-as-2.png)](https://postimg.cc/CZQKPH6c)