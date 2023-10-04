> **Funções de Agregação (MAX, MIN, AVG, COUNT, SUM) **     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Funções de Agregação (MAX, MIN, AVG, COUNT, SUM)

As funções de agregação são funções SQL que permitem executar operações aritméticas nos valores de uma coluna em todos os registros de uma tabela. Elas retornam um valor simples baseado em um conjunto de valores de entrada.

### Sintaxe básica:
`função(ALL | DISTINCT expressão)`

- `ALL` avalia todos os registros ao agregar o valor da função; é o comportamento padrão.
- `DISTINCT` usa apenas valores distintos (sem repetição) ao avaliar a função.

As funções de agregação desconsideram valores NULL (com exceção da função COUNT(*)).
As principais funções de agregação (mais comuns) em MySQL são as seguintes:

- `MIN`: Valor Mínimo de um conjunto de valores
- `MAX`: Valor Máximo de um conjunto de valores
- `AVG`: Média Aritmética de um conjunto de valores
- `SUM`: Total (Soma) de um conjunto de valores
- `COUNT`: Contar quantidade total de itens

As funções `SUM` e `AVG` somente aceitam como entrada um conjunto de números; já as demais funções podem operar também com outros tipos de dados não-numéricos, como por exemplo strings (caracteres) ou datas.

### Exemplos

1. Retornar o número total de autores cadastrados na tabela de autores:

```sql
SELECT COUNT(*) FROM tbl_autores;
```

2. Contar o número de autores que possuem livros cadastrados na tabela de autores, sem repetições:

```sql
SELECT COUNT(DISTINCT id_autor) FROM tbl_Livro;
```

3. Descobrir o preço mais alto dos livros:

```sql
SELECT MAX(Preco_Livro) FROM tbl_Livro;
```

4. Descobrir a data de publicação do livro mais antigo:

```sql
SELECT MIN(Data_Pub) FROM tbl_Livro;
```

5. Retornar o preço médio dos livros cadastrados no banco:

```sql
SELECT AVG(Preco_Livro) FROM tbl_Livro;
```

6. Descobrir o valor total dos livros presentes na tabela de livros:

```sql
SELECT SUM(Preco_Livro) FROM tbl_Livro;
```

É muito comum usar as funções agregadas em conjunto com a cláusula `GROUP BY`, aplicando-as a grupos de dados específicos.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>