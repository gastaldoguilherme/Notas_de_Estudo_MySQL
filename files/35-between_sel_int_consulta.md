> **BETWEEN – Seleção de intervalos em consultas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## BETWEEN – Seleção de intervalos em consultas

Aprimorar nossas consultas em um banco de dados MySQL usando a cláusula BETWEEN, que nos permite selecionar intervalos de dados ao retornar os resultados de uma consulta.

Podemos usar a cláusula BETWEEN para, por exemplo, retornar registros cujos preços estejam entre dois valores distintos, ou registros contidos dentro de um intervalo de datas especificado.

A sintaxe para uso da cláusula BETWEEN é a seguinte:

```sql
SELECT colunas FROM tabela
WHERE coluna BETWEEN valor1 AND valor2;
```

Usamos o operador lógico AND para auxiliar na criação do código de consulta.

### Exemplos

**Exemplo 1:** Vamos retornar todos os livros da tabela tbl_livro cuja data de publicação esteja entre 17/05/2004 e 17/05/2011 (note como a data é fornecida no código: ano|mês|dia):

```sql
SELECT * FROM tbl_Livro
WHERE Data_Pub BETWEEN '20040517' AND '20110517';
```


**Exemplo 2:** Agora vamos retornar os nomes dos livros e seus respectivos preços, da tabela tbl_livros, porém somente os livros cujos preços estiverem entre R$ 40,00 e 60,00:

```sql
SELECT Nome_Livro AS Livro, Preco_Livro AS Preço
FROM tbl_Livro
WHERE Preco_Livro BETWEEN 40.00 AND 60.00;
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>