> **FOREIGN KEY (Chave Estrangeira)**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## Opções de Chave Estrangeira no MySQL (e MariaDB)

Existem algumas opções aplicáveis às chaves estrangeiras que auxiliam a manter a integridade dos dados nas tabelas do banco de dados. Vamos relembrar a sintaxe SQL para criação de uma chave estrangeira em uma definição de tabela:

```sql
[CONSTRAINT nome_chave_estrangeira] FOREIGN KEY (nomes de colunas separados por vírgulas)
REFERENCES nome_tabela_pai (nomes de colunas separados por vírgulas na tabela pai)
[ON DELETE ação referencial]
[ON UPDATE ação referencial];
```

Os itens entre colchetes `[ ]` são opcionais. `ON DELETE` significa que a ação referencial será executada quando um registro for excluído da tabela pai, e `ON UPDATE` indica que a ação referencial será executada quando um registro for modificado na tabela pai.

As principais opções para as ações referenciais são as seguintes:

- `CASCADE`: A opção CASCADE permite excluir ou atualizar os registros relacionados presentes na tabela filha automaticamente, quando um registro da tabela pai for atualizado (ON UPDATE) ou excluído (ON DELETE). É a opção mais comum aplicada.
- `RESTRICT`: Impede que ocorra a exclusão ou a atualização de um registro da tabela pai, caso ainda hajam registros na tabela filha. Uma exceção de violação de chave estrangeira é retornada. A verificação de integridade referencial é realizada antes de tentar executar a instrução UPDATE ou DELETE.
- `SET NULL`: Esta opção é usada para definir com o valor NULL o campo na tabela filha quando um registro da tabela pai for atualizado ou excluído.
- `NO ACTION`: Essa opção equivale à opção RESTRICT, porém a verificação de integridade referencial é executada após a tentativa de alterar a tabela. É a opção padrão, aplicada caso nenhuma das opções seja definida na criação da chave estrangeira.
- `SET DEFAULT`: “Configura Padrão” – Define um valor padrão na coluna na tabela filha, aplicado quando um registro da tabela pai for atualizado ou excluído.

Vejamos um exemplo usando a cláusula `ON DELETE CASCADE`, que é uma das mais comuns usadas em chaves estrangeiras. Todos os exemplos mostrados aqui também podem ser utilizados com a cláusula `ON UPDATE` e, na prática, podemos usar ambas as cláusulas na mesma tabela.

Para isso, vamos criar um banco de dados de nome “testes”, contendo duas tabelas relacionadas, chamadas de “Pai” e “Filho”, conforme a seguinte estrutura:

```sql
-- Estrutura de tabelas no MySQL - Banco de Dados testes

CREATE DATABASE testes;
USE testes;

CREATE TABLE Pai (
 ID_Pai SMALLINT PRIMARY KEY,
 Nome_Pai VARCHAR(50)
);

CREATE TABLE Filho (
 ID_Filho SMALLINT AUTO_INCREMENT PRIMARY KEY,
 Nome_Filho VARCHAR(50),
 ID_Pai SMALLINT,
 FOREIGN KEY filho(ID_Pai) REFERENCES Pai(ID_Pai)
 ON DELETE CASCADE
 ON UPDATE CASCADE
);
```

Carregando dados de teste nas tabelas:

```sql
INSERT INTO Pai
VALUES (1,'João'), (2,'Mário'), (3,'Renato'), (4,'Emerson'), (5,'André');

INSERT INTO Filho (Nome_Filho, ID_Pai)
VALUES ('João',1), ('Mário',1), ('Renato',3), ('Emerson',4), ('André',3);
```

Consultando os dados carregados:

```sql
SELECT P.ID_Pai, P.Nome_Pai, F.ID_Filho, F.Nome_Filho
FROM Filho F
INNER JOIN Pai P
ON F.ID_Pai = P.ID_Pai;
```

Vamos testar agora a exclusão de um filho:

```sql
DELETE FROM Filho
WHERE Nome_Filho = 'Renato';
```
&nbsp;

---
**ERRO:** " Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column.  To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect."

**SOLUÇÃO:** Este erro que ocorre no MySQL é devido ao modo de atualização segura (safe update mode) que está ativado por padrão. Esse modo impede que você atualize ou exclua registros de uma tabela sem especificar uma cláusula `WHERE` que use uma coluna chave (KEY) para garantir que você não faça alterações acidentais em toda a tabela.

Para resolver esse erro, você tem algumas opções:

***Opção 1:*** Você pode desativar temporariamente o modo de atualização segura com o seguinte comando:

```sql
SET SQL_SAFE_UPDATES = 0;
```

Após desativar o modo seguro, você pode executar sua instrução `DELETE` como originalmente planejado:

```sql
DELETE FROM Filho
WHERE Nome_Filho = 'Renato';
```

***Opção 2:*** Se você quiser manter o modo de atualização segura ativado, você pode adicionar uma cláusula `LIMIT` à sua instrução `DELETE` para garantir que apenas um número limitado de registros seja excluído de cada vez. Por exemplo:

```sql
DELETE FROM Filho
WHERE Nome_Filho = 'Renato'
LIMIT 1;
```

Isso excluirá apenas um registro com o nome 'Renato'. Repetir esse comando conforme necessário até que todos os registros correspondentes tenham sido excluídos.

Lembre-se de que a opção 1 desativa temporariamente o modo seguro, o que pode ser útil para tarefas pontuais. A opção 2 mantém o modo seguro ativado e é mais segura em termos de prevenção de exclusões acidentais em massa. Escolha a opção que melhor se adequar às suas necessidades.

---

&nbsp;

Ao excluirmos o filho Renato, seu pai, que também se chama Renato, continuará a existir na tabela de pais:

```sql
SELECT Nome_Pai, Nome_Filho
FROM Filho
INNER JOIN Pai
ON Filho.ID_Pai = Pai.ID_Pai;
```

Agora vamos testar a cláusula `ON DELETE CASCADE`. Vamos excluir o Pai Renato da tabela de pais. Neste caso, a exclusão deverá se propagar para a tabela de filhos, eliminando o registro do filho relacionado, que no caso é o André:

```sql
DELETE FROM Pai
WHERE Nome_Pai = 'Renato';
```

Verificando a exclusão do pai:

```sql
SELECT Nome_Pai, Nome_Filho
FROM Filho
INNER JOIN Pai
ON Filho.ID_Pai = Pai.ID_Pai;
```

Verificando a exclusão cascateada do filho:

```sql
SELECT * FROM Filho;
```

Agora sobraram apenas os filhos João, Mário e Emerson; Já o André, que era filho do Renato, foi excluído automaticamente após eliminarmos o registro de seu pai da tabela de pais, devido à cláusula `ON DELETE CASCADE`.

Vejamos agora um exemplo usando `SET NULL`.

## Exemplo com SET NULL

Suponha que, ao excluir um pai do banco de dados, em vez de excluir imediatamente seus filhos (cascateamento) nós queiramos manter esses registros, e o campo de ID_Pai da tabela de filhos passe então a conter um valor NULL (“filhos órfãos”).

Neste caso, a tabela de filhos deve ser criada da maneira mostrada a seguir, substituindo a cláusula `ON DELETE CASCADE` por `ON DELETE SET NULL`:

```sql
DROP TABLE Filho;
DROP TABLE Pai;
CREATE TABLE Pai (
 ID_Pai SMALLINT PRIMARY KEY,
 Nome_Pai VARCHAR(50)
) Engine=InnoDB;

CREATE TABLE Filho (
 ID_Filho SMALLINT AUTO_INCREMENT PRIMARY KEY,
 Nome_Filho VARCHAR(50),
 ID_Pai SMALLINT,
 FOREIGN KEY (ID_Pai) REFERENCES Pai(ID_Pai)
 ON DELETE SET NULL
 ON UPDATE CASCADE
) Engine=InnoDB;
```

Após recriar a tabela de filhos e populá-la novamente, com a nova opção de chave estrangeira, vamos realizar um teste excluindo um dos pais da tabela de pais – por exemplo, novamente o Renato:

```sql
DELETE FROM Pai
WHERE Nome_Pai = 'Renato'
limit 1;
```

E agora verificamos os registros na tabela de filhos:

```sql
SELECT * FROM Filho;
```

Note que após excluir o pai, seus filhos, Renato e André mostram o valor “NULL” na coluna ID_Pai da tabela de filhos. Mas eles não foram excluídos automaticamente, como aconteceu ao usarmos `CASCADE` no exemplo anterior.

A coluna não pode ter sido criada com a restrição `NOT NULL` durante a definição da tabela, ou este comando irá gerar uma exceção.

## Usando valor padrão – SET DEFAULT

Outra opção seria a de exibir um valor padrão na coluna quando o valor relacionado for atualizado ou excluído. Para isso, definimos o valor padrão para uma coluna usando a restrição `DEFAULT`, e então acrescentamos a ação referencial `SET DEFAULT` à declaração da chave estrangeira.

Por exemplo, ao excluirmos um pai da tabela de pais, em vez de exibir valor NULL na tabela de filhos, poderíamos exibir o valor “0” (zero), simbolizando um órfão, na coluna ID_Pai desta tabela.

Porém, apesar de a ação referencial `SET DEFAULT` ser suportada pelo MySQL Server, ela é rejeitada como inválida pelo motor de banco de dados InnoDB – que é o motor padrão do MySQL. Um motor de banco de dados que suporta essa ação é o PBXT, um motor que não é  fornecido como parte integrante do MySQL (nem do MariaDB).

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>