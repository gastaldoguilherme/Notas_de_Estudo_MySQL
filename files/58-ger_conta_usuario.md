> **Gerenciar Contas de Usuários – Criar, Consultar, Renomear e Excluir**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Gerenciamento de Usuários do Sistema – Criar, Consultar, Renomear e Excluir

### Gerenciando Contas de Usuários 

Uma das principais tarefas que devem ser realizadas para garantir a segurança de um banco de dados criado em MySQL é o gerenciamento das contas de usuários. Isso inclui a criação de usuários, configuração de permissões de acesso (privilégios) aos bancos de dados e objetos relacionados, e a eventual exclusão de usuários do sistema.

Neste artigo, vamos mostrar como criar e excluir usuários usando declarações SQL no MySQL. Os comandos devem ser executados dentro do sistema do MySQL, e você precisa ter os privilégios adequados para isso. Geralmente, o usuário root do MySQL é quem executa as ações de gerenciamento de usuários, se não houver um outro usuário configurado com permissões administrativas.

### Consultando os Usuários Existentes no Sistema

Podemos efetuar uma consulta à tabela interna User para descobrir os usuários existentes e a partir de qual host eles podem se conectar aos bancos de dados. Para isso, usamos uma declaração SQL SELECT simples, consultando a coluna User da tabela mysql.user, como segue:

```sql
SELECT User, Host FROM mysql.user;
```

Veja abaixo os usuários existentes em meu sistema após a execução dessa declaração:



### Declaração CREATE USER

Usada para criar um novo usuário no sistema (sem privilégios).

**Sintaxe:**

```sql
CREATE USER usuário@host IDENTIFIED BY 'senha';
```

- `host` é o nome do host a partir de onde o usuário pode se conectar ao banco de dados; geralmente usamos localhost para a máquina local. Se não for especificado um host, o MySQL acrescentará automaticamente o símbolo % como nome do host, o que significa que o usuário poderá se conectar de qualquer lugar. É possível também usar o endereço IP de um host (por exemplo, 127.0.0.1 para o host local).
- Você pode também especificar um domínio a partir de onde o usuário pode se conectar. Por exemplo, para que um usuário de nome marcos se conecte a partir de qualquer host do domínio planetaunix.com.br, use a sintaxe `marcos@'%.planetaunix.com.br'` (com o sinal de porcentagem e o nome do domínio entre aspas).

Após a criação do usuário, ele não terá nenhum privilégio em nenhum banco de dados. Os privilégios podem ser atribuídos por meio da declaração GRANT, que estudaremos na próxima lição.

**Exemplos:**

1. Criando um usuário de nome "fabio" com senha "1234" no MySQL, com acesso a partir do host local:

```sql
CREATE USER fabio@localhost IDENTIFIED BY '1234';
```

Verificando se o usuário foi criado como especificado:

```sql
SELECT User, Host FROM mysql.user;
```



2. Criando um usuário de nome "ana" com acesso a partir de qualquer local:

```sql
CREATE USER ana IDENTIFIED BY "1234";
```

Note que na coluna Host aparece o símbolo % para a usuária ana, significando que ela pode acessar o SGBD de qualquer local.

3. Criando um usuário de nome marcos sem senha definida no momento:

```sql
CREATE USER marcos@localhost;
```

Para alterar ou configurar uma senha para esse usuário posteriormente, use o comando SET PASSWORD:

```sql
SET PASSWORD FOR 'marcos'@'localhost' = PASSWORD('1234');
```

Alteramos a senha do usuário marcos para 1234 com essa declaração.

Nas versões mais recentes do MySQL, a declaração SET PASSWORD foi deprecada e não será mais utilizada nas próximas versões.

### Declaração RENAME USER

Usada para renomear um usuário do MySQL. Se o usuário possuir privilégios configurados, eles são mantidos para o novo nome de usuário.

**Sintaxe:**

```sql
RENAME USER nome_atual TO novo_nome;
```

**Exemplo:**

Vamos renomear a usuária ana para monica:

```sql
RENAME USER ana TO monica;
```

### Declaração DROP USER

Usada para excluir um usuário do MySQL. Esta declaração elimina o usuário e seus privilégios do sistema.

**Sintaxe:**

```sql
DROP USER nome_usuário;
```

**Exemplo:**

Vamos remover a usuária monica:

```sql
DROP USER monica;
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>