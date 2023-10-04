> **Funções e Procedimentos Armazenados**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Rotinas Armazenadas

Estudo de Rotinas Armazenadas em MySQL. Uma Rotina Armazenada é um subprograma que pode ser criado para efetuar tarefas específicas nas tabelas do banco de dados, usando comandos da linguagem SQL e Lógica de Programação.

## Funções e Procedimentos Armazenados

São dois tipos de rotinas armazenadas, parte da especificação SQL. As Funções e Procedimentos são um pouco similares, porém possuem aplicações diferentes.

São invocadas de formas diferentes também (CALL x declaração). 

## Funções Armazenadas (CREATE FUNCTION) 

Uma função é usada para gerar um valor que pode ser usado em uma expressão. Esse valor é geralmente baseado em um ou mais parâmetros fornecidos à função. As funções são executadas geralmente como parte de uma expressão.

O MySQL possui diversas funções internas que o desenvolvedor pode utilizar, e também permite que criemos nossas próprias funções, e é isso que mostraremos como fazer agora.

#### Sintaxe para criação de uma Função

```sql
CREATE FUNCTION nome_função (parâmetros)
RETURNS tipo_dados
código_da_função;
```

#### Como invocar (chamar) uma Função:

```sql
SELECT nome_função(parâmetros);
```

#### Exemplo de aplicação de uma função

Vamos criar uma função que recebe dois valores numéricos e retorna o resultado da multiplicação entre eles:

**Criando a função:**

```sql
CREATE FUNCTION fn_teste (a DECIMAL(10,2), b INT)
RETURNS INT
RETURN a * b;
```

**Invocando a função:**

```sql
SELECT fn_teste(2.5, 4) AS Resultado;
```

**Exemplo 02** – Usando o banco de dados de testes db_biblioteca. Vamos criar uma função que consulta um livro a partir de seu código e retorna o preço total de 6 unidades desse livro:

```sql
SELECT Nome_Livro, fn_teste(Preco_Livro, 6) AS 'Preço de 6 unidades'
FROM tbl_Livro
WHERE ID_Livro = 2;
```

**Exemplo 03** – Crie uma função que mostre a mensagem “O preço do livro XXX é R$ YYY” para os livros do banco de dados, consultados pelo seu ID (XXX é o nome do livro, e YYY o seu preço):

```sql
CREATE FUNCTION fn_verPreço (a SMALLINT)
RETURNS VARCHAR(60)
RETURN
(SELECT CONCAT('O preço do livro ', Nome_Livro, ' é R$ ', Preco_Livro)
FROM tbl_livro
WHERE ID_livro = a);
```

**Testando a função com o livro de código 9:**

```sql
SELECT fn_verPreço(9);
```

#### Excluindo uma função

Para excluir uma função usamos o comando DROP FUNCTION, de acordo com a sintaxe a seguir:

```sql
DROP FUNCTION nome_função;
```


## Procedimentos Armazenados -  Stored Procedures (CREATE PROCEDURE)

Um procedimento armazenado (Stored Procedure, em inglês) é uma sub-rotina disponível para aplicações que acessam sistemas de bancos de dados relacionais.

Podem ser usados para validação de dados, controle de acesso, execução de declarações SQL complexas e muitas outras situações.

Desde a versão 5.0, o MySQL suporta a criação e execução de Stored Procedures.

### Criar Procedimentos Armazenados

A seguir temos a sintaxe para criação de um Procedimento Armazenado em MySQL:

```sql
CREATE PROCEDURE nome_procedimento (parâmetros)
declarações;
```

### Executando um Procedimento

Para invocar uma stored procedure usamos a instrução CALL:

```sql
CALL nome_procedimento (parâmetros);
```

#### Exemplo:

Vamos a um exemplo. Iremos criar um procedimento para consulta de preço de livros, passando como parâmetro o ID do livro:

```sql
-- Criação da stored procedure
DELIMITER //
CREATE PROCEDURE ver_Preco (varLivro SMALLINT)
BEGIN
    SELECT CONCAT('O preço do livro ', Nome_Livro, ' é R$', Preco_Livro) AS Preco 
    FROM tbl_Livro 
    WHERE ID_Livro = varLivro;
END;
//
DELIMITER ;
```

Invocando o procedimento:

```sql
CALL verPreço(3);
```

#### Exemplo 02:

Procedimento para trazer os preços dos livros de uma determinada editora, por nome da editora:

```sql

DELIMITER //
CREATE PROCEDURE consulta_Livros (varEditora VARCHAR(50))
BEGIN
SELECT CONCAT('O livro ', Nome_Livro, ' custa R$ ', Preco_Livro) AS Preço
FROM tbl_Livro
INNER JOIN tbl_editoras
ON tbl_livro.ID_editora = tbl_editoras.ID_Editora
WHERE tbl_editoras.Nome_Editora = varEditora;
END;
//
DELIMITER ;

```

Invocando o procedimento:

```sql
CALL consulta_Livros('O´Reilly');
```

### Excluir stored procedure

Para excluir uma stored procedure do sistema, usamos a declaração DROP PROCEDURE, seguida do nome do procedimento a ser excluído:

```sql
DROP PROCEDURE nome_procedimento;
```

Por exemplo, para excluir a procedure ver_Preco criada no exemplo anterior:

```sql
DROP PROCEDURE ver_Preco;
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>