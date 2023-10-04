> **Operadores AND, OR e NOT**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Operadores AND, OR e NOT no MySQL

Os operadores AND, OR e NOT são usados para filtrar registros baseados em mais de uma condição.

- O operador **AND** mostra um registro se ambas as condições forem verdadeiras.
- O operador **OR** mostra um registro se pelo menos uma das condições for verdadeira.
- O operador **NOT** é a negação de uma expressão (inverte seu estado lógico).

### Exemplo 1
Retornar todas as colunas da tabela de livros com os dados de livros de ID maior que 2 e ID de autor menor que 3, ao mesmo tempo:

```sql
SELECT * FROM tbl_Livro
WHERE ID_Livro > 2 AND ID_Autor < 3;
```


### Exemplo 2
Trazer todos os dados da tabela de livros de livros cujo ID é maior que 2 ou cujo ID do autor seja menor do que 3:

```sql
SELECT * FROM tbl_Livro
WHERE ID_Livro > 2 OR ID_Autor < 3;
```


### Exemplo 3
Retornar todos os registros da tabela de livros cujo ID do livro seja maior do que 2 e o ID do autor não seja menor do que 3:

```sql
SELECT * FROM tbl_Livro
WHERE ID_Livro > 2 AND NOT ID_Autor < 3;
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>