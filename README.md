# Introdução

Neste workshop abordaremos a ferramenta SonarQube mais focada em sua utilização geral e na verificação de métricas.

O workshop completo contendo informações mais técnicas como instalação, configuração, informações de código limpo e etc podem ser acessado neste [link](https://github.com/GladsonBruno/SonarQube).



# O que é SonarQube?

O SonarQube é uma plataforma de código aberto desenvolvida pela SonarSource, ele é usado por equipes de desenvolvimento para o gerenciamento da qualidade de código fonte.

O SonarQube fornece análise e integração totalmente automatizadas com Maven, Ant, Gradle, MSBuild e ferramentas de integração contínua ( Atlassian Bamboo, Jenkins, Hudson, etc).

Atualmente a versão gratuita do SonarQube (Community Edition) fornece suporte para 15 linguagens de programação distintas.



# Como o SonarQube funciona?

O SonarQube possui uma arquitetura bastante simples e flexível que é constituída por três componentes:

- Um conjunto de analisadores de código fonte que são acionados por demanda.

- Um banco de dados para mantêm os resultados de análises.

- Uma ferramenta *Web* para exibir painéis de qualidade de código sobre projetos, bugs, vulnerabilidades e etc.

  

Com esses componentes o SonarQube embarca as melhores ferramentas para analisar violações de regras de qualidade, bugs em potencial, cobertura de testes de unidade, violações de segurança, entre outros.



# Métricas

O SonarQube oferece uma série de métricas sobre a qualidade do código, entre elas estão:

- Complexidade (ciclomática e cognitiva)

- Código duplicado

- Quantidade de Problemas

- Tamanho (quantidade de linhas de código, número de classes, etc…)

- Cobertura de testes

- Índice de Manutenibilidade, Confiabilidade e Segurança






# Alguns conceitos do SonarQube 

Ao abrirmos o SonarQube pela primeira vez nos deparamos com uma séries de termos desconhecidos até o momento, neste tópico abordaremos cada um deles.



## Rules (Regras)

O SonarQube se baseia em regras pré-definidas para analisar o código. Uma regra ou Rule é uma boa prática e cada linguagem possui um grupo de regras relacionadas. Toda a regra possui uma descrição, normalmente, com exemplo de código e links para descrições mais detalhadas, o que ajuda o desenvolvedor a entender e resolver o problema relacionado, como mostra o exemplo abaixo:

<img src="imagens/exemplo-5.png"/>

Todas as regras pré-definidas no SonarQube podem ser acessadas através do menu **Rules**.





## Issues (Problemas)

Toda vez que um código quebra uma regra, uma *Issue* é gerada.

No menu Issues podemos verificar todas as Issues geradas de todos os projetos registrados no SonarQube.

Abaixo um exemplo da tela de Issues.

<img src="imagens/exemplo-5-1.png"/>



As *Issues* estão divididas nas seguintes categorias: 

<img src="imagens/exemplo-6.png"/>



- **Code Smells:** São problemas relacionados a manutenibilidade do código. Deixar isso como está significa que, na melhor das hipóteses, os desenvolvedores terão mais dificuldade do que deveriam para fazer alterações no código. Na pior das hipóteses, eles ficarão tão confusos com o estado do código que introduzirão mais erros à medida que fizerem alterações.

- **Bugs:** itens que representam erros no código que, se ainda não aconteceram em produção, provavelmente acontecerão, e no pior momento possível. Problemas desta categoria precisam ser corrigidos.

- **Vulnerabilities (Vulnerabilidades):** são fraquezas ou brechas de segurança na aplicação.

- Além dessas 3 categorias principais podemos ter também uma outra categoria chamada de **Security Hotspot** que se trata de uma vulnerabilidade referente a um código sensível à segurança da aplicação no qual o desenvolvedor precisa revisar. Após a revisão será definido se o ponto em específico é realmente uma vulnerabilidade de segurança a ser tratada.

  Para compreender detalhadamente sobre **Security Hotspots** acesse este [link]( https://docs.sonarqube.org/latest/user-guide/security-hotspots/ ).

  

As *Issues* também são classificadas por severidade, conforme a tabela abaixo: 

<img src="imagens/exemplo-7.png"/>



 Existem sete coisas diferentes que você pode fazer com uma *Issue* (além de corrigi-la!) 

<img src="imagens/exemplo-8.png"/>

- **Confirm (Confirmar):** ao confirmar um problema, você está basicamente dizendo “Sim, isso é um problema”. Ao fazê-lo, ele sai do status “Aberto” para “Confirmado”.
- **False Positive (Falso Positivo):** olhando para a questão em contexto, você percebe que, por qualquer motivo, esse problema não é realmente um problema. Então você marca como falso positivo e segue em frente.
- **Won’t Fix (Não será corrigido):** olhando para o problema no contexto, você percebe que, embora seja um problema válido, não é um problema que realmente precisa ser corrigido. Em outras palavras, representa dívida técnica aceita.
- **Change Severity (Mudar severidade):** este é o meio termo entre as duas opções anteriores. Sim, é um problema, mas não é um problema tão ruim quanto a gravidade padrão da regra diz. Ou talvez seja muito pior. De qualquer forma, você ajusta a gravidade do problema para adequá-lo ao que você acha correto.
- **Resolve (Resolver):** se você acha que resolveu um problema em aberto, pode escolher esta opção. Se você está certo, a próxima análise irá movê-lo para o status fechado. Se você estiver errado, o status será reaberto.
- **Assign (Atribuir):** depois que os problemas passarem pela revisão técnica, é hora de decidir quem vai lidar com eles. Por padrão, eles são atribuídos ao último *committer* no momento em que o problema é levantado, mas você pode reatribuí-lo a si mesmo ou a outra pessoa. O responsável receberá uma notificação por e-mail da tarefa se ele se inscreveu para notificações, e a atribuição será exibida em todos os lugares em que o problema for exibido.
- **Comment (Registrar comentário):** a qualquer momento durante o ciclo de vida de um problema, você pode registrar um comentário sobre ele. Comentários são exibidos nos detalhes do problema. Você pode editar ou excluir os comentários que você fez.





## Quality Profile (Perfil de Qualidade)

As *Issues* são geradas a partir das regras pré-definidas, que, por sua vez, estão relacionadas a um **Quality Profile (Perfil de Qualidade)**. Cada linguagem possui um perfil de qualidade associado. Além disso, o SonarQube permite extensão de perfis através de herança.

Somente usuários com permissão podem editar um perfil de qualidade

Para acessar os perfis de qualidade pré-definidos pelo SonarQube você pode acessar o menu **Quality Profiles**.

Um exemplo desta tela seria:

<img src="imagens/exemplo-9.png"/>





## Quality Gate (Meta de Qualidade)

Um *Quality Gate* (Meta de Qualidade) é uma meta que deve ser atingida antes que uma build possa ser liberada. Por exemplo:

**Posso liberar uma build hoje? Sim, desde que:**

- Os índices de Confiabilidade, Segurança e Manutenibilidade do novo código sejam = A

- 90% dos testes unitário passarem com sucesso

  

Somente usuários com permissão podem editar um Quality Gate.



Os Quality Gate pré definidos pelo SonarQube podem ser acessados através do menu **Quality Gates**.

Um exemplo desta tela seria:

<img src="imagens/exemplo-10.png"/>



## Exercicio 1

Crie um Quality Gate chamado QualityGateExemplo com as seguintes condições de erro:

* Bugs > 0
* Issues > 5
* Condition Coverage < 80%
* Code Smells > 5000
* Vulnerabilities > 5



## Exercício 2
Atualize o Quality Gate criado no exercício anterior adicionando as seguintes condições de erro

* Coverage on New Code(Cobertura de código novo) < 80.0%
* Duplicated Lines on New Code(Linhas duplicadas no código novo) > 3.0%
* Maintainability Rating on New Code(Classificação da manutenção do novo código) é pior do que A
* Reliability Rating on New Code(Classificação de confiabilidade do novo código) é pior do que A
* Security Rating on New Code(Classificação de segurança do novo código) é pior do que A
* New Code Smells > 5
* New Issues > 5 
* New Bugs > 0
* New Vulnerabilities > 0



## Exercício 3
Crie um Quality Gate a partir de uma cópia do Quality Gate padrão SonarWay e atribua as seguintes condições de erro a ele:

* New Code Smells > 5
* New Issues > 5 
* New Bugs > 0
* New Vulnerabilities > 0



## Exercício 4
Para finalizarmos com os Quality Gates delete os 2 Quality Gates que criamos nos exercícios anteriores.



# Acessando as informações e métricas de nossos projetos



## Menu Projects

Para verificar as métricas resumidas de nossos projetos podemos acessar o menu **Projects** onde veremos algo como o exemplo abaixo:

<img src="imagens/exemplo-4.png"/>



Podemos observar que o projeto de exemplo possui 1 bug, 3 vulnerabilidades, 5 Code Smells, 0% de cobertura de código e 0.0% de duplicatas.

Podemos ver a nota de qualidade atribuída as categorias de Bugs, Vulnerabilidades e Code Smells, além disso podemos ver ao lado direito do nome do projeto o status do projeto referente ao Quality Gate pré definido pelo SonarQube.

Para ter uma visão mais detalhada clique no projeto **API de Produtos**.

Ao fazermos isso seremos redirecionados a página detalhada de métricas de nosso projeto conforme o exemplo abaixo:

<img src="imagens/exemplo-11.png"/>



nos próximos tópicos abordaremos cada um dos Sub menus do detalhamento de um projeto.





## Sub menu Overview

Apresenta uma visão geral de nosso projeto.





## Sub menu Issues

Apresenta as informações de Issues do projeto selecionado.





## Sub menu Measures

O menu **Measures** apresenta algumas medições do projeto em uma visão geral e em outras visões conforme podemos observar neste exemplo:

<img src="imagens/exemplo-12.png"/>



Além da visão geral das medições do projeto também possuímos medições de:

* **Reliability (Confiabilidade)**: Nesta categoria são marcados alguns pontos a nível de código no qual você poderá obterá um comportamento diferente do esperado.

* **Security (Segurança)**: Nesta categoria são marcados a nível de código possíveis pontos fracos para hackers. 

* **Maintainability (Manutenibilidade)**: Nesta categoria são marcados a nível de código pontos da aplicação no qual a manutenibilidade será mais difícil do que deveria.

* **Coverage (Cobertura)**: Nesta categoria serão marcados a nível de código pontos da aplicação que não possuem cobertura de testes automatizados.

* **Duplications (Duplicatas)**: Nesta categoria são marcados a nível de código fonte pontos da aplicação destacados como duplicatas dentro da aplicação e a densidade dessas duplicatas de código em toda a aplicação.

* **Size (Tamanho)**: Fornece uma medição de Linhas de código, Métodos, Funções, Classes, Arquivos, Linhas comentadas e porcentagem de comentários do projeto.

  Exemplo:

  <img src="imagens/exemplo-13.png" style="float: left"/>

* **Complexity (Complexidade)**: Quão simples ou complicado é o fluxo de controle do aplicativo. 
  Esta categoria fornece a medição de **Complexidade Ciclomática** e **Complexidade Cognitiva**.
  A **complexidade ciclomática** mede o número mínimo de casos de teste necessários para a cobertura total do teste. 
  A **complexidade cognitiva** é uma medida de quão difícil é de se entender o aplicativo.

  Exemplo:

  <img src="imagens/exemplo-14.png" style="float: left"/>

  

* **Issues (Problemas)**: Esta categoria fornece uma visão geral sobre os Issues do projeto e seu status atual.

  Exemplo:

  <img src="imagens/exemplo-15.png" style="float: left"/>





## Sub menu Code

Fornece a visão do código do aplicativo e uma medição de:

* Linha de código
* Bugs
* Vulnerabilidades
* Code Smells
* Security Hotspots
* Cobertura de código
* Duplicatas



Exemplo:

<img src="imagens/exemplo-16.png"/>





## Sub menu Activity

Fornece uma visão geral do histórico de atividade do projeto a cada vez que o mesmo é analisado pelo SonarQube.

Nele podemos ver um histórico do projeto referente a melhorias ou pioras de acordo com as métricas do SonarQube como aumento ou diminiuição de Bugs, Code Smells e etc.

Exemplo:

<img src="imagens/exemplo-17.png"/>





## Sub menu Administration

Neste sub menu existem uma série de outros sub menus relacionados a administração do projeto no SonarQube.

Exemplo:

<img src="imagens/exemplo-18.png" style="float: left"/>

Podemos observar que neste sub menu possuímos outros sub menus referentes a:

* **General Settings**: Configurações gerais do projeto.

* **Quality Profiles**: Permite escolher qual perfil estará associado ao projeto, idioma por idioma.

* **Quality Gate**: Permite escolher qual Quality Gate estará associado ao projeto.

* **Custom Measures (Medições personalizadas)**: Permite atualizar os valores das métricas personalizadas para este projeto. As alterações entrarão em vigor na próxima análise do projeto. Métricas personalizadas devem ser criadas em nível global.

  Uma observação importante é que este menu está marcado para remoção em versões futuras do SonarQube.

* **Links**: Permite editar alguns links associados ao projeto.

* **Permissions (Permissões)**: Permite conceder e revogar permissões no nível do projeto. As permissões podem ser concedidas a grupos ou usuários individuais.

* **Background Tasks (Tarefas de segundo plano)**: Esta página permite o monitoramento da fila de tarefas em execução de forma assíncrona no servidor do SonarQube. Também fornece acesso ao histórico de tarefas concluídas e seu status. O processamento do relatório de análise é o tipo mais comum de tarefa em segundo plano.

* **Update Key**: Permite alterar a chave de identificação que definimos para o projeto.

* **Webhooks**: Os webhooks são usados para notificar serviços externos quando uma análise de projeto é feita. Uma solicitação HTTP POST incluindo uma carga JSON é enviada para cada um dos URLs fornecidos.

* **Deletion (Deleção)**: Permite realizar a deleção do projeto no SonarQube.



# Visão geral menu Administration(Administração)

Neste tópico veremos uma visão geral do que o menu Administração tem a oferecer.

Ao acessarmos o menu adminstração veremos algo semelhante a isso:

<img src="imagens/exemplo-19.png"/>



Observe que ao acessar o menu administração somos apresentados a outros 5 menus, sendo eles:

* Configuration
* Security
* Projects
* System
* Marketplace



Abordaremos cada um deles nos próximos tópicos.





## Menu Configuration e seus sub menus

O menu **Configuration** possui alguns submenus que fornecem as seguinte funcionalidades:

* **General Settings**: Configurações global da instância SonarQube

* **Encryption**: Fornece a possibilidade de gerar chaves secretas no SonarQube.

* **Custom Metrics**: Fornece a possibilidade de criar métrica personalizadas para todos os projetos do SonarQube





## Menu Security e seus sub menus

O menu **Security** possui alguns submenus que fornecem as seguinte funcionalidades:

* **Users**: Permite criar e administrar usuários individuais no SonarQube.
* **Groups**: Permite criar e administrar grupos de usuários no SonarQube.
* **Global Permissions**: Permite conceder e revogar permissões para fazer alterações a nível global. Essas permissões incluem editar perfis de qualidade, executar análises e executar a administração global do sistema.
* **Permission Templates**: Permite gerenciar templates de permissões para projetos.





## Menu Projects e seus sub menus

O menu **Projects** referente ao menu **Administration** possui alguns submenus que fornecem as seguinte funcionalidades:

* **Management**: Permite gerenciar todos os projetos cadastrados no SonarQube.

* **Background Tasks (Tarefas de segundo plano)**: Permite o monitoramento global da fila de tarefas em execução de forma assíncrona do servidor do SonarQube. Também fornece acesso ao histórico de tarefas concluídas e seu status. O processamento do relatório de análise é o tipo mais comum de tarefa em segundo plano.





## Menu System

Fornece uma série de informações sobre o servidor SonarQube, alem de possibilitar o download de logs e informações do servidor.

Neste menu também é possível reiniciar o servidor do SonarQube.

Exemplo:

<img src="imagens/exemplo-20.png"/>





## Menu Marketplace

Este menu fornece a possibilidade de realizar o download de plugins para o SonarQube.

Basta pesquisar e instalar o plugin.

Exemplo:

<img src="imagens/exemplo-21.png"/>

