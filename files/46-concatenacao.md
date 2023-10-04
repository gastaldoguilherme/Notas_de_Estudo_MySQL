> **Concatenação de Strings: CONCAT, IFNULL e COALESCE**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Concatenação de Strings com as Funções CONCAT, IFNULL e COALESCE

No MySQL, é possível concatenar strings usando as funções CONCAT, IFNULL e COALESCE. Vamos estudá-las nesta lição.

Para fins de estudo, vamos criar uma tabela em um banco de dados de teste. Use o código a seguir para fazer isso:

**Criar tabela:**

```sql
CREATE TABLE teste_nulos (
  id smallint PRIMARY KEY auto_increment,
  item varchar(20),
  quantidade smallint NULL
 );
```

**Inserir dados para testes:**

```sql
INSERT INTO teste_nulos (id, item, quantidade)
VALUES (1, 'Pendrive', 5);
INSERT INTO teste_nulos (id, item, quantidade)
VALUES (2, 'Monitor', 7);
INSERT INTO teste_nulos (id, item, quantidade)
VALUES (3, 'Teclado', NULL);
```

**Efetuar consulta para verificar funcionalidade da tabela:**

```sql
SELECT * FROM teste_nulos;
```

### Função CONCAT

**Sintaxe:**

```sql
CONCAT(string ou nome_coluna, <string | nome_coluna)
```

**Exemplos:**

```sql
SELECT CONCAT('William ', 'Shakespeare') AS 'Escritor';
```

```sql
SELECT CONCAT(Nome_autor, ' ', Sobrenome_autor) AS 'Nome Completo'
FROM tbl_autores;
```

```sql
SELECT CONCAT('Eu gosto do livro ', Nome_Livro) as frase_concatenada
FROM tbl_Livro WHERE ID_autor = 2;
```

### Concatenação com NULL

Se uma string for concatenada com o valor NULL, o resultado retornado será apenas NULL, independentemente das outras partes concatenadas. Veja um código de exemplo:

```sql

--este é um item cuja quantidade é nula
SELECT CONCAT('A quantidade adquirida é ', ' ', quantidade)
FROM teste_nulos
WHERE  item = 'Teclado'; 

```

Para evitar esse problema de concatenação com valores nulos, existem funções disponíveis que substituem NULL por outro valor, como as funções IFNULL e COALESCE.

### Função IFNULL

Essa função efetua a concatenação de strings e, caso a string concatenada seja nula, a substitui por um valor padrão (substituição).

**Sintaxe:**

```sql
IFNULL (valor, substituição)
```

**Exemplo:**

```sql
SELECT CONCAT('A quantidade adquirida é ', ' ', IFNULL(quantidade, 0)) as frase_concat_ifnull
FROM teste_nulos
WHERE  item = 'Teclado';
```

### Função COALESCE

Essa função retornará o primeiro valor não-nulo encontrado em seus argumentos.

**Sintaxe:**

```sql
COALESCE (valor1, valor2, …, valorN)
```

**Exemplo:**

```sql
SELECT CONCAT('A quantidade adquirida é ', ' ', COALESCE(NULL, quantidade, NULL, 0)) as frase_concat_coalesce
FROM teste_nulos
WHERE  item = 'Teclado';
```

Isso conclui o estudo sobre a concatenação de strings com as funções CONCAT, IFNULL e COALESCE em MySQL.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>