> **INSERT INTO - Inserir Dados em Tabelas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Inserir Dados em Tabelas - Comando INSERT INTO

Para inserir dados em uma tabela no MySQL, utilizamos o comando `INSERT INTO`. A sintaxe geral é a seguinte:

```sql
INSERT INTO nome_tabela (coluna1, coluna2, ...)
VALUES (valor1, valor2, ...);
```

Neste comando, especificamos a tabela na qual queremos inserir os dados, juntamente com as colunas correspondentes às quais estamos inserindo valores. Em seguida, após a palavra-chave `VALUES`, fornecemos os valores correspondentes nas mesmas colunas e na mesma ordem.

Caso haja uma coluna com auto incremento, ela não deve ser incluída na lista de colunas do comando, pois seus valores são gerados automaticamente pelo MySQL quando um novo registro é adicionado.

### Exemplos no banco de dados db_biblioteca:

#### Inserindo dados na tabela tbl_editoras:

```sql
INSERT INTO tbl_editoras (Nome_Editora) VALUES ('Prentice Hall');
INSERT INTO tbl_editoras (Nome_Editora) VALUES ('O´Reilly');
INSERT INTO tbl_editoras (Nome_Editora) VALUES ('Microsoft Press');
INSERT INTO tbl_editoras (Nome_Editora) VALUES ('Wiley');
INSERT INTO tbl_editoras (Nome_Editora) VALUES ('McGraw-Hill Education');
```

#### Inserindo dados na tabela tbl_autores:

```sql
INSERT INTO tbl_autores
VALUES
(1, 'Daniel', 'Barret'),
(2, 'Gerald', 'Carter'),
(3, 'Mark', 'Sobell'),
(4, 'William', 'Stanek'),
(5, 'Richard', 'Blum'),
(6, 'Jostein', 'Gaarder'),
(7, 'Umberto', 'Eco'),
(8, 'Neil', 'De Grasse Tyson'),
(9, 'Stephen', 'Hawking'),
(10, 'Stephen', 'Jay Gould'),
(11, 'Charles', 'Darwin'),
(12, 'Alan', 'Turing'),
(13, 'Simon', 'Monk'),
(14, 'Paul', 'Scherz');
```

#### Inserindo dados na tabela tbl_categorias:

```sql
INSERT INTO tbl_categorias
VALUES
(1, 'Tecnologia'),
(2, 'História'),
(3, 'Literatura'),
(4, 'Astronomia'),
(5, 'Botânica');
```

#### Inserindo dados na tabela tbl_livro:

```sql
INSERT INTO tbl_Livro (Nome_Livro, ISBN13, ISBN10, Data_Pub, Preco_Livro, Id_Categoria, ID_Autor, ID_Editora)
VALUES
('Linux Command Line and Shell Scripting','9781118983843', '111898384X', '20150109', 68.35, 1, 5, 4),
('SSH, the Secure Shell','9780596008956', '0596008953', '20050517', 58.30, 1, 1, 2),
('Using Samba','9780596002565', '0596002564', '20031221', 61.45, 1, 2, 2),
('Fedora and Red Hat Linux', '9780133477436', '0133477436', '20140110', 62.24, 1, 3, 1),
('Windows Server 2012 Inside Out','9780735666313', '0735666318', '20130125', 66.80, 1, 4, 3),
('Microsoft Exchange Server 2010','9780735640610', '0735640610', '20101201', 45.30, 1, 4, 3),
('Practical Electronics for Inventors', '9781259587542', '1259587541', '20160324', 67.80, 1, 13, 5);


```

Neste último exemplo, especificamos as colunas que receberiam os dados, pois uma das colunas (ID_livro) é auto-incrementada e não precisa ser fornecida.

Para testar a inserção de dados, você pode executar consultas como as seguintes:

```sql
SELECT * FROM tbl_autores;
SELECT * FROM tbl_editoras;
SELECT * FROM tbl_livro;
```

Isso permitirá verificar os dados inseridos nas tabelas.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>