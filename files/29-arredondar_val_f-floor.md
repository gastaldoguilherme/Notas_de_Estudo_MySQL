> **Função FLOOR()**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## A Função FLOOR() no MySQL

A função FLOOR() ("piso", em português) no MySQL retorna o maior valor inteiro que é menor ou igual a um número passado como argumento. Em outras palavras, esta função arredonda um número decimal para baixo, mostrando apenas sua parte inteira.

### Sintaxe

```sql
FLOOR(número)
```

Onde o parâmetro "número" é o valor que se deseja arredondar para baixo (inteiro sem parte decimal).

### Exemplos

1. Arredondar um número decimal passado como argumento:

```sql
SELECT FLOOR(63.75) AS Arredondado;
```


2. Retornar um valor monetário armazenado em uma coluna de tabela, ignorando os centavos (casas decimais):

```sql
SELECT PrecoLivro AS 'Preço Real', FLOOR(PrecoLivro) AS 'Reais sem centavos'
FROM tbl_Livros
WHERE PrecoLivro > 200.00;
```


Todos os valores foram arredondados para baixo (número inteiro mais próximo inferior ao valor), independente da quantidade de dígitos presentes nas casas decimais.

A função complementar da função FLOOR() no MySQL é a função CEILING(), que arredonda os valores numéricos para cima (mostra apenas o valor inteiro mais próximo superior).




&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>