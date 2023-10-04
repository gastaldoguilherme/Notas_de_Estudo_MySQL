> **ALTER TABLE - Renomear Colunas em Tabelas **     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Renomear Colunas em uma Tabela com ALTER TABLE

No MySQL, é comum a necessidade de alterar o nome de uma coluna em uma tabela. Para fazer isso, utilizamos o comando `ALTER TABLE` seguido do comando `CHANGE`, onde especificamos o nome atual da coluna e o novo nome que desejamos atribuir a ela. Opcionalmente, podemos também alterar o tipo de dados em alguns casos.

Aqui está a sintaxe geral para renomear uma coluna em uma tabela MySQL:

```sql
ALTER TABLE nome_da_tabela
CHANGE nome_atual novo_nome [Tipo de Dados];
```

### Exemplo:

Vamos supor que temos uma tabela de produtos chamada `tbl_Produto` com a seguinte estrutura:

| Coluna    | Tipo de Dados |
| --------- | -------------- |
| ID_Prod   | SMALLINT       |
| Nome_Prod | VARCHAR(25)    |
| Tipo_Prod | VARCHAR(20)    |
| Preco_Prod| DECIMAL(6,2)   |

Agora, desejamos alterar o nome da coluna `Tipo_Prod` para `Categ_Prod` e aumentar a quantidade de caracteres suportada no campo. Para fazer isso, podemos executar o seguinte comando SQL:

```sql
ALTER TABLE tbl_Produto
CHANGE Tipo_Prod Categ_Prod VARCHAR(30);
```

Neste exemplo, estamos renomeando a coluna `Tipo_Prod` para `Categ_Prod` e também modificando seu tipo de dados para `VARCHAR(30)`, permitindo assim mais caracteres.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>