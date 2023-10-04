> **DELETE e TRUNCATE TABLE - Excluir Registros de uma Tabela**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Excluir Registros de uma Tabela no MySQL com DELETE e TRUNCATE TABLE

Uma das tarefas mais comuns na manutenção de tabelas de bancos de dados é a exclusão de registros (linhas). É muito comum, por exemplo, excluir um produto de uma tabela que não é mais ofertado por uma loja, ou um cliente que se descadastrou de um sistema.

Além disso, em algumas situações muito especiais, pode ser necessário excluir todos os registros de uma tabela – ou seja, limpar a tabela.

Podemos excluir registros de uma tabela com SQL por meio de duas declarações: `DELETE FROM` e `TRUNCATE TABLE`.

### Excluir um ou mais registros especificados – Cláusula DELETE
Com a cláusula DELETE podemos excluir registros específicos, indicados (filtrados) por meio de uma condição na cláusula `WHERE`.

### Sintaxe:

```sql
DELETE FROM tabela WHERE coluna = valor;
```

**Exemplo** – vamos excluir o autor da tabela de autores cujo id de autor é igual a 2:

```sql
DELETE FROM tbl_autores
WHERE ID_Autor = 2;
```

Obs.: Sempre use a cláusula `WHERE` para evitar a perda de dados da tabela, caso contrário todos os registros serão excluídos, um a um!

### TRUNCATE TABLE
O comando `TRUNCATE TABLE` permite remover todas as linhas de uma tabela em uma única operação, sem registrar as exclusões de linhas individuais.

O `TRUNCATE TABLE` equivale a executar a instrução DELETE, porém sem usar a cláusula `WHERE`. Portanto, é usada para apagar completamente o conteúdo de uma tabela no MySQL.

Entretanto, a cláusula `TRUNCATE TABLE` é mais rápida e utiliza menos recursos de sistema e log de transações durante sua execução.

### Exemplo
Exemplo: Vamos excluir todos os registros presentes na tabela `tbl_teste_incremento`:

```sql
TRUNCATE TABLE tbl_teste_incremento;
```

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>