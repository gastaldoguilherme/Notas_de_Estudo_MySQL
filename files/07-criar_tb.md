> **CREATE TABLE - Criar Tabelas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Criação de Tabelas – comando CREATE TABLE

A sintaxe básica para criar uma tabela no MySQL é a seguinte:

```sql
CREATE TABLE IF NOT EXISTS nome_tabela (
   coluna tipo_dados constraints,
   coluna tipo_dados constraints,
   coluna tipo_dados constraints,
   ...
);
```

Note que precisamos especificar, além do nome da tabela, os nomes das colunas que a comporão e também seus respectivos tipos de dados, além das eventuais constraints.



## Aqui está um exemplo de criação de tabela:

```sql
CREATE TABLE IF NOT EXISTS tbl_livro (
  ID_Livro SMALLINT AUTO_INCREMENT PRIMARY KEY,
  Nome_Livro VARCHAR(70) NOT NULL,
  ISBN13 CHAR(13),
  ISBN10 CHAR(10),
  Data_Pub DATE NOT NULL,
  Preco_Livro DECIMAL(6,2) NOT NULL,
  ID_Categoria SMALLINT,
  ID_Autor SMALLINT NOT NULL,
  ID_Editora VARCHAR(70) NOT NULL
);

```

## Agora, vamos criar outras tabelas como exemplo:

```sql
CREATE TABLE tbl_autores (
  ID_Autor SMALLINT PRIMARY KEY,
  Nome_Autor VARCHAR(50) NOT NULL,
  Sobrenome_Autor VARCHAR(60) NOT NULL
);

CREATE TABLE tbl_categorias (
  ID_Categoria SMALLINT PRIMARY KEY,
  Categoria VARCHAR(30) NOT NULL
);

CREATE TABLE tbl_editoras (
  ID_Editora SMALLINT PRIMARY KEY AUTO_INCREMENT,
  Nome_Editora VARCHAR(50) NOT NULL
);
```

Estas são algumas tabelas para armazenar informações sobre livros, autores, categorias e editoras.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>