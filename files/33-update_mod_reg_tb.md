> **UPDATE – Modificar Registros em Tabelas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## UPDATE – Modificar Registros em Tabelas

Como modificar registros em uma tabela do MySQL. É muito comum alterar o valor de um registro, como o endereço de um cliente em um banco de dados, o telefone ou o preço de um produto.

Para alterar colunas de um ou mais registros em uma tabela, usamos o comando SQL UPDATE, seguindo a sintaxe abaixo:

```sql
UPDATE tabela
SET coluna1 = novo_valor_armazenado,
    coluna2 = novo_valor_armazenado,
    colunaN = novo_valor_armazenado
WHERE coluna = valor_filtro;
```

**Observação importante:** Se não usar a cláusula WHERE para filtrar os registros, todos os dados das colunas indicadas serão alterados. Portanto, tenha cuidado!

### Exemplo

Exemplo: Vamos a um exemplo de alteração de registros. Iremos alterar o nome de um livro na tabela tbl_livros, cujo ID é igual a 101, para “SSH, o Shell Seguro”:

```sql
UPDATE tbl_Livro
SET Nome_Livro = 'SSH, o Shell Seguro'
WHERE ID_LIVRO = 2;
```

**Atenção:** No próximo exemplo, crie um indice para o campo `ISBN13` antes de usar a cláusula WHERE. 

Em consultas que incluem cláusulas WHERE, os índices podem permitir que o MySQL localize os registros que atendem aos critérios de pesquisa mais rapidamente. Isso é especialmente importante em aplicações onde a velocidade de resposta é crucial.

```sql
CREATE INDEX idx_ISBN13 ON tbl_livro(ISBN13);
```

Exemplo: Vamos aumentar o preço do livro cujo ISBN13 é 9780735640610 para R$ 47,20 (atualmente ele custa R$ 45,30)
:

```sql
UPDATE tbl_livro
SET Preco_Livro = 47.20
WHERE ISBN13 = '9780735640610';
```

Basta realizar uma consulta à tabela para verificar se a alteração foi realizada com sucesso.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>