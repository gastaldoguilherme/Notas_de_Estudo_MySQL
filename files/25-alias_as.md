> **ALIAS - AS (Apelido)**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## ALIAS - AS (Apelido)

Pode-se dar um nome diferente (e mais amigável) a uma coluna ou tabela ao realizar uma junção (join) ou retornar o resultado de uma consulta, de modo que seja mais fácil ou intuitivo entender os dados retornados. Para isso, usamos a cláusula `AS`.

### Sintaxe de alias para colunas:

```sql
SELECT coluna
AS alias_coluna
FROM tabela AS alias_tabela;
```

**Exemplo** – Retornar a coluna Nome_Livro com o nome de Livro, simplesmente:

```sql
SELECT Nome_Livro
AS Livro
FROM tbl_Livro;
```

Podemos também aplicar um alias a uma coluna sem a necessidade de usar a palavra `AS`, bastando para isso inserir o alias desejado logo após o nome da coluna, sem separação por vírgulas. Veja o exemplo a seguir:

```sql
SELECT Nome_Livro Livro
FROM tbl_Livro;
```

Para aplicar alias em mais de uma coluna, basta acrescentá-las normalmente, separando-as por vírgulas, e incluindo os alias logo após o nome de cada coluna.

Além disso, podemos criar alias usando palavras compostas, incluindo espaços, bastando para isso envolver o alias entre aspas. O exemplo a seguir mostra as duas possibilidades juntas:

```sql
SELECT Nome_Livro Livro, Preco_Livro 'Preço do Livro'
FROM tbl_Livro;
```

Recomenda-se também usar aspas em aliases que contém caracteres especiais ou que precisam respeitar diferenciação entre maiúsculas e minúsculas (case-sensitive).

É possível também usar os aliases em tabelas inteiras. Veremos como fazer isso na aula sobre INNER JOIN.



&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>