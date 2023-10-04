> **Constraint DEFAULT – Valores padrão em colunas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## Constraint DEFAULT – Valores padrão em colunas

A constraint DEFAULT é utilizada para inserirmos um valor padrão em uma coluna no MySQL. Esse valor padrão é inserido automaticamente nos registros, se nenhum valor for especificado para a coluna em questão.

### Sintaxe para criar um padrão em uma nova tabela onde uma coluna tem o valor padrão "São Paulo":

```sql
CREATE TABLE nome_tabela
(
  coluna1 tipo restrição,
  coluna2 tipo DEFAULT 'São Paulo',
  colunaN tipo restrição
);
```

### Sintaxe para criar um padrão em uma tabela já existente:

```sql
ALTER TABLE nome_tabela
MODIFY COLUMN nome_coluna tipo_dados DEFAULT 'valor_padrão';
```

### Exemplo – Aplicando Padrões:

Vamos criar o padrão de sobrenome "da Silva" na coluna Sobrenome_autor da tabela tbl_autores:

```sql
ALTER TABLE tbl_autores
MODIFY COLUMN Sobrenome_Autor Varchar(60)
DEFAULT 'da Silva';
```

Em seguida, inserimos um registro para teste:

```sql
INSERT INTO tbl_autores (ID_Autor, Nome_autor)
VALUES (6, 'João');
```

Não foi especificado o sobrenome do autor; será assumido o padrão criado.

Verificando o resultado:

```sql
SELECT * FROM tbl_autores;
```

### Desaplicando Padrões

É possível eliminar o valor padrão aplicado a uma coluna. Vamos eliminar o padrão da coluna Sobrenome_autor e testar:

```sql
ALTER TABLE tbl_autores
MODIFY COLUMN Sobrenome_Autor Varchar(60);
```

Em seguida, inserimos outro registro de teste:

```sql
INSERT INTO tbl_autores (ID_Autor, Nome_autor)
VALUES (7, 'Joana');
```

Verificando o resultado:

```sql
SELECT * FROM tbl_autores;
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>