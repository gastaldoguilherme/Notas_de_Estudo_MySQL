> **ALTER TABLE, DROP TABLE - Alterar Tabelas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Alterar Tabelas no MySQL - Comando ALTER TABLE e Visualização de Relacionamentos

No MySQL, podemos modificar a estrutura de uma tabela depois de criada, adicionando ou removendo colunas, bem como definindo relacionamentos entre tabelas. O comando principal usado para isso é o `ALTER TABLE`.

### Excluir Colunas: ALTER TABLE - DROP

Para remover uma coluna de uma tabela, você pode usar o seguinte comando:

```sql
ALTER TABLE nome-tabela
DROP COLUMN nome-coluna;
```

Por exemplo, para excluir a coluna `ID_autor` da tabela `tbl_livro`, você faria:

```sql
ALTER TABLE tbl_livro
DROP COLUMN ID_autor;
```

### Excluir uma Chave Primária

Se desejar excluir uma chave primária de uma tabela, você pode fazer isso com o comando `ALTER TABLE` da seguinte maneira:

```sql
ALTER TABLE nome-tabela
DROP PRIMARY KEY;
```

### Adicionar Colunas: ALTER TABLE - ADD

Para adicionar uma nova coluna a uma tabela, utilize o seguinte comando:

```sql

ALTER TABLE nome-tabela
ADD nome-coluna tipo-de-dados constraints;

```

Por exemplo, para adicionar a coluna `ID_autor` da tabela `tbl_livro`, você faria: `after` ou `first`. 
Após procedimento deletar novamente o campo `ID_autor`.

1) após o campo `ID_Categoria`

```sql

ALTER TABLE tbl_livro
add ID_autor SMALLINT NOT NULL after ID_Categoria;

```
2) como primeiro campo

```sql

ALTER TABLE tbl_livro
add ID_autor SMALLINT NOT NULL first;

```

Por exemplo, vamos adicionar a coluna `ID_Autor` à tabela `tbl_livro` com a restrição de chave estrangeira:

```sql
ALTER TABLE tbl_livro
ADD CONSTRAINT fk_ID_Autor
FOREIGN KEY (ID_Autor)
REFERENCES tbl_autores (ID_autor)
ON DELETE CASCADE
ON UPDATE CASCADE;
```

Neste exemplo, estamos criando um relacionamento entre a coluna `ID_Autor` na tabela `tbl_livro` e a coluna `ID_autor` na tabela `tbl_autores`.

### Criar Relacionamentos Entre Tabelas

Você também pode criar relacionamentos entre tabelas usando o `ALTER TABLE`. Por exemplo, para adicionar um relacionamento entre a tabela `tbl_livro` e a tabela `tbl_editoras`, você faria o seguinte:

```sql
ALTER TABLE tbl_livro
ADD CONSTRAINT fk_id_editora
FOREIGN KEY (ID_editora)
REFERENCES tbl_editoras (ID_editora)
ON DELETE CASCADE
ON UPDATE CASCADE;
```

Isso cria uma chave estrangeira na tabela `tbl_livro` que se relaciona com a tabela `tbl_editoras`.

### Modificar Colunas: ALTER TABLE - MODIFY COLUMN

Você pode alterar o tipo de dados de uma coluna existente usando o comando `ALTER TABLE`. Por exemplo:

```sql
ALTER TABLE tbl_Livro
MODIFY COLUMN ID_Autor SMALLINT;
```

Isso alteraria o tipo de dados da coluna `ID_Autor` para `SMALLINT`.

### Excluir Tabelas: DROP TABLE

Finalmente, se você deseja excluir completamente uma tabela, use o comando `DROP TABLE`:

```sql
DROP TABLE nome-tabela;
```

Por exemplo, para excluir a tabela fictícia `Clientes`, você faria:

```sql
DROP TABLE Clientes;
```

Lembre-se de ter cuidado ao executar comandos que excluem tabelas, pois isso apagará todos os dados nessa tabela permanentemente.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>