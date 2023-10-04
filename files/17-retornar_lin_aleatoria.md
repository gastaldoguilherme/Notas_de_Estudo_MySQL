> **SELECT + RAND() - Retornar Linhas Aleatórias**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Retornar Linhas Aleatórias em uma Consulta no MySQL com a Função RAND()

Suponha uma tabela de banco de dados com uma grande quantidade de registros. Desejamos retornar 10 registros aleatórios dessa tabela, para fins, por exemplo, de pesquisa ou amostragem.

Ou ainda, por exemplo, uma tabela com nomes de clientes de uma loja, a partir da qual queremos “sortear” um número determinado de usuários.

### Como Retornar Esses Registros de Forma Aleatória?

Existem diferentes formas de retornar linhas aleatórias de uma tabela em um banco de dados, dependendo do sistema de gerenciamento de banco de dados (SGBD) que estivermos usando. Neste tutorial mostrarei como realizar esse procedimento em um banco MySQL, usando a função RAND().

### Como Funciona a Função RAND() no MySQL

A função matemática RAND() no MySQL é utilizada para gerar um número aleatório. Quando a função é chamada sem nenhum argumento, ela retorna um número aleatório de ponto flutuante entre 0 e 1:

```sql
SELECT RAND();
```

Essa declaração gera um número aleatório de ponto flutuante no intervalo entre 0 e 1.

Se quisermos gerar um número aleatório dentro de um intervalo específico, devemos ajustar a faixa de valores gerados efetuando um cálculo com o retorno obtido pela função RAND(). 

Por exemplo, se quisermos gerar um número aleatório de ponto flutuante entre 1 e 100, podemos usar a seguinte expressão:

```sql
SELECT RAND() * 100;
```

Caso desejemos um número aleatório inteiro, podemos combinar a função FLOOR() com a função RAND() para realizar um arredondamento e eliminar as casas decimais:

```sql
SELECT FLOOR(1 + RAND() * 100) AS Numero_Aleatorio;
```

Cada vez que a função for invocada irá gerar um número inteiro aleatório diferente.

A função RAND() usa um algoritmo para gerar números pseudoaleatórios. Esse algoritmo usa um valor inicial chamado “seed” (“semente”) para começar a gerar a sequência de números aleatórios. Se não for especificado um valor de “seed”, o MySQL usará o valor atual do relógio do sistema como semente.

No entanto, se quisermos que a sequência de números aleatórios seja a mesma em todas as chamadas da função RAND() durante uma execução do MySQL, podemos especificar um valor de seed empregando a função rand(). Por exemplo:

```sql
SELECT RAND(100) AS Numero_Aleatorio;
```

Esta consulta retornará sempre o mesmo número aleatório, desde que seja executada na mesma instância do MySQL com o mesmo valor de seed (100).

Outro exemplo: Retornar um número decimal aleatório >= 5 e < 10:

```sql
SELECT 5 + RAND()*(10-5);
```

Já para retornar um número inteiro aleatório >= 5 e < 10, arredondamos o valor gerado com o emprego da função FLOOR():

```sql
SELECT FLOOR(5 + RAND()*(10-5)) AS 'Inteiro Aleatório';
```

### Como Retornar Registros Aleatórios com RAND()

Uma forma de retornar registros aleatórios é utilizando a função RAND() para gerar um número aleatório para cada registro da tabela e então ordenar os resultados por esse número com a cláusula ORDER BY. No MySQL, por exemplo, podemos utilizar a seguinte declaração SQL para retornar 3 registros aleatórios de uma tabela com dados de livros de nome tbl_Livro:

```sql
SELECT Nome_Livro FROM tbl_Livros ORDER BY RAND() LIMIT 3;
```

Neste caso, são gerados números aleatórios para cada linha da tabela e, em seguida, essas linhas são ordenadas, sendo retornadas 3 delas devido à limitação com LIMIT 3. Cada vez que a consulta é realizada, um conjunto diferente de três registros é retornado, mostrando que o dataset gerado é aleatório.

Observe que, ao usar a função RAND() combinada com a cláusula ORDER BY, pode haver uma certa sobrecarga na performance do banco, especialmente para grandes tabelas, pois o MySQL precisa gerar um valor aleatório para cada linha da tabela antes de classificá-la.

Portanto, é importante avaliar o impacto na performance antes de usar essa técnica em uma tabela grande ou em uma consulta que precise ser executada com frequência.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>