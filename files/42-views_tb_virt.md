> **VIEWS – Criando Tabelas Virtuais (Visões)**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## VIEWS – Criando Tabelas Virtuais (Visões)

Uma **View (Exibição / Visão)** é uma tabela virtual (estrutura de dados) baseada no conjunto de resultados de uma consulta SQL, criada a partir de um conjunto de tabelas (ou outras views) presentes no banco, que servem como tabelas-base.

Contém linhas e colunas como uma tabela real, e pode receber comandos como declarações JOIN, WHERE e funções como uma tabela normal. A view fica armazenada no banco de dados.

Mostra sempre resultados de dados atualizados, pois o motor do banco de dados recria os dados toda vez que um usuário consulta a visão.

## Aplicações das Views

Usamos views para propósitos diversos:

- Para simplificar o acesso a dados que estão armazenados em múltiplas tabelas relacionadas
- Implementar segurança nos dados de uma tabela, por exemplo criando uma visão que limite os dados que podem ser acessados, por meio de uma cláusula WHERE
- Prover isolamento de uma aplicação da estrutura específica de tabelas do banco acessado.

## Como criar Views no MySQL

Podemos criar uma visão no MySQL usando a sintaxe abaixo:

### Sintaxe:

```sql
CREATE VIEW Nome_visão
AS SELECT colunas
FROM tabela
WHERE condições;
```

**Exemplo**: Vamos criar uma view de nome vw_LivrosAutores que retorne ao ser consultada os nomes dos livros e seus respectivos autores, eliminando a necessidade de realizar INNER JOIN toda vez que precisarmos desses dados:

```sql
CREATE VIEW vw_LivrosAutores
AS SELECT tbl_Livro.Nome_Livro AS Livro, tbl_autores.Nome_Autor AS Autor
FROM tbl_Livro
INNER JOIN tbl_autores
ON tbl_Livro.ID_Autor = tbl_autores.ID_Autor;
```

## Como usar a View criada

Vamos utilizar a view criada, realizando uma consulta nela como se estivéssemos consultando uma tabela real do banco de dados:

```sql
SELECT Livro, Autor
FROM vw_LivrosAutores
ORDER BY Autor;
```

Veja como ficou mais simples retornar os nomes dos livros e dos autores agora – o código fica muito mais limpo e simples, facilitando, por exemplo, sua incorporação em uma aplicação que acesse o banco de dados do MySQL.

## Como alterar uma View

Podemos alterar uma view, para que ela funcione de forma diferente, usando o comando ALTER VIEW. Vamos alterar a view vw_LivrosAutores para incluir também os preços dos livros. Veja o código abaixo:

```sql
ALTER  VIEW vw_LivrosAutores AS
SELECT tbl_Livro.Nome_Livro AS Livro, tbl_autores.Nome_Autor AS Autor, Preco_Livro AS Valor
FROM tbl_Livro
INNER JOIN tbl_autores
ON tbl_Livro.ID_Autor = tbl_autores.ID_Autor;
```

Podemos testá-la com uma consulta:

```sql
SELECT * FROM vw_LivrosAutores;
```

## Como visualizar as views existentes nos bancos de dados

Podemos consultar as views existentes em um banco de dados com o comando a seguir:

```sql
SHOW FULL TABLES IN nome_banco
WHERE TABLE_TYPE LIKE 'VIEW';
```

Por exemplo, para ver todas as visões criadas em um banco de nome biblioteca:

```sql
SHOW FULL TABLES IN biblioteca
WHERE TABLE_TYPE LIKE 'VIEW';
```

Caso o banco a ser verificado seja o selecionado atualmente, não é necessário informar seu nome ao consultar as views, como segue:

```sql
SHOW FULL TABLES
WHERE TABLE_TYPE LIKE 'VIEW';
```

Finalmente, podemos ver todas as views de todos os bancos de dados existentes na instância do MySQL com o comando a seguir:

```sql
SELECT TABLE_SCHEMA, TABLE_NAME
FROM information_schema.TABLES
WHERE TABLE_TYPE LIKE 'VIEW';
```

## Como excluir views

Se precisarmos excluir uma view do MySQL, basta usar o comando DROP VIEW seguido do nome da View. Vamos excluir a view vw_LivrosAutores:

```sql
DROP VIEW vw_LivrosAutores;
```



&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>