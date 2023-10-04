> **Chave Primária (Primary Key)**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Chave Primária (Primary Key) em Bancos de Dados Relacionais

A **Chave Primária (Primary Key)** é um conceito fundamental em bancos de dados relacionais. Ela se refere a um campo ou conjunto de campos em uma tabela que é usado para identificar de forma única e exclusiva cada linha (registro) na tabela. Uma coluna marcada como chave primária não permite repetição de valores nas linhas e não pode conter valores nulos.

### Tipos de Chave Primária

Uma chave primária pode ser **Simples** ou **Composta**:

### Chave Primária Simples

Uma chave primária simples é constituída por apenas uma coluna em uma tabela, sendo o caso mais comum. Quando não existe um campo "natural" que possa ser usado como chave primária, criamos uma **Chave Surrogada** ou **Substituta**, que é um valor numérico único adicionado à tabela para servir como chave primária. A Chave Surrogada não possui significado para os usuários e é frequentemente usada no lugar de uma chave primária composta.

### Chave Primária Composta

Uma chave primária composta é formada por duas ou mais colunas (atributos). Geralmente é usada quando não é possível utilizar uma única coluna para identificar de forma exclusiva os registros.

## Como Criar uma Chave Primária em uma Nova Tabela

Aqui estão dois modos de criar uma chave primária em uma nova tabela no MySQL:

### Modo 1 – Constraint em Nível de Coluna:

```sql
CREATE TABLE funcionarios (
  id_func smallint PRIMARY KEY AUTO_INCREMENT,
  nome_func VARCHAR(30) NOT NULL,
  sobrenome_func VARCHAR(50) NOT NULL
);
```

### Modo 2 – Constraint em Nível de Tabela (Nomeada):

```sql
CREATE TABLE departamentos_mod (
  id_dep smallint AUTO_INCREMENT,
  nome_dep VARCHAR(30) NOT NULL,
  PRIMARY KEY(id_dep)
);

```

No MySQL, o nome fornecido para uma constraint PRIMARY KEY é ignorado, sendo usada automaticamente a palavra "PRIMARY". Para outros tipos de constraints, o nome fornecido é empregado normalmente.

## Como Adicionar uma Chave Primária a uma Tabela Existente

Você pode adicionar uma chave primária a uma tabela existente da seguinte maneira:

```sql
ALTER TABLE fornecedores
ADD PRIMARY KEY (id_forn);
```

## Como Criar uma Chave Primária Composta

Para criar uma chave primária composta que englobe duas colunas, use uma constraint em nível de tabela:

```sql
CREATE TABLE vendas (
  id_produto smallint,
  id_cliente smallint,
  qtde smallint,
  PRIMARY KEY(id_produto, id_cliente)
);
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>