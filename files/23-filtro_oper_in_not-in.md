> **Operadores IN e NOT IN**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Operadores IN e NOT IN no MySQL

O operador SQL **IN** permite verificar se um valor específico corresponde a algum valor presente em uma lista ou subconsulta, passada como parâmetro a uma cláusula de filtragem **WHERE**.

### Sintaxe

```sql
SELECT coluna(s)
FROM tabela
WHERE expressão | coluna IN (valor1, valor2, ...);
```

O operador **IN** retorna o valor 1 (true) se o valor da expressão ou da coluna na cláusula WHERE corresponder a qualquer um dos valores presentes na lista passada e retorna 0 (false) se não houver nenhuma correspondência.

### Operador NOT IN

Podemos combinar o operador IN com o operador lógico **NOT** SQL para determinar se um valor NÃO corresponde com nenhum valor na lista ou subconsulta realizada:

```sql
SELECT coluna(s)
FROM tabela
WHERE expressão | coluna NOT IN (valor1, valor2, ...);
```

## Exemplos

1. Retornar livros cujas editoras têm os códigos 2 ou 4:

```sql
SELECT Nome_Livro, Id_Editora
FROM tbl_livro
WHERE Id_Editora IN (2, 4);
```


2. Retornar livros cuja edição não é a primeira nem a segunda:

```sql
SELECT Nome_Livro, Edicao
FROM tbl_livro
WHERE Edicao NOT IN (1, 2);
```


### Operador IN e Subconsultas

O operador IN (e NOT IN) é frequentemente empregado com uma subconsulta, em vez de uma lista de valores fornecida. A lista de valores a ser avaliada pelo operador IN é fornecida como resultado da subconsulta (subquery).

## Sintaxe

```sql
SELECT coluna(s)
FROM tabela
WHERE expressão | coluna IN (
  SELECT coluna(s)
  FROM tabela
  WHERE | GROUP BY | HAVING | ORDER BY
);
```

### Exemplo 3

Retornar livros e IDs de editoras publicados pelas editoras Wiley ou Microsoft Press, sem usar joins:

```sql

SELECT Nome_Livro, Id_Editora
FROM tbl_livro
WHERE Id_Editora IN (
  SELECT Id_Editora
  FROM tbl_editoras
  WHERE Nome_Editora = 'Wiley' OR Nome_Editora = 'Microsoft Press'
);

```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>