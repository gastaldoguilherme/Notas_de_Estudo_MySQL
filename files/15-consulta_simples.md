> **SELECT - Consultar Tabelas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Consultas Simples

Podemos dizer que a tarefa mais importante que um banco de dados MySQL realiza, do ponto de vista do usuário, é permitir a realização de consultas aos dados armazenados. O comando básico que utilizamos para realizar as consultas é o comando SELECT.

### Comando SELECT

**Sintaxe:**

```sql
SELECT coluna(s) FROM Tabela;
```

**Exemplos:**

- Consultar nomes dos autores cadastrados na tabela de autores:

  ```sql
  SELECT Nome_Autor FROM tbl_Autores;
  ```

- Consultar todos os dados da tabela de autores (usamos o caractere curinga * para denotar todos os campos):

  ```sql
  SELECT * FROM tbl_Autores;
  ```

- Consultar os nomes dos livros (apenas) na tabela de livros:

  ```sql
  SELECT Nome_Livro FROM tbl_livro;
  ```

- Consultar nomes de livros e IDs de autores respectivos na tabela de livros:

  ```sql
  SELECT Nome_Livro, ID_Autor FROM tbl_livro;
  ```

- Consultar nomes de livros e seus ISBNs na tabela de livros:

  ```sql
  SELECT Nome_Livro, ISBN FROM tbl_livro;
  ```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>