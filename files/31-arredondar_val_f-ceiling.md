> **Função CEILING()**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## A Função CEILING() no MySQL

A função CEILING() (ou "teto" em português) retorna o menor valor inteiro que é maior ou igual a um número. Em outras palavras, ela permite arredondar um número decimal para cima, mostrando apenas sua parte inteira.

### Sintaxe

```sql
CEILING(número)
```

Onde o parâmetro "número" é o valor que se deseja arredondar para cima.

**Observação:** A função CEIL() é idêntica à função CEILING() e pode ser usada no lugar dela.

```sql
CEIL(número)
```

### Exemplos

1. Arredondar um número decimal para cima:

```sql
SELECT CEILING(72.25) AS 'Arredonda para cima';
```


2. Retornar a parte inteira de um valor armazenado em uma coluna de tabela:

```sql
SELECT Preco_Livro AS 'Preço Real', CEILING (Preco_Livro) AS 'Arredondado para cima'
FROM tbl_Livro
WHERE Preco_Livro > 50.00;
```


Todos os valores foram arredondados para cima (inteiro mais próximo superior), independente do valor presente nas casas decimais.

3. O mesmo que o exemplo anterior, mas usando a função CEIL():

```sql
SELECT Preco_Livro AS 'Preço Real', CEIL(Preco_Livro) AS 'Arredondado para cima'
FROM tbl_Livros
WHERE Preco_Livro > 50.00;
```



A função complementar da função CEILING() no MySQL é a função FLOOR(), que arredonda os valores numéricos para baixo (inteiro mais próximo inferior ao valor informado).


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>