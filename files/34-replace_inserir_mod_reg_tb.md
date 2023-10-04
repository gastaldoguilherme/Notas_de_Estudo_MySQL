> **REPLACE - Inserir ou Modificar Registro em Tabela**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## REPLACE - Inserir ou Modificar Registro em Tabela

A declaração MySQL REPLACE permite inserir um novo registro em uma tabela do MySQL, caso o registro ainda não exista, ou atualizar um registro já existente. Funciona como se fosse uma declaração INSERT, mas sem apresentar erros se tentamos inserir um registro já inserido na tabela – em vez disso, valores das colunas podem ser alterados. É uma “combinação” de INSERT com UPDATE.

Para determinar se um registro (linha) já existe na tabela, são usados os valores da chave primária ou coluna com constraint UNIQUE na tabela. Se a tabela não possuir esses índices, a declaração REPLACE funciona como um INSERT simples.

Para usar o REPLACE em MySQL, é necessário ter privilégios para executar as instruções INSERT e DELETE.

### Como inserir uma nova linha com REPLACE no MySQL

**Sintaxe:**

```sql
REPLACE [INTO] nomeTabela(lista_colunas)
VALUES(lista_valores);
```

Como podemos ver, a sintaxe é bem parecida com a da declaração INSERT!

### Exemplos

Vamos ver como inserir e modificar registros em uma tabela no MySQL usando a declaração REPLACE.

Primeiramente, criamos uma nova tabela para testes:

```sql
--Tabela para testes da declaração REPLACE
  
  CREATE TABLE paises (
  ID_Pais Tinyint AUTO_INCREMENT,
  nome_Pais VARCHAR(25) UNIQUE NOT NULL,
  nome_Capital VARCHAR(50) NOT NULL,
  PRIMARY KEY(ID_Pais)
);
```

Populamos a tabela com alguns registros:

```sql
INSERT INTO paises(nome_Pais, nome_Capital)
VALUES
('Argentina','Buenos Aires'),('Brasil','Brasília'),
('Equador','Quito'),('Namíbia','Windhoek'),
('Bélgica','Bruxelas'),('China','Pequim'),
('Espanha','Sevilha'),('Marrocos','Rabat');
```

Note que um dos registros tem um valor errado – a capital da Espanha é Madrid, e não Sevilha. Vamos consertar isso posteriormente.

Vamos visualizar a tabela com seu conteúdo:

```sql
SELECT * FROM paises;
```

As linhas foram inseridas com sucesso, mas um dos registros – Espanha – foi inserido com valor errado para sua capital, que é Madrid, e não Sevilha. Vamos inserir o registro novamente, como uma nova linha, usando uma declaração INSERT comum:

```sql
INSERT INTO paises(nome_Pais, nome_Capital)
VALUES ('Espanha','Madrid');
```

Note que foi gerado um erro, pois o país Espanha já está cadastrado – e a coluna nome_Pais possui a restrição UNIQUE configurada, o que significa que não são aceitos valores repetidos nesta coluna.

Vamos usar agora a instrução REPLACE para trocar os dados do país incorreto:

```sql
REPLACE INTO paises(ID_Pais, nome_Pais, nome_Capital)
VALUES (7, 'Espanha', 'Madrid');
```

Note que fornecemos nesta declaração o ID do país (7), valor da chave primária do registro, para que o valor atual seja substituído, e não um novo registro criado.

Vamos visualizar a tabela modificada:

```sql
SELECT * FROM paises;
```

Note que o nome da capital foi alterado, sem alterar o valor da chave primária – exatamente como uma declaração UPDATE faria.

Mas, o que acontece se eu não fornecer a chave primária ao executar um REPLACE? Vamos testar isso.

A capital da Namíbia é Windhoek, como está registrado na tabela. Mas existe um nome aportuguesado para esta cidade: Vinduque. Vamos tentar trocar o nome da capital da Namíbia usando REPLACE, mas agora sem fornecer o valor da chave primária (que é 4):

```sql
REPLACE INTO paises(nome_Pais, nome_Capital)
VALUES ('Namíbia', 'Vinduque');
```

Vejamos o que aconteceu:

```sql
SELECT * FROM paises;
```

Neste caso, foi usado o valor padrão da coluna ID_Pais, pois não fornecemos um valor para a chave primária. E, no caso, trata-se de uma coluna de auto incremento, e assim valor padrão é um novo numero na sequência de valores – ou seja, uma nova chave primária (no caso, 10).

Não ocorreu um update da linha Namíbia, o que podemos ver claramente pois o Id do país (chave primária) mudou – isso indica que o registro atual foi excluído e um novo registro foi criado.

E se o registro não existisse previamente na tabela? O que ocorreria ao tentar usar o REPLACE?

Neste caso um novo registro é criado. Tente isso com exercício – use o REPLACE com os seguintes dados:

- País: Angola
- Capital: Luanda


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>