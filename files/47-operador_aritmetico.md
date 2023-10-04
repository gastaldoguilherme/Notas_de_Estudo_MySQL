> **Funções Matemáticas e Operadores Aritméticos**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## MySQL – Funções Matemáticas e Operadores Aritméticos

Nesta lição, vamos aprender como usar funções matemáticas e operadores aritméticos no MySQL para realizar cálculos com os dados das tabelas.

É possível realizar operações matemáticas simples nos valores de uma coluna e retornar resultados em uma coluna calculada. Usamos os operadores matemáticos comuns, como soma, subtração, divisão, multiplicação, divisão inteira, módulo (resto da divisão) e outros:

- Soma: +
- Subtração: -
- Divisão: /
- Multiplicação: *
- Módulo: % ou MOD
- Divisão Inteira: DIV

Vejamos alguns exemplos do uso de operadores aritméticos simples:

```sql
SELECT 3 * 9;
```
```sql
SELECT Nome_Livro, Preco_Livro * 5 AS 'Preço de 5 Unidades' FROM tbl_Livro;
```
```sql
SELECT 2 * 9 / 3;
SELECT Nome_Livro, Preço_Livro / 2 AS 'Preço com 50% de desconto' FROM tbl_Livro;
```
```sql
SELECT 10 MOD 3;
```

Aumentando os preços de todos os livros da tabela de livros em 10% (equivale a multiplicar o preço por 1,1):

```sql
UPDATE tbl_livro SET Preco_livro = Preco_livro * 1.1;
```

Neste exemplo, todos os livros têm o preço reajustado, pois não utilizamos a cláusula WHERE na declaração. 
Para aumentar apenas o preço de livros específicos, é necessário aplicar o filtro adequado.

### Funções Matemáticas

É possível também utilizar funções matemáticas nos valores de uma coluna e retornar resultados em uma coluna calculada. Abaixo, listamos algumas funções matemáticas mais comuns:

- CEILING(): Arredondar para cima
- FLOOR(): Arredondar para baixo
- PI(): Retorna o valor de Pi
- POW(x, y): Retorna x elevado a y
- SQRT(): Raiz quadrada de um argumento
- SIN(): Retorna o seno de um número dado em radianos
- HEX(): Retorna a representação hexadecimal de um valor decimal.

Exemplos de Funções Matemáticas:

```sql
SELECT Nome_Livro, CEILING(Preco_Livro * 5) AS 'Preço Arredondado' FROM tbl_livro;
SELECT PI();
SELECT POW(2, 4);
SELECT SQRT(81);
SELECT SIN(PI());
SELECT HEX(1200);
```

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>