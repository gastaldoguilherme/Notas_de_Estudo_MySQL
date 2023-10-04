> **Função ROUND()**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## Arredondar Valores em Consultas com a Função ROUND no MySQL

Uma tarefa comum ao realizar consultas SQL é efetuar o arredondamento de valores numéricos para um número de casas decimais pré-determinado. O MySQL possui funções que permitem realizar esse arredondamento, e uma delas é a função `ROUND()`, que estudaremos neste tutorial.

### Função ROUND()

A função `ROUND()` arredonda um valor numérico até um número especificado de casas decimais.

### Sintaxe

```sql
ROUND(valor, casas_decimais)
```

**Parâmetros:**
- `valor`: o número que se quer arredondar.
- `casas_decimais`: número de casas decimais desejadas. Se omitido, retorna o valor sem nenhuma casa decimal (somente parte inteira).

### Exemplos

1. Arredondar o número 52.36956 para duas casas decimais:

```sql
SELECT ROUND(52.36956, 2) AS Arredondado;
```

2. Arredondar os valores da coluna de preços dos livros para uma casa decimal:

```sql
SELECT NomeLivro, ROUND(PrecoLivro, 1) AS Preço
FROM tbl_Livros;
```

3. Arredondar o valor médio calculado sobre uma coluna de valores numéricos:

```sql
SELECT ROUND(AVG(PrecoLivro), 2) AS 'Preço Médio dos Livros'
FROM tbl_Livros;
```

Esses são exemplos de como utilizar a função `ROUND()` em consultas SQL no MySQL para arredondar valores conforme suas necessidades.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>