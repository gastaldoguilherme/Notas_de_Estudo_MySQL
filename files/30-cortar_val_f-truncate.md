> **Função TRUNCATE()**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## A Função TRUNCATE() no MySQL

A função TRUNCATE trunca ("corta") um valor numérico, mostrando um número especificado de casas decimais. Note que esta função não arredonda valores, apenas oculta as casas decimais, de acordo com a quantidade que será exibida.

### Sintaxe

```sql
TRUNCATE(valor, casas_decimais)
```

**Parâmetros:**

- **valor:** o número a ser truncado.
- **casas_decimais:** número de casas decimais (depois da vírgula) a serem exibidas.

### Exemplos

1. Truncar um número para não exibir casas decimais (0 casas)

```sql
SELECT TRUNCATE(52.69863, 0) AS Truncado;
```



Contraste o resultado retornado como obtido com a função ROUND() aplicada no mesmo valor:

```sql
SELECT ROUND(52.69863, 0) AS Arredondado;
```



Veja que neste segundo caso o valor foi arredondado, o que não aconteceu ao usar a função TRUNCATE(), que apenas oculta as casas decimais.

2. Truncar os valores retornados por uma coluna que contém valores monetários para exibir apenas uma casa decimal:

```sql
SELECT TRUNCATE(PrecoLivro, 1) AS Preços
FROM tbl_livro
WHERE PrecoLivro >= 250.00;
```



**Observação:** Cuidado para não confundir a função TRUNCATE() com a declaração SQL TRUNCATE TABLE, que é empregada para limpar todo o conteúdo de uma tabela!

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>