> **Cláusula HAVING**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Cláusula HAVING – Filtrando os resultados de um Agrupamento

A cláusula HAVING é usada para especificar condições de filtragem em grupos de registros ou agregações. É frequentemente usada em conjunto com a cláusula GROUP BY para filtrar as colunas agrupadas.

### Sintaxe:

```sql
SELECT colunas, função_agregação()
FROM tabela
WHERE filtro
GROUP BY colunas
HAVING filtro_agrupamento
```

### Exemplos do uso de HAVING (usar tabela criada na aula anterior sobre a cláusula GROUP BY):

1. Consulta retornando o total de vendas das cidades com menos de 2500 produtos vendidos:

```sql
SELECT Cidade, SUM(Quantidade) As Total
FROM Vendas
GROUP BY Cidade
HAVING SUM(Quantidade) < 2500;
```

2. Consulta retornando o total de vendas do produto 'Teclado' nas cidades com menos de 1500 teclados vendidos:

```sql
SELECT Cidade, SUM(Quantidade) As TotalTeclados
FROM Vendas
WHERE Produto = 'Teclado'
GROUP BY Cidade
HAVING SUM(Quantidade) < 1500;
```

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>