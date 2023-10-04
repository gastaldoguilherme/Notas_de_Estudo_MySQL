> **Tipo de Dados ENUM**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Tipo de Dados ENUM no MySQL

O tipo de dados ENUM é um objeto string cujo valor é escolhido a partir de uma lista de valores permitidos, enumerados de forma explícita durante a especificação de uma coluna, quando uma tabela é criada.

É uma forma de economizar espaço em disco quando se sabe de antemão que a coluna só poderá armazenar um conjunto limitado de valores. Isso ocorre porque os valores são codificados internamente automaticamente como números, independente dos dados armazenados serem números, strings, etc.; assim, independente do tamanho do dado inserido na coluna, cada registro ocupará apenas um byte de espaço neste campo.

| Tipo  | Tam. em Bytes | Descrição                               |
|-------|---------------|-----------------------------------------|
| ENUM  | 1-2           | Permite armazenar um valor selecionado de uma lista de valores aceitáveis. |

### Como Criar uma Coluna do Tipo ENUM

Declaramos uma coluna do tipo ENUM ao criarmos uma tabela, passando os valores que serão armazenados entre parênteses, separados por vírgulas e individualmente envoltos entre aspas. Veja o exemplo:

```sql
CREATE TABLE camisas (
  idCamisa TINYINT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(25),
  tamanho ENUM('pequena','média','grande','extra-grande')
);
```

A coluna "tamanho" é uma enumeração que consiste nos quatro tamanhos possíveis para camisas a serem registradas na tabela.

Vamos inserir um registro nesta tabela, por exemplo, uma camisa regata tamanho grande:

```sql
INSERT INTO camisas (nome, tamanho)
VALUES ('regata', 'grande');
```

E então realizar uma consulta simples para verificar a inserção dos dados:

```sql
SELECT * FROM camisas;
```

### Tipo ENUM no MySQL

Vamos tentar inserir agora um registro de uma camisa social, porém escrevendo o tamanho “large” (que não consta na lista de enumeração):

```sql
INSERT INTO camisas (nome, tamanho)
VALUES ('social', 'medium');
```

Agora ocorrerá um erro, pois o valor “medium” não consta na enumeração, e o registro não será inserido.


Alterando o valor inserido para “média” resolve o problema. Vamos aproveitar e inserir mais alguns registros:

```sql
INSERT INTO camisas (nome, tamanho)
VALUES
('social', 'média'),
('polo', 'pequena'),
('polo', 'grande'),
('camiseta', 'extra-grande');
```

Uma coluna do tipo enum pode ter no máximo 65.535 elementos atribuídos.

Podemos consultar os valores permissíveis para uma coluna do tipo enum com a declaração seguinte:

```sql
SHOW COLUMNS
FROM camisas
LIKE 'tamanho';
```



Além disso, podemos visualizar os números de índice dos valores enumerados armazenados consultando a coluna enum em um contexto numérico, como na seguinte declaração:

```sql
SELECT nome, tamanho+0
FROM camisas;
```



Note que há duas camisas com o mesmo número de índice associado (regata e polo) – isso ocorre porque ambas possuem o mesmo tamanho (grande, índice 3).

### Problemas com o Tipo ENUM

Um problema típico do tipo enum em MySQL é a aplicação da cláusula ORDER BY para tentar ordenar os resultados de uma consulta pela coluna deste tipo. A ordenação padrão mostra os elementos na ordem em que foram inseridos (ordem de seus índices), e não em ordem alfabética. Veja o exemplo:

```sql
SELECT * FROM camisas
ORDER BY tamanho;
```

Resultado:


Claramente o resultado não foi o que esperávamos. Porém, podemos consertar isso executando o ORDER BY combinado com CAST, da seguinte maneira:

```sql
SELECT * FROM camisas
ORDER BY CAST(tamanho AS CHAR);
```

Resultado:


Agora sim, resultado ordenado por tamanho em ordem alfabética.

Não é recomendado usar valores numéricos em uma coluna do tipo enum, pois neste caso não haverá economia de espaço de armazenamento (em relação a valores SMALLINT e TINYINT), além do risco de haver confusão entre o valor armazenado e o número empregado para representá-lo internamente.

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>