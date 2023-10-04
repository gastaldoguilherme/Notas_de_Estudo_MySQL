> **Constraints (Restrições)**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## Constraints (Restrições)

As **Restrições** são regras aplicadas às colunas de uma tabela no SQL MySQL. Elas são usadas para limitar os tipos de dados que podem ser inseridos. As constraints podem ser especificadas no momento de criação da tabela (usando `CREATE TABLE`) ou após a tabela ter sido criada (usando `ALTER TABLE`).

As principais constraints são as seguintes:

- **NOT NULL**: A constraint NOT NULL impõe que uma coluna não aceite valores NULL. Isso significa que o campo deve sempre possuir um valor, e não é possível inserir um registro (ou atualizá-lo) sem fornecer um valor para esse campo.

- **UNIQUE**: A restrição UNIQUE garante a unicidade dos valores em uma coluna ou conjunto de colunas. Tanto UNIQUE quanto PRIMARY KEY garantem a unicidade dos dados. Uma constraint PRIMARY KEY automaticamente possui uma restrição UNIQUE definida, portanto, não é necessário especificar essa constraint nesse caso. É possível ter várias constraints UNIQUE em uma mesma tabela, mas apenas uma Chave Primária por tabela.

- **PRIMARY KEY**: A constraint PRIMARY KEY (Chave Primária) identifica de forma única cada registro em uma tabela de banco de dados. As Chaves Primárias devem sempre conter valores únicos, e uma coluna de chave primária não pode conter valores NULL. Cada tabela deve ter uma chave primária e apenas uma chave primária.

- **FOREIGN KEY**: Uma FOREIGN KEY (Chave Estrangeira) em uma tabela é um campo que aponta para uma chave primária em outra tabela. Isso é usado para criar relacionamentos entre tabelas no banco de dados.

- **DEFAULT**: A restrição DEFAULT é usada para inserir um valor padrão especificado em uma coluna. O valor padrão será adicionado a todos os novos registros caso nenhum outro valor seja especificado no momento da inserção de dados.

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>
