> **WHERE – Filtrar resultados de consultas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## WHERE – Filtrar resultados de consultas

A cláusula WHERE permite filtrar registros nos resultados de uma consulta, de modo a trazer apenas as informações desejadas (e não o conteúdo completo das colunas).

### Sintaxe:

```sql
SELECT colunas
FROM tabela 
WHERE coluna = valor;
```

### Exemplos:

1. Retornar o nome e a data de publicação do livro cujo ID do autor é 1:

```sql
SELECT Nome_Livro, Data_Pub
FROM tbl_Livro
WHERE ID_Autor = 1;
```



Foi retornado apenas um registro, do livro cujo autor possui o ID especificado na cláusula WHERE.

2. Trazer o ID e Nome do autor do autor cujo sobrenome é Stanek:

```sql
SELECT ID_Autor, Nome_Autor
FROM tbl_autores
WHERE Sobrenome_Autor = 'Stanek';
```


Foi retornado o nome do autor cujo sobrenome é Stanek: William Stanek.

3. Mostrar os nomes e os preços dos livros publicados pela editora de ID igual a 3:

```sql
SELECT Nome_Livro, Preco_Livro
FROM tbl_livro
WHERE ID_Editora = 3;
```

Neste caso foram retornados dois livros, publicados pela editora de ID indicado.

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>