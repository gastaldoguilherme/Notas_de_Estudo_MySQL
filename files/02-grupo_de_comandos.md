> **DDL, DML, DCL, DQL, DTL - Grupos de Comandos SQL**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Grupos de Comandos SQL
Os comandos SQL podem ser divididos em cinco grupos principais:

1. #### DDL – Data Definition Language
Comandos que possuem a função de definir a estrutura do banco de dados (esquema). Permitem efetuar a criação, alteração e exclusão de objetos, como tabelas, views, triggers, procedimentos armazenados e outros.

- `CREATE`: Cria um novo banco de dados, tabela, visão, índice ou outro objeto no BD.
- `ALTER`: Modifica um objeto existente no BD, como uma tabela.
- `DROP`: Exclui uma tabela inteira, uma exibição de uma tabela ou outro objeto, incluindo o próprio banco de dados.

2. #### DML – Data Manipulation Language
Comandos utilizados para gerenciar os dados armazenados no banco, permitindo inserir novos dados, alterar dados existentes ou excluir dados armazenados.

- `INSERT`: Cria um novo registro (linha).
- `UPDATE`: Modifica registros existentes.
- `DELETE`: Exclui um ou mais registros.

3. #### DCL – Data Control Language
Comandos utilizados para controlar o acesso aos dados armazenados no banco, por meio de permissões de acesso.

- `GRANT`: Fornece privilégios de acesso a um usuário.
- `REVOKE`: Retira os privilégios fornecidos a um usuário.
- `ALTER USER`: Permite modificar contas, como a senha de um usuário.

4. #### DQL – Data Query Language
Comandos utilizados para realizar consultas em um banco, por exemplo para obter dados armazenados.

- `SELECT`: Obtém registros especificados de uma ou mais tabelas, ou seja, efetuar consultas em tabelas. (Alguns autores consideram o comando SELECT como pertencente ao grupo de comandos DML.)

5. #### DTL – Data Transaction Language
Comandos empregados para gerenciar transações no banco de dados. São usados para gerenciar as alterações realizadas por comandos DML executados.

- `COMMIT`: Salvar transações de forma permanente no banco de dados.
- `ROLLBACK`: Restaurar o banco ao último estado após um commit que teve êxito.
- `SAVEPOINT`: Salvar temporariamente uma transação para que seja possível efetuar rollback àquele ponto se necessário.

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>