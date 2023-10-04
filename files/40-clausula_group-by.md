> **Cláusula GROUP BY**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Cláusula GROUP BY

Usamos a cláusula GROUP BY para agrupar registros em subgrupos baseados em colunas ou valores retornados por uma expressão.

Com o GROUP BY podemos agrupar os valores de uma coluna e também realizar cálculos sobre esses valores. Desta forma, ao realizarmos uma consulta, os valores encontrados nas linhas são agrupados e então uma função de agregação pode ser aplicada sobre esses grupos.

### Sintaxe básica:

```sql
SELECT colunas, função_agregação()
FROM tabela
WHERE filtro
GROUP BY coluna
```

### Criar uma tabela para testarmos o GROUP BY:

```sql
CREATE TABLE Vendas (
  ID Smallint Primary Key,
  Nome_Vendedor Varchar(20),
  Quantidade Int,
  Produto Varchar(20),
  Cidade Varchar(20)
);
```

### Inserir registros na tabela criada para teste de GROUP BY:

```sql
INSERT INTO Vendas (ID, Nome_Vendedor, Quantidade, Produto, Cidade)
VALUES
  (10,'Jorge',1400,'Mouse','São Paulo'),
  (12,'Tatiana',1220,'Teclado','São Paulo'),
  (14,'Ana',1700,'Teclado','Rio de Janeiro'),
  (15,'Rita',2120,'Webcam','Recife'),
  (18,'Marcos',980,'Mouse','São Paulo'),
  (19,'Carla',1120,'Webcam','Recife'),
  (22,'Roberto',3145,'Mouse','São Paulo');
```

### Usando o GROUP BY:

#### 1. Consulta usando agregação para obter o total de vendas de Mouses (sem o GROUP BY):

```sql
SELECT SUM(Quantidade) As TotalMouses
FROM Vendas
WHERE Produto = 'Mouse';
```

#### 2. Consulta totalizando as vendas de todos os produtos por cidade:

```sql
SELECT Cidade, SUM(Quantidade) As Total
FROM Vendas
GROUP BY Cidade;
```

#### 3. Consulta contando o número de registros de vendas (quantidade de vendas) por cidade:

```sql
SELECT Cidade, COUNT(*) As Total
FROM Vendas
GROUP BY Cidade;
```

#### 4. Consulta com o total de vendas realizadas por cada vendedor:

```sql
SELECT Nome_Vendedor, SUM(Quantidade)
FROM Vendas
GROUP BY Nome_Vendedor;
```

Também é possível utilizar a cláusula GROUP BY sem o emprego de funções de agregação. Neste caso, a consulta simplesmente retornará valores sem que haja repetição de dados na coluna indicada pela cláusula. Isso é equivalente a aplicar a cláusula DISTINCT em uma consulta usando apenas o SELECT simples.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>