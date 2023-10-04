> **Criar e excluir índices**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Índices em MySQL

Os índices são empregados em uma consulta para ajudar a encontrar registros com um valor específico em uma coluna de forma rápida – ou seja, para aumentar o desempenho na execução de consultas. Sem índices, o MySQL faz uma busca iniciando no primeiro registro e varrendo toda a tabela até encontrar os registros que importam.

Idealmente, devemos criar índices nos campos que são usados em cláusulas WHERE e também envolvidos em JOINS nas consultas.

### Tipos de índices em MySQL
- B-Tree (árvore balanceada): Tipo mais comum (padrão), suportado pela maioria dos engines.
- Hash: Suportado pela engine MEMORY, e pelo InnoDB via adaptative hash indexes.
- R-Tree: Adequado para tipos de dados espaciais. Mais usado em sistemas como o PostgreSQL. Suportado pela engine InnoDB.
- Full-Text Index: Usado em operações do tipo MATCH AGAINST. Suportado pelas engines MyISAM e InnoDB.

## Como criar Índices em MySQL
Podemos criar índices no momento em que criamos uma tabela, ou posteriormente, alterando a estrutura de uma tabela já existente.

### Criar índice junto com a tabela
Para criar um índice no momento em que criamos uma tabela, usamos a declaração INDEX (coluna).

**Sintaxe**

```sql
CREATE [UNIQUE] INDEX nome_índice
ON nome_tabela (
  coluna1 [ASC | DESC],
  [coluna2 [ASC | DESC]]...
);
```

- UNIQUE significa que o índice não permitirá valores duplicados na coluna.
- ASC e DESC se referem à ordem de indexação, se ascendente (ASC) ou descendente (DESC). O padrão é ASC, se nada for informado.

**Exemplo:**

```sql
CREATE TABLE tbl_Editoras (
IdEditora SMALLINT PRIMARY KEY AUTO_INCREMENT,
Nome_Editora VARCHAR(40) NOT NULL,
INDEX (Nome_Editora)
);
```

### Criar índice em tabela já existente
Para adicionar um índice a uma tabela já existente usamos a declaração CREATE INDEX:

**Sintaxe**

```sql
CREATE INDEX nome_índice ON tabela(colunas);
```

**Exemplo:**

```sql
CREATE INDEX idx_editora ON tbl_Editoras(Nome_Editora);
```

### Visualizar os índices
Podemos visualizar os índices associados com uma tabela por meio do comando SHOW INDEX, como segue:

```sql
SHOW INDEX FROM tabela;
```

**Exemplo:**

```sql
SHOW INDEX FROM tbl_Editoras;
```

## Testando os índices
Vamos testar a busca com os índices. Para isso vamos primeiramente recriar a tabela de editoras sem especificar um índice secundário, apenas com a chave primária:

```sql
CREATE TABLE tbl_Editoras (
Id_Editora SMALLINT PRIMARY KEY AUTO_INCREMENT,
Nome_Editora VARCHAR(40) NOT NULL
);
```

Logo após, vamos inserir registros e então realizar uma consulta na tabela.

Inserimos 20 registros na tabela:

```sql
INSERT INTO tbl_Editoras (Nome_Editora)
VALUES 
('Mc Graw-Hill'),('Apress'),('Bookman'),('Bookboon'),
('Packtpub'),('O´Reilly'),('Springer'),('Érica'),
('For Dummies'),('Novatec'),('Microsoft Press'),('Cisco Press'),
('Addison-Wesley'),('Companhia das Letras'),('Artech House'),('Wiley'),
('CRC Press'),('Manning'),('Penguin Books'),('Sage Publishing');
```

Realizamos uma consulta simples agora para ver todos os registros inseridos:

```sql
SELECT * FROM tbl_Editoras;
```

Vamos agora realizar uma consulta mais específica, filtrando o resultado pelo nome de uma editora, como por exemplo a editora Springer:

```sql
SELECT * FROM tbl_Editoras WHERE Nome_Editora = 'Springer';
```

Podemos ver como o MySQL realiza esta consulta internamente acrescentando a cláusula EXPLAIN à consulta:

```sql
EXPLAIN SELECT * FROM tbl_Editoras WHERE Nome_Editora = 'Springer';
```

Vamos agora criar um índice na coluna Nome_Editora:

```sql
CREATE INDEX idx_editora ON tbl_Editoras(Nome_Editora);
```

E então repetir o comando EXPLAIN para ver como o MySQL se comportará agora que a coluna consultada possui um índice:

```sql
EXPLAIN SELECT * FROM tbl_Editoras WHERE Nome_Editora = 'Springer';
```

Como podemos ver, o MySQL teve de ler apenas uma linha para encontrar o registro solicitado. Muito mais rápido e efetivo. Veja que na coluna “Extra” temos a informação de que a consulta usou o índice (“Using index”).

## Como excluir um índice
Para excluir um índice (sem excluir a coluna associada), usamos o comando DROP INDEX, conforme a sintaxe a seguir:

```sql
DROP INDEX nome_índice ON tabela;
```

**Exemplo:**

```sql
DROP INDEX idx_editora ON tbl_Editoras;
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>