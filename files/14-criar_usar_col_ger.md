> **Criar e Usar Colunas Geradas**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## Criando e usando Colunas Geradas – Campos Calculados em Tabelas no MySQL

Campos calculados (ou colunas geradas) são colunas em uma tabela em um banco de dados que apresentam os resultados de uma expressão pré-definida, geralmente uma fórmula aplicada a outras colunas, da mesma forma que uma View, porém sem causar overhead no banco, pois por padrão seus dados não são fisicamente armazenados na tabela. Uma outra vantagem de um campo calculado é que a integridade dos dados é aumentada, pois os cálculos são realizados em nível de tabela, em vez de serem realizados por meio de queries (consultas) criadas pelo desenvolvedor.

Como citado, por padrão um campo calculado no MySQL não armazena nenhum valor – os dados são calculados no momento de uma consulta. Porém, é possível armazenar os dados de um campo gerado opcionalmente, o que significa que o cálculo é realizado e os dados são salvos na coluna. É possível até mesmo indexar um campo calculado, e uma das aplicações desses campos é na substituição de triggers, simplificando o design e a operação sobre o banco de dados.

## Sintaxe

Para criar uma coluna calculada usamos a seguinte sintaxe:

```sql
nome_coluna tipo_dados [GENERATED ALWAYS] AS expressão [VIRTUAL | STORED] constraints
```

- `GENERATED ALWAYS` é apenas uma forma de indicar explicitamente que o campo é calculado.
- `expressão` é a fórmula que desejamos usar para realizar o cálculo do valor da coluna.
- `VIRTUAL` significa que o valor do campo é calculado sempre que for realizada uma consulta a ele, mas seus dados não ficam armazenados na tabela em si. O campo nesse caso não ocupa espaço em disco. É possível criar índices secundários em colunas calculadas virtuais (com InnoDB).
- `STORED` significa que o valor do campo é calculado (em operações de inserção e atualização de dados) e armazenado na tabela. O acesso aos dados é mais rápido nesse caso, mas obviamente ocupa mais espaço em disco.

O padrão é a criação de colunas do tipo `VIRTUAL` caso não seja especificada a opção. Também é possível ter colunas `VIRTUAL` e `STORED` na mesma tabela (claro que não na mesma coluna).

Uma coluna gerada pode fazer referência a outras colunas geradas, desde que elas tenham sido definidas antes na definição da tabela. Com relação às colunas base (não-geradas), é possível fazer referência a qualquer uma (exceto colunas com auto incremento), mesmo que sua definição ocorra posteriormente na tabela.

Não é possível usar a opção `AUTO_INCREMENT` em um campo calculado.

## Exemplos

Como primeiro exemplo, vamos criar uma tabela de nome `tbl_mult`, que contém três campos numéricos: dois com dados inseridos pelo usuário (`num1` e `num2`) e um terceiro gerado pela multiplicação de `num1` por `num2` (`num1 * num2`):

```sql
CREATE TABLE tbl_mult (
  ID SMALLINT PRIMARY KEY AUTO_INCREMENT,
  num1 SMALLINT NOT NULL,
  num2 SMALLINT NOT NULL,
  num3 SMALLINT GENERATED ALWAYS AS (num1 * num2) VIRTUAL
);
```

Como criamos a coluna gerada como `VIRTUAL`, seus dados não ficam armazenados em disco.

Podemos inserir alguns registros na tabela para testar a geração dos dados no campo calculado `num3`:

```sql
INSERT INTO tbl_mult (num1, num2)
VALUES (2,1), (2,2), (2,3), (2,4);
```

E verificar os dados calculados realizando uma consulta à tabela:

```sql
SELECT * FROM tbl_mult;
```

Veja que os dados na coluna `num3` mostram o resultado do cálculo especificado em cada linha da tabela.

### Exemplo 2

Vejamos outro exemplo. Suponha uma tabela de vendas contendo os campos `Preco_Produto`, `Qtde`, `Desconto` e `Preco_Total`. Queremos criar essa tabela de modo que o campo `Preco_Total` seja calculado dinamicamente, multiplicando o preço do produto pela quantidade (adquirida), e aplicando um desconto percentual especificado na coluna `Desconto` ao preço total. Queremos também persistir o valor calculado na tabela:

```sql
CREATE TABLE tbl_Vendas (
 ID_Venda SMALLINT PRIMARY KEY AUTO_INCREMENT,
 Preco_Produto DECIMAL(6,2) NOT NULL,
 Qtde TINYINT NOT NULL,
 Desconto DECIMAL(4,2) NOT NULL,
 Preco_Total DECIMAL(6,2) AS (Preco_Produto * Qtde * (1 - Desconto / 100)) STORED
);
```

Podemos inserir alguns dados de vendas na tabela e depois verificar se o preço total foi calculado corretamente:

```sql
INSERT INTO tbl_Vendas (Preco_Produto, Qtde, Desconto)
VALUES
(50.00, 2, 20),
(65.00, 3, 15),
(100.00, 1, 12),
(132.00, 3, 18);
```

Agora vamos efetuar a consulta para visualizar os dados na tabela:

```sql
SELECT * FROM tbl_Vendas;
```

Note que o campo `Preco_Total` possui os preços calculados corretamente para cada produto vendido.

**Observações importantes:**
- Uma coluna calculada não pode ter a restrição `NOT NULL` aplicada, e também não pode ter dados inseridos por uma declaração `INSERT` e nem modificados por um `UPDATE`.
- Também não pode ser utilizada com definições de restrição `DEFAULT` e `FOREIGN KEY` (chave estrangeira).
- Não é necessário especificar o tipo de dados do campo calculado ao criar a tabela.
- Colunas persistidas ocupam mais espaço em disco do que colunas calculadas virtuais (sem `PERSISTED`).


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>