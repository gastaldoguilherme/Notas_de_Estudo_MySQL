> **Auto Incremento de Valores em Colunas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Auto Incremento de Valores em Colunas

O auto incremento permite que um número único seja gerado quando um novo registro é inserido em uma tabela. No MySQL, isso é feito com a palavra-chave AUTO_INCREMENT. O valor inicial padrão é 1 e se incrementa de 1 em 1. Para iniciar o valor da coluna em algo diferente de 1, você pode usar o seguinte comando:

```sql
ALTER TABLE tabela AUTO_INCREMENT = 100;
```

Isso iniciará o auto incremento em 100. Ao inserir valores na tabela, não é necessário especificar um valor para a coluna de auto-incremento. Geralmente, só é permitido usar uma coluna de auto incremento por tabela, que é tipicamente do tipo inteiro e também deve ter a constraint NOT NULL configurada (geralmente, isso é feito automaticamente).

#### Aqui está um exemplo de criação de tabela com auto incremento:

```sql
CREATE TABLE tbl_teste_incremento (
  Codigo SMALLINT PRIMARY KEY AUTO_INCREMENT,
  Nome VARCHAR(20) NOT NULL
) AUTO_INCREMENT = 15;
```

Neste exemplo, a coluna "Codigo" será incrementada automaticamente a partir de 15.

#### Inserir dados na tabela sem especificar um valor para a coluna de auto-incremento:

```sql
INSERT INTO tbl_teste_incremento (Nome) VALUES ('Ana');
INSERT INTO tbl_teste_incremento (Nome) VALUES ('Maria');
INSERT INTO tbl_teste_incremento (Nome) VALUES ('Julia');
INSERT INTO tbl_teste_incremento (Nome) VALUES ('Joana');
```

#### Para verificar os valores inseridos na tabela, você pode executar uma consulta:

```sql
SELECT * FROM tbl_teste_incremento;
```

#### Verificar o valor atual do auto incremento usando a função MAX:

```sql
SELECT MAX(Codigo) FROM tbl_teste_incremento;
```

#### Alterar o próximo valor de auto-incremento, pode fazer isso com o seguinte comando:

```sql
ALTER TABLE tbl_teste_incremento AUTO_INCREMENT = 90;
```

Isso definirá o próximo valor de auto-incremento como 90.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>