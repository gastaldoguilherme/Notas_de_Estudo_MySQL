> **SELECT + ORDER BY - Consultas com Ordenação**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Consultas com Ordenação – Cláusula ORDER BY

A palavra-chave ORDER BY é usada para ordenar o conjunto de resultados de registros em uma consulta SQL, tanto de forma ascendente quanto descendente.

### Sintaxe:

```sql
SELECT colunas FROM tabela
ORDER BY coluna_a_ordenar;
```

Podemos configurar a ordenação como ascendente (crescente) ou descendente (decrescente) com o uso das palavras ASC ou DESC:

- ASC – Ordem ascendente
- DESC – Ordem descendente (inversa)

### Ordem de Classificação por Tipo de Dados

A ordem padrão de classificação do ORDER BY (ASC) para os diversos tipos de dados é a seguinte:

- Valores numéricos são exibidos com os menores valores primeiro (do menor para o maior).
- Valores de data são mostrados com os valores menores primeiro, o que significa as datas mais antigas (do mais antigo para o mais recente).
- Valores de caracteres são exibidos em ordem alfabética.
- Quando houver valores nulos (NULL), eles serão mostrados por último (em sequências descendentes, com DESC, são mostrados primeiro).

É possível classificar os dados da consulta usando uma coluna que não esteja presente na lista de colunas da declaração SELECT.

Também é possível ordenar os resultados da consulta usando mais de uma coluna. Para isso, basta listar as colunas na cláusula ORDER BY, separadas por vírgulas. Os resultados serão ordenados pela primeira coluna na lista e, em seguida, pela segunda coluna, e assim por diante.

Pode-se ordenar qualquer das colunas listadas em qualquer ordem, por exemplo, colunas em ordem ascendente e colunas em ordem descendente, bastando para isso suceder o nome da coluna que será classificada em ordem inversa com a palavra-chave DESC.

### Exemplos:

```sql
SELECT * FROM tbl_Livro
ORDER BY Nome_Livro ASC;
```

```sql
-- Cláusula SQL ORDER BY em MySQL
SELECT Nome_Livro, ID_Editora
FROM tbl_Livro
ORDER BY ID_Editora; -- (ordem crescente)
```

```sql
SELECT Nome_Livro, Preco_Livro
FROM tbl_Livro
ORDER BY Preco_Livro DESC;
-- (ordem decrescente)
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>