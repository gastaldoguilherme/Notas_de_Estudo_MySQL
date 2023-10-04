> **Operador UNION**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Operador UNION

Assim como uma JOIN, uma operação UNION permite combinar dados provenientes de duas ou mais tabelas (ou da mesma tabela, com condições diferentes). Porém, em vez de combinar as colunas dessas tabelas, a UNION combina as linhas de dois ou mais conjuntos de resultados. Imagine que um INNER JOIN é uma operação de intersecção entre conjuntos, e que o UNION é uma operação de soma de conjuntos.

Assim, uma UNION combina (“une”) duas ou mais declarações SELECT. O resultado de cada SELECT deve possuir o mesmo número de colunas, e o tipo de dado de cada coluna correspondente deve ser compatível.

Para ordenar o resultado de uma operação UNION, podemos usar uma declaração ORDER BY após o último SELECT codificado. Neste ORDER BY somente é possível usar os nomes de colunas que foram declarados no primeiro SELECT da declaração UNION completa. Os nomes de colunas no resultado final são tirados deste primeiro SELECT.

### Sintaxe do UNION

```sql
SELECT declaração_1
UNION [ALL}
SELECT declaração_2
UNION [ALL}
SELECT declaração_3 ...
[ORDER BY colunas]
```

Por padrão, o operador UNION elimina resultados duplicados; para incluí-los no resultado final, acrescente a palavra ALL.


#### Exemplo 01

Retornar nomes de livros, preços e categorias dos livros.
Caso a categoria seja Tecnologia, mostrar o preço acrescido de 15% em seu valor.
Caso o livro custe mais de 200 reais, descontar 10% em seu valor.
Ordenar por preço, do mais caro para o mais barato.

```sql
SELECT L.Nome_Livro, L.Preco_Livro AS 'Preço Normal', L.Preco_Livro * 0.90 AS Preco_Ajustado, A.ID_Categoria, A.Categoria 
FROM tbl_Livro L 
INNER JOIN tbl_categorias A ON L.ID_Categoria = A.ID_Categoria 
WHERE L.Preco_Livro > 200.00
UNION
SELECT L.Nome_Livro, L.Preco_Livro AS 'Preço Normal', L.Preco_Livro * 1.15 AS Preco_Ajustado, A.ID_Categoria, A.Categoria 
FROM tbl_Livro L 
INNER JOIN tbl_categorias A ON L.ID_Categoria = A.ID_Categoria 
WHERE A.Categoria = 'tecnologia'
ORDER BY Preco_Ajustado DESC;
```



#### Exemplo 02

Retornar nomes de livros e preços dos livros.
Caso o preço do livro seja igual ou superior a R$ 150,00, mostrar a mensagem “Livro Caro” em uma coluna à direita no resultado da consulta.
Caso contrário, mostrar a mensagem “Preço Razoável”
Ordenar por preço, do mais barato para o mais caro.

```sql
SELECT Nome_Livro Livro, Preco_Livro Preço, 'Livro Caro' Resultado
FROM tbl_Livro
WHERE Preco_Livro >= 150.00
UNION
SELECT Nome_Livro Livro, Preco_Livro Preço, 'Preço Razoável' Resultado
FROM tbl_Livro
WHERE Preco_Livro < 150.00
ORDER BY Preço asc;
```

#### Exemplo 03

Por padrão, o MySQL não possui suporte a FULL OUTER JOIN (junção externa completa). Porém, podemos simular um FULL OUTER JOIN usando UNION, como no exemplo abaixo.

```sql
SELECT * FROM tbl_Categorias
LEFT JOIN tbl_Livro
ON tbl_Livro.Id_Categoria = tbl_Categorias.Id_Categoria
UNION
SELECT * FROM tbl_Categorias
RIGHT JOIN tbl_Livro
ON tbl_Livro.Id_Categoria = tbl_Categorias.Id_Categoria;
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>