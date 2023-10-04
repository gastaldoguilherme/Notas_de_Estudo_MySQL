> **Blocos Condicionais IF – THEN – ELSEIF – ELSE e CASE**      
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## Blocos Condicionais IF – THEN – ELSEIF – ELSE e CASE em MySQL ## 

Em MySQL, os blocos condicionais IF – THEN – ELSEIF – ELSE e CASE são fundamentais para controlar o fluxo de execução do código em funções, procedimentos armazenados ou em instruções SQL condicionais, permitindo uma tomada de decisão mais complexa com base em várias condições.

## Blocos Condicionais IF – THEN – ELSEIF – ELSE: ## 

O bloco condicional IF – THEN – ELSEIF – ELSE permite que você execute diferentes ações com base em várias condições. Sua sintaxe básica é a seguinte:

```sql
IF condição1 THEN
    -- código a ser executado se condição1 for verdadeira
ELSEIF condição2 THEN
    -- código a ser executado se condição2 for verdadeira
ELSE
    -- código a ser executado se nenhuma das condições anteriores for verdadeira
END IF;
```

Principais elementos:

- `IF`: Inicia a estrutura condicional.
- `condição1`, `condição2`, etc.: As condições a serem avaliadas sequencialmente. Se uma das condições for verdadeira, o código correspondente é executado.
- `THEN`: Marca o início do código a ser executado se a condição for verdadeira.
- `ELSEIF`: Permite adicionar condições adicionais a serem verificadas.
- `ELSE`: Opcionalmente, você pode fornecer um bloco de código a ser executado se nenhuma das condições anteriores for verdadeira.
- `END IF;`: Finaliza o bloco condicional.

Aqui está um exemplo de uso do bloco IF – THEN – ELSEIF – ELSE em um procedimento armazenado que classifica um aluno com base em sua nota:

```sql
DELIMITER //
CREATE PROCEDURE classificar_aluno(IN nota INT)
BEGIN
    IF nota >= 90 THEN
        SELECT 'Excelente';
    ELSEIF nota >= 70 THEN
        SELECT 'Bom';
    ELSEIF nota >= 50 THEN
        SELECT 'Regular';
    ELSE
        SELECT 'Insuficiente';
    END IF;
END //
DELIMITER ;
```

Neste exemplo, o procedimento `classificar_aluno` aceita um parâmetro `nota` e, com base na nota fornecida, seleciona a classificação apropriada.

## Blocos Condicionais CASE: ## 

O bloco condicional CASE é usado quando você precisa avaliar uma expressão em relação a várias condições e executar código com base no resultado. A sintaxe básica é a seguinte:

```sql
CASE
    WHEN condição1 THEN
        -- código a ser executado se condição1 for verdadeira
    WHEN condição2 THEN
        -- código a ser executado se condição2 for verdadeira
    ELSE
        -- código a ser executado se nenhuma das condições anteriores for verdadeira
END CASE;
```

Principais elementos:

- `CASE`: Inicia a estrutura condicional.
- `WHEN condição THEN`: Define uma condição específica a ser avaliada e o código a ser executado se a condição for verdadeira.
- `ELSE`: Opcionalmente, você pode fornecer um bloco de código a ser executado se nenhuma das condições anteriores for verdadeira.
- `END CASE;`: Finaliza o bloco condicional.

Aqui está um exemplo de uso do bloco CASE em um procedimento armazenado que classifica um aluno com base em sua nota:

```sql
DELIMITER //
CREATE PROCEDURE classificar_aluno(IN nota INT)
BEGIN
    CASE
        WHEN nota >= 90 THEN
            SELECT 'Excelente';
        WHEN nota >= 70 THEN
            SELECT 'Bom';
        WHEN nota >= 50 THEN
            SELECT 'Regular';
        ELSE
            SELECT 'Insuficiente';
    END CASE;
END //
DELIMITER ;
```

Neste exemplo, o procedimento `classificar_aluno` aceita um parâmetro `nota` e, com base na nota fornecida, seleciona a classificação apropriada.

Em resumo, os blocos condicionais IF – THEN – ELSEIF – ELSE e CASE em MySQL são ferramentas essenciais para controlar o fluxo de execução em funções, procedimentos armazenados e instruções SQL condicionais. Eles permitem tomar decisões com base em múltiplas condições, melhorando a flexibilidade e a lógica de seus scripts SQL. Certifique-se de usar essas estruturas condicionais de forma apropriada para atender às necessidades do seu código.

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>