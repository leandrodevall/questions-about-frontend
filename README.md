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
