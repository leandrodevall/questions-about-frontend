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

`O que é é um Callback Hell?`<br/>

callback é uma convensão do JS sobre funções que usam resultado de outras funções para fazer algo, isso também é muito comum quando lidamos com assincronismo, já que precisamos esperar um resultado para seguir com alguma função, nesse contexto surgem os callbacks hell.

Exemplo: temos uma função que faz uma chamada assíncrona para carregar algum dado, e esse dado vai ser usado como argumento para algumas funções também assíncronas, e dado um momento que uma função precisa esperar o resultado acabávamos tendo que fazer nesting de funções para ir utilizando os resultado conforme forem ficando disponível, resultando em uma função com muitas funções de difícil leitura e compreensão. 

Todo esse contexto foi resolvido com a chegada das Promisses, sendo basicamente um recurso para lidar melhor com programação assyncronica. Uma Promisse é iniciada como uma função com duas instruções básicas, resolve e reject e a palavra reservada Promise. No Resolve callback só é executado quando temos uma resposta válida e o reject quando temos um erro. Também temos a opções de usar função utilizando a palavra reservada await na chamada da promisse, e a diferença entre os dois é que com await o JS em tempo de execução vai esperar até que a promisse seja resolvida e a proposta do then é continuar a execução até que tenhamos uma resposta para seguir com callback. Quando temos um cenário com várias promssies podemos utilizar também o promisseAll. Com isso temos mais organização e legibilidade do código e não mais toda aquela tripa de funções em funções.

