# questions-about-frontend

Perguntas retiradas do repo: https://github.com/rubenmarcus/120-perguntas-frontend.

Respondendo todas as perguntas com base nas minhas experiências e testes como desenvolvedor front End. Dependendo da pergunta estarei acrescentando na resposta algumas experiências da minha vida profissional.

1.`O que é SQL injection?`<br/>

SQL Injection (SQLI) é um ataque geralmente focado na web que tem como objetivo comprometer o banco de dados do sistema através de sentenças SQL. Esse foi um dos primeiros assuntos abordados sobre segurança quando comecei minha carrreira, pois com pouco conhecimento já é possivel comprometer e obter informações de um recurso com essa falha. Hoje ainda temos muito sistemas legados com esse tipo de brecha.

exemplo: 
Original: .php?type=books
test SQLI: .php?type=3-1 

Nesse exemplo estou alterando o parâmetro para realizar uma operação, se essa operação foi realizada então teriamos uma vunerabilidade de SQLI sendo possível aprofundar e explorar ainda mais essa falha.

exemplo:
/products?category=Gifts'--

em alguns sgdbs é utilizado '-- para comentários, sendo assim explorando essa vunebilidade passando esse comentario no parâmetros teríamos a situação onde o restante da query é ignorado.

SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1

Resumindo, essa query está sendo montanda diretamente com o parâmetro recebido pelo usuário.

Toda e qualquer dado vindo de fora ou client deverá ser sanitizado 

2.`O que é escopo em JavaScript?`<br/>

Escopos no JS pode ser deinifido como a visibilidade ou disponibilidade de uma variável, temos três tipos escopos:

Esses três escopos não são válidos para o var e sim para o let e const introduzidos no ES6. 

Escopo de funções: Em uma função, toda variável declarada só poderá ser acessada dentro do escopo dessa função. Caso a variável fora do escopo de função for chamada ocorrera um erro de que essa variável não foi declarada. Uma caracteriza interessante desse escopo é que podemos ter variáveis com mesmo nome em diferentes escopos.

Escopo de blocos: O JS caracteriza como bloco tudo que estiver entre chaves, sendo assim variável criada dentro de um bloco como por exemplo um for, a variável não é válida fora desse bloco. 

Escopo léxico: nesse tipo de escopo podemos acessar variaveis declaradas dentro de funções alinhadas, ou seja, funções dentro de funções, uma função com uma variável declarada, caso essa função tenha outras funções internas, essas funções estao aptas para acessar a variavel declarada no primero nível, termo bem utilizado para esse conceito Function Nesting, bastante utilizada na programação funcional.

extra: para conseguir que o var tenha algum tipo de escopo podemos utilizar variável dentro uma função retornando o valor, assim essa variável passa a ter um escopo função

3.`Explique o CSS “box model” e os componentes de layout que o compõem.`<br/>

Uma das primeiras coisas que aprendi quando comecei a estudar css é o box model. 

box model é um conjunto de propriedades que juntas formam um caixa, então todo elemento html renderizado pelo browser tem um box model e com css podemos resetar ou alterar essa box model resultando na forma como é renderizado pelo browser, temos alguns elementos bem importantes no entendimento do box model: conteúdo, espaçamento, bordas e margens.

extra: ao longo da minha jornada com css uma ferramenta bem interessante pra entender e resolver problemas de box model é saber debugar o estado atual daquele elemento na devtools, temos um box model visual e conseguimos saber exatamente que tipo de valor está sendo atribuído para qualquer propriedade daquele elemento.

4.`Como JavaScript e jQuery são diferentes?`<br/>

JavaScript é uma linguagem de programação que pode ser utilizada tanto no back quanto no front end. Já o Jquery é uma biblioteca criada em cima do JS para facilitar no processo de desenvolvimento. Temos diversas bibliotecas com objetivos diferentes mas o Jquery foi criado para facilitar a manipulação no DOM.

extra: com a evolução da web e da própria linguagem Javascript, muito do que se via abstraído na lib Jquery vou sendo implementada nativamente no JS.
exemplo com Jquery: $("#about").hasClass("opened");
exemplo com JS implementado posteriormente: about.classList.contains("anyClass")

5.`O que é é um Callback Hell?`<br/>

callback é uma convensão do JS sobre funções que usam resultado de outras funções para fazer algo, isso também é muito comum quando lidamos com assincronismo, já que precisamos esperar um resultado para seguir com alguma função, nesse contexto surgem os callbacks hell.

Exemplo: temos uma função que faz uma chamada assíncrona para carregar algum dado, e esse dado vai ser usado como argumento para algumas funções também assíncronas, e dado um momento que uma função precisa esperar o resultado acabávamos tendo que fazer nesting de funções para ir utilizando os resultado conforme forem ficando disponível, resultando em uma função com muitas funções de difícil leitura e compreensão. 

Todo esse contexto foi resolvido com a chegada das Promisses, sendo basicamente um recurso para lidar melhor com programação assyncronica. Uma Promisse é iniciada como uma função com duas instruções básicas, resolve e reject e a palavra reservada Promise. No Resolve callback só é executado quando temos uma resposta válida e o reject quando temos um erro. Também temos a opções de usar função utilizando a palavra reservada await na chamada da promisse, e a diferença entre os dois é que com await o JS em tempo de execução vai esperar até que a promisse seja resolvida e a proposta do then é continuar a execução até que tenhamos uma resposta para seguir com callback. Quando temos um cenário com várias promssies podemos utilizar também o promisseAll. Com isso temos mais organização e legibilidade do código e não mais toda aquela tripa de funções em funções.

6.`O que é Cross-Site Scripting (XSS)?`<br/>

XSS é um ataque a sistemas web que tem como objetivo inserir código malicioso para obter informações ou orquestrar informações sendo mais comum utilizado para sequestrar sessões, tokens para obter ou elevar acessos. Existem três principais tipos de ataque de injeção de script:

Persistente: O script injetado pelo atacante fica alojado de forma permanente no servidor de destino. O usuário pode acionar a carga apenas por navegar num website infectado; portanto, qualquer usuário pode executar o código malicioso sem nenhuma ação específica. Esse é um tipo bastante perigoso de ataque, pois o código pode estar alojado em diversos destinos, como campos de comentário, base de dados etc. Com isso o ataque pode inserir um código que sequestre toda a sessão do usuario e envie para outro host.

Não persistente/Refletido: Neste caso, o script não estará alojado em um servidor de destino e por isso precisará ser entregue para cada vítima. Isso pode acontecer por várias formas de engenharia social, por exemplo uma mensagem de erro ou um resultado de busca. Uma forma frequente será um link distribuído por meio de esquemas de phishing. Ao acionar o servidor, por meio do link, o script será refletido e executado no navegador. Esta técnica é a mais frequente.

Baseado em DOM: O terceiro tipo de ataque XSS explora o Document Object Model (DOM), que é a interface que define a leitura de HTML e XML no navegador. O script é capaz de alterar as propriedades das aplicações que executam estes tipos de extensões diretamente no navegador, portanto sem necessidade de interação com o servidor para performar o ataque. Neste caso, a falha está na validação do código HTML ou XML no navegador.

Para evitar esse tipo de ataque é sempre interresante validar e sanitizar todas as entradas de dados, tanto no back quanto no front end. Encondificar dados a serem transmitidos e utilizar CDNs.

O que é o CDN?
O CDN é o Content Distribution Network, ou seja, uma Rede de Distribuição de Conteúdo.

Seu objetivo é ter uma rede de servidores que armazenam réplicas do conteúdo, de modo a entregá-los para as regiões mais próximas. Além de ser uma solução muito mais rápida e eficaz, deixa o seu conteúdo bem mais seguro.

Sem essa opção, o seu conteúdo está totalmente exposto, já que cada usuário interage diretamente com ele. Por outro lado, com o CDN, a arquitetura de servidores é mais forte e mais bem distribuída, descentralizando e limitando o acesso ao seu conteúdo original. Assim, os outros servidores podem sofrer os ataques de DDOS, XSS, syn flood, SQL injection e quaisquer outros, deixando o seu servidor original intacto.

Além disso, este recurso também disponibiliza um firewall e todas as outras ferramentas que podem auxiliar o seu ambiente a estar completamente protegido, permitindo mais proteção para os seus dados e as informações dos clientes. Tudo isso, sem nenhum custo extra. Por isso, o CDN é a forma mais barata, conveniente e segura de trazer a maior proteção possível para o seu site contra os ataques cross-site scripting e diversos outros.
