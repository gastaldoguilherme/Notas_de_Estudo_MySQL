> **LEFT e RIGHT JOIN – Consultar dados em duas ou mais tabelas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## LEFT e RIGHT JOIN – Consultar dados em duas ou mais tabelas

Continuando nosso estudo sobre JOINS em MySQL, nesta lição, vamos analisar o uso do OUTER JOINS. Existem três tipos principais:

- **LEFT JOIN:** Retorna todas as linhas da tabela à esquerda, mesmo se não houver nenhuma correspondência na tabela à direita.
- **RIGHT JOIN:** Retorna todas as linhas da tabela à direita, mesmo se não houver nenhuma correspondência na tabela à esquerda.
- **FULL JOIN:** Retorna linhas quando houver uma correspondência em qualquer uma das tabelas. É uma combinação de LEFT e RIGHT JOINS.

Vamos ver a sintaxe e alguns exemplos de cada um deles. Falaremos também sobre o CROSS JOIN nesta lição.

### LEFT JOIN

**Sintaxe:**

```sql
SELECT colunas
FROM tabela_esq
LEFT (OUTER) JOIN tabela_dir
ON tabela_esq.coluna = tabela_dir.coluna;
```

**Exemplo:**

```sql
SELECT * FROM tbl_autores
LEFT JOIN tbl_Livro
ON tbl_Livro.ID_Autor = tbl_autores.ID_Autor;
```

**LEFT JOIN excluindo correspondências:**

**Sintaxe:**

```sql
SELECT coluna
FROM tabela_esq
LEFT (OUTER) JOIN tabela_dir
ON tabela_esq.coluna = tabela_dir.coluna
WHERE tabela_dir.coluna IS NULL;
```

**Exemplo:**

```sql
SELECT * FROM tbl_autores
LEFT JOIN tbl_Livro
ON tbl_Livro.ID_Autor = tbl_autores.ID_Autor
WHERE tbl_Livro.ID_Autor IS NULL;
```

### RIGHT JOIN

**Sintaxe:**

```sql
SELECT colunas
FROM tabela_esq
RIGHT (OUTER) JOIN tabela_dir
ON tabela_esq.coluna = tabela_dir.coluna;
```

**Exemplo:**

```sql
SELECT * FROM tbl_Livro AS Li
RIGHT JOIN tbl_editoras AS Ed
ON Li.ID_editora = Ed.ID_editora;
```

**RIGHT JOIN excluindo correspondências:**

**Sintaxe:**

```sql
SELECT coluna
FROM tabela_esq
RIGHT (OUTER) JOIN tabela_dir
ON tabela_esq.coluna = tabela_dir.coluna
WHERE tabela_esq.coluna IS NULL;
```

**Exemplo:**

```sql
SELECT * FROM tbl_Livro
RIGHT JOIN tbl_editoras
ON tbl_Livro.ID_editora = tbl_editoras.ID_editora
WHERE tbl_Livro.ID_editora IS NULL;
```

### FULL JOIN

**Sintaxe:**

```sql
SELECT colunas
FROM tabela1
FULL (OUTER) JOIN tabela2
ON tabela1.coluna = tabela2.coluna;
```

**FULL JOIN excluindo correspondências:**

**Sintaxe:**

```sql
SELECT colunas
FROM tabela1
FULL (OUTER) JOIN tabela2
ON tabela1.coluna = tabela2.coluna
WHERE tabela1.coluna IS NULL
OR tabela2.coluna IS NULL;
```

### CROSS JOIN

Um CROSS JOIN retorna um produto cartesiano entre as tabelas, mostrando todas as combinações possíveis entre os registros.

**Sintaxe:**

```sql
SELECT colunas FROM tabela1
CROSS JOIN tabela2;
```

Vejamos um exemplo de CROSS JOIN – Retornar Nome e Preço dos livros, cruzando os dados com a tabela de autores:

```sql
SELECT Nome_Livro, Preco_Livro
FROM tbl_livro
CROSS JOIN tbl_autores;
```

Isso representa o produto cartesiano de um Cross Join entre as tabelas de livros e autores.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>