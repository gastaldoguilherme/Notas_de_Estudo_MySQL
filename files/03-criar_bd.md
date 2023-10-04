> **CREATE DATABASE -  Criar banco de dados**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

### Criar um novo banco de dados

Para criar um novo banco de dados no MySQL, você pode usar o seguinte comando SQL:

```sql
CREATE DATABASE IF NOT EXISTS nome_BD;
```

- Onde `nome_BD` é o nome que você deseja dar ao banco de dados. 
- O elemento `IF NOT EXISTS` é opcional e evita o erro de tentar criar um banco de dados que já existe no servidor, pois não é possível ter dois bancos de dados com o mesmo nome.

**Exemplo:** Vamos criar um banco de dados chamado `db_Biblioteca`, que será usado nos demais exemplos deste curso:

```sql
CREATE DATABASE db_Biblioteca;
```

### Verificar Bancos de Dados

Você pode verificar os bancos de dados existentes no MySQL usando o comando SQL `SHOW DATABASES;`:

```sql
SHOW DATABASES;
```

### Usar um Banco de Dados

O comando `USE` instrui o SGBDR a utilizar o banco de dados especificado para executar os comandos. A sintaxe é a seguinte:

```sql
USE nome_banco_de_dados;
```

Para verificar o banco de dados selecionado no momento, você pode usar o comando SQL:

```sql
SELECT DATABASE();
```

### Excluir Banco de Dados

Para excluir um banco de dados existente, você pode usar o comando SQL `DROP DATABASE;`:

```sql
DROP DATABASE IF EXISTS nome_BD;
```

O elemento `IF EXISTS` é opcional e evita erros caso o banco de dados não exista.

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>

