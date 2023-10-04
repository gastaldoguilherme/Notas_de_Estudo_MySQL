> **INNER JOIN – Consultar dados em duas ou mais Tabelas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## INNER JOIN – Consultar dados em duas ou mais Tabelas 

### JOINS

A cláusula JOIN é usada para combinar dados provenientes de duas ou mais tabelas do banco de dados, baseado em um relacionamento entre colunas destas tabelas. Há duas categorias principais de joins:

- **INNER JOIN:** Retorna linhas (registros) quando houver pelo menos uma correspondência em ambas as tabelas.
- **OUTER JOIN:** Retorna linhas (registros) mesmo quando não houver ao menos uma correspondência em uma das tabelas (ou ambas). O OUTER JOIN divide-se em LEFT JOIN, RIGHT JOIN e FULL JOIN.

Nesta aula, vamos estudar especificamente a cláusula INNER JOIN.

### INNER JOIN

Como dito, um INNER JOIN (ou simplesmente JOIN) permite obter registros com dados provenientes de duas ou mais tabelas relacionadas do banco de dados no MySQL. A sintaxe básica de um INNER JOIN em uma consulta é:

```sql
SELECT colunas
FROM tabela1
INNER JOIN tabela2
ON tabela1.coluna = tabela2.coluna;
```

Onde `tabela1.coluna` é o nome da primeira tabela concatenado com um ponto e com o nome da coluna chave primária ou estrangeira da tabela, e `tabela2.coluna` é o nome da segunda tabela concatenado com um ponto e com a chave estrangeira ou primária dessa tabela que se relaciona com a chave da primeira tabela.

###### Exemplo 1

Vamos consultar as tabelas de livros e autores (`tbl_livro` e `tbl_autores`) e retornar os dados relativos aos livros e aos autores ao mesmo tempo:

```sql
SELECT * FROM tbl_Livro
INNER JOIN tbl_autores
ON tbl_Livro.ID_Autor = tbl_autores.ID_Autor;
```

###### Exemplo 2

Vamos retornar apenas os nomes dos livros, seus ISBNs e os nomes dos autores desses livros:

```sql
SELECT tbl_Livro.Nome_Livro, tbl_Livro.ISBN, tbl_autores.Nome_Autor
FROM tbl_Livro
INNER JOIN tbl_autores
ON tbl_Livro.ID_Autor = tbl_autores.ID_Autor;
```

###### Exemplo 3

Vamos retornar os nomes dos livros e nomes das editoras, mas somente das editoras cujo nome se inicia com a letra M:

```sql
SELECT L.Nome_Livro AS Livros, E.Nome_editora AS Editoras
FROM tbl_Livro AS L
INNER JOIN tbl_editoras AS E
ON L.ID_editora = E.ID_editora
WHERE E.Nome_Editora LIKE 'M%';
```

###### Exemplo 4

Aqui vamos fazer um INNER JOIN com as três tabelas do banco de dados simultaneamente. Queremos os nomes e preços dos livros, nomes de seus autores e editoras, mas somente das editoras cujo nome se inicia com a letra O, tudo isso ordenado em ordem decrescente de preço dos livros:

```sql
SELECT L.Nome_Livro AS Livro,
A.Nome_autor AS Autor,
E.Nome_Editora AS Editora,
L.Preco_Livro AS 'Preço do Livro'
FROM tbl_Livro AS L
INNER JOIN tbl_autores AS A
ON L.ID_autor = A.ID_autor
INNER JOIN tbl_editoras AS E
ON L.ID_editora = E.ID_editora
WHERE E.Nome_Editora LIKE 'O%'
ORDER BY L.Preco_Livro DESC;
```

Neste exemplo fazemos o join entre a tabela de livros e a de autores, e logo em seguida entra a tabela de livros e a de editoras, pois os relacionamentos se dão entre essas tabelas. Também ordenamos os resultados por ordem decrescente dos preços dos livros.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>