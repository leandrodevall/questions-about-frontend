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
