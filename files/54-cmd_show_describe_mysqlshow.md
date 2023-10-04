> **Comandos SHOW, DESCRIBE e mysqlshow**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## Comandos SHOW, DESCRIBE e mysqlshow ##

### Comandos SHOW

Os comandos do grupo SHOW são usados para acessar os metadados no sistema. Para verificar quais comandos SHOW estão disponíveis, digite no terminal:

```shell
mysql -u root -p
HELP SHOW;
```

Exemplos de Comandos SHOW:

1. Ver os bancos de dados presentes no sistema:

```sql
SHOW DATABASES;
```

2. Informações sobre procedimentos armazenados e funções:

```sql
SHOW CREATE PROCEDURE verpreço;
SHOW CREATE FUNCTION calcula_desconto;
```

3. Mostrar código usado na criação de uma tabela:

```sql
SHOW CREATE TABLE tbl_Livro;
```

4. Mostrar as tabelas do banco de dados atual:

```sql
SHOW TABLES;
```

5. Ver as colunas de uma tabela:

```sql
SHOW [FULL] COLUMNS FROM tbl_editoras;
```

6. Ver colunas com nomes específicos:

```sql
SHOW COLUMNS FROM tbl_Livro LIKE 'I%';
```

7. Especificando tipos de dados:

```sql
SHOW COLUMNS FROM tbl_Livro WHERE Type like 'varchar%';
```

8. Mostrar privilégios de acesso aos DBs para um usuário:

```sql
SHOW GRANTS FOR root@localhost;
```

### Comando DESCRIBE

O comando DESCRIBE é um atalho para o comando SHOW COLUMNS FROM;

Exemplo:

```sql
DESCRIBE tbl_Livro;
```

O comando DESCRIBE também pode ser abreviado para:

```sql
DESC tbl_Livro;
```

Obs. O comando DESCRIBE não suporta as cláusulas LIKE e WHERE.

### Comando mysqlshow

O comando mysqlshow opera diretamente no shell do Linux. Ele permite obter informações sobre os bancos de dados, tabelas e colunas.

Sintaxe:

```shell
mysqlshow -u usuário -p [banco [tabela [coluna]]]
```

Exemplos do comando mysqlshow:

1. Ver os bancos de dados disponíveis:

```shell
mysqlshow -u root -p
```

2. Ver as tabelas em um banco de dados específico:

```shell
mysqlshow -u root -p db_Biblioteca
```

3. Ver os campos pertencentes a uma tabela:

```shell
mysqlshow -u root -p db_Biblioteca tbl_autores %
```

4. Ver as tabelas com contagem de colunas e linhas, começando com uma letra específica:

```shell
mysqlshow -vv -u root -p db_Biblioteca 't*'
```

5. Ver informações sobre uma coluna específica em uma tabela:

```shell
mysqlshow -u root -p db_Biblioteca tbl_autores ID_autor
```

Obs.: Usamos % no final do comando para que o shell não interprete tbl_autores como wildcard, e sim como o parâmetro tabela; esse problema ocorre quando temos o caractere underline (_) no nome da tabela.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>