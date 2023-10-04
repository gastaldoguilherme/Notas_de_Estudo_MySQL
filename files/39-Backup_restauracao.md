> **Backup e restauração de bancos de dados**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Backup e restauração de bancos de dados com mysqldump

Backup e a restauração dos bancos de dados criados com MySQL. Faremos o backup de um banco de dados que está rodando no MySQL em um servidor Linux. Para realizar backup e restauração rodando o MySQL no Microsoft Windows, use o PHPMyAdmin.

Para isso, usaremos o comando mysqldump, que será executado no terminal do Linux, de acordo com a sintaxe a seguir (criando o arquivo de backup cujo nome você deverá especificar, com a extensão .sql):

```shell
mysqldump -u root -p nome_banco > arquivo_backup.sql
```

Por exemplo, para realizarmos o backup do banco de dados db_Biblioteca no diretório do usuário, usamos o comando a seguir:

```shell
mysqldump -u root -p db_Biblioteca > /home/usuario/db_Biblioteca.sql
```

Você pode abrir o arquivo resultante com algum editor de textos no terminal para ver seu conteúdo.

## Restauração do Banco de Dados

Se o banco de dados apresentar algum problema e precisar ser restaurado a partir do backup, siga o procedimento a seguir:

1. Crie um banco de dados novo no servidor, com o nome que desejar. Por exemplo, "teste-restore";

2. Execute o seguinte comando (no terminal):

```shell
mysql -u root -p banco_criado < backup.sql
```

Exemplo: Crie um novo banco denominado teste-restore; Restaure o banco de dados db_Biblioteca digitando o comando a seguir:

```shell
mysql -u root -p teste-restore < /home/usuario/db_Biblioteca.sql
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>