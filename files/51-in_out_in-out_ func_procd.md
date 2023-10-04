> **Funções e Procedimentos Armazenados - Parâmetros IN, OUT e INOUT**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Funções Armazenadas

Funções armazenadas em MySQL podem usar parâmetros IN, OUT e INOUT, que permitem que a função receba valores de entrada, retorne valores de saída ou faça ambos, dependendo das necessidades.

### Parâmetro IN

 Os parâmetros IN são usados para passar valores de entrada para a função. Eles são usados para fornecer informações à função que ela usará em seu processamento, mas não podem ser modificados pela função. Para declarar um parâmetro IN, você simplesmente o lista na definição da função.

  Exemplo:
  ```sql
  CREATE FUNCTION minha_funcao(parametro_in INT)
  RETURNS INT
  BEGIN
      -- Lógica que utiliza o parâmetro de entrada parametro_in
      RETURN parametro_in * 2;
  END;
  ```


- **Exemplo de Aplicação:**
  Vamos criar uma função que calcula o imposto com base em um valor de compra fornecido como um parâmetro IN.

  ```sql
  DELIMITER //
  CREATE FUNCTION calcular_imposto(valor_compra DECIMAL(10, 2))
  RETURNS DECIMAL(10, 2)
  BEGIN
      DECLARE imposto DECIMAL(10, 2);
      SET imposto = valor_compra * 0.10; -- Imposto de 10%
      RETURN imposto;
  END;
  //
  DELIMITER ;
  ```

  Você pode chamar essa função passando um valor de compra e obter o valor do imposto calculado.

  ```sql
  SELECT calcular_imposto(100.00); -- Chama a função com um valor de compra de 100.00
  ```



### Parâmetro OUT

 Os parâmetros OUT são usados para retornar valores da função. Eles são declarados na definição da função e podem ser usados para retornar um ou mais valores calculados pela função. Os valores são definidos dentro da função e serão retornados quando a função for chamada.

  Exemplo:
  ```sql
  CREATE FUNCTION minha_funcao(parametro_in INT, OUT resultado_out INT)
  BEGIN
      -- Lógica que calcula o resultado
      SET resultado_out = parametro_in * 2;
  END;
  ```


- **Exemplo de Aplicação:**
  Vamos criar uma função que retorna o nome e o salário de um funcionário com base em seu ID, usando parâmetros OUT.

  ```sql
  DELIMITER //
  CREATE FUNCTION obter_informacoes_funcionario(id_funcionario INT, OUT nome VARCHAR(50), OUT salario DECIMAL(10, 2))
  BEGIN
      SELECT Nome, Salario INTO nome, salario FROM funcionarios WHERE ID = id_funcionario;
  END;
  //
  DELIMITER ;
  ```

  Você pode chamar essa função passando o ID do funcionário e recebendo os valores do nome e do salário como saída.

  ```sql
  DECLARE @nome VARCHAR(50);
  DECLARE @salario DECIMAL(10, 2);
  CALL obter_informacoes_funcionario(1, @nome, @salario);
  SELECT @nome, @salario;
  ```



### Parâmetro INOUT

 Os parâmetros INOUT são usados quando você deseja passar valores de entrada para a função e também deseja que a função retorne valores modificados que podem ser usados fora da função. Eles são uma combinação de parâmetros IN e OUT e são declarados na definição da função.

  Exemplo:
  ```sql
  CREATE FUNCTION minha_funcao(INOUT parametro_inout INT)
  BEGIN
      -- Lógica que utiliza e modifica o parâmetro parametro_inout
      SET parametro_inout = parametro_inout * 2;
  END;
  ```

Você pode usar esses tipos de parâmetros para criar funções armazenadas mais flexíveis e poderosas em MySQL, dependendo dos requisitos específicos da sua aplicação.


- **Exemplo de Aplicação:**
  Vamos criar uma função que aumenta o salário de um funcionário em um valor específico e também retorna o novo salário usando um parâmetro INOUT.

  ```sql
  DELIMITER //
  CREATE FUNCTION aumentar_salario(INOUT salario_atual DECIMAL(10, 2), aumento DECIMAL(10, 2))
  BEGIN
      SET salario_atual = salario_atual + aumento;
  END;
  //
  DELIMITER ;
  ```


  Você pode chamar essa função passando o salário atual como um parâmetro INOUT e especificando o aumento desejado. O valor do salário será atualizado dentro da função e também será retornado.

  ```sql
  DECLARE @salario DECIMAL(10, 2);
  SET @salario = 1000.00; -- Salário inicial
  CALL aumentar_salario(@salario, 200.00); -- Aumento de 200.00
  SELECT @salario; -- Novo valor do salário
  ```

&nbsp;


## Procedimentos Armazenados

### Parâmetros IN, OUT e INOUT em Procedimentos Armazenados 

Em MySQL, os procedimentos armazenados são uma parte fundamental para executar operações complexas no banco de dados. Os parâmetros são essenciais nesse contexto para passar informações para o procedimento e, em alguns casos, obter informações de volta. Existem três tipos de parâmetros que podem ser usados em procedimentos armazenados: IN, OUT e INOUT.

### Parâmetro IN

O parâmetro IN é usado para passar valores para o procedimento armazenado. É como uma entrada para a função. Dentro do procedimento, você pode usar esse valor, mas não pode modificá-lo. A sintaxe para criar um parâmetro IN em um procedimento armazenado é a seguinte:

```sql
CREATE PROCEDURE nome_procedimento(IN nome_parametro tipo_de_dados)
```

Aqui está um exemplo de um procedimento que usa um parâmetro IN para realizar uma consulta:

```sql
CREATE PROCEDURE consultar_cliente(IN id_cliente INT)
BEGIN
    SELECT * FROM clientes WHERE id = id_cliente;
END;
```

### Parâmetro OUT

O parâmetro OUT é usado para retornar valores do procedimento armazenado. É como uma saída da função. Dentro do procedimento, você pode modificar esse valor e, quando o procedimento for concluído, o valor atualizado será retornado. A sintaxe para criar um parâmetro OUT em um procedimento armazenado é a seguinte:

```sql
CREATE PROCEDURE nome_procedimento(OUT nome_parametro tipo_de_dados)
```

Aqui está um exemplo de um procedimento que usa um parâmetro OUT para calcular a média de preços de produtos e retorná-lo:

```sql
CREATE PROCEDURE calcular_media_precos(OUT media DECIMAL(10, 2))
BEGIN
    SELECT AVG(preco) INTO media FROM produtos;
END;
```

### Parâmetro INOUT

O parâmetro INOUT combina as funcionalidades do IN e OUT. Você pode passar um valor para o procedimento e também obter um valor atualizado de volta. A sintaxe para criar um parâmetro INOUT em um procedimento armazenado é a seguinte:

```sql
CREATE PROCEDURE nome_procedimento(INOUT nome_parametro tipo_de_dados)
```

Aqui está um exemplo de um procedimento que usa um parâmetro INOUT para calcular o aumento de preço de um produto e atualizar seu valor:

```sql
CREATE PROCEDURE calcular_aumento_preco(INOUT preco_antigo DECIMAL(10, 2), IN percentual_aumento DECIMAL(5, 2))
BEGIN
    SET preco_antigo = preco_antigo * (1 + (percentual_aumento / 100));
END;
```

Para chamar um procedimento armazenado que usa parâmetros IN, OUT ou INOUT, você pode usar a seguinte sintaxe:

```sql
CALL nome_procedimento(valor);
```

Onde nome_procedimento é o nome do seu procedimento armazenado e valor é o valor que você está passando ou recebendo, dependendo do tipo de parâmetro. Por exemplo:

```sql
-- Chamando o procedimento que usa um parâmetro IN
CALL consultar_cliente(1);

-- Chamando o procedimento que usa um parâmetro OUT
DECLARE @media DECIMAL(10, 2);
CALL calcular_media_precos(@media);
SELECT @media;

-- Chamando o procedimento que usa um parâmetro INOUT
DECLARE @preco DECIMAL(10, 2);
SET @preco = 50.00;
CALL calcular_aumento_preco(@preco, 10.00);
SELECT @preco;
```

Os parâmetros IN, OUT e INOUT em procedimentos armazenados são poderosas ferramentas para tornar seus procedimentos mais flexíveis e capazes de interagir com o banco de dados de maneira mais eficaz. Eles permitem que você passe informações para o procedimento, obtenha informações de volta e até mesmo modifique valores dentro do procedimento, tornando suas operações de banco de dados mais dinâmicas e personalizadas.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>