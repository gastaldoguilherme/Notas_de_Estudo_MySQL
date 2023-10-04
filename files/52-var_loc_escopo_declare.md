> **Variáveis Locais e Escopo em MySQL**      
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## Variáveis Locais e Escopo em MySQL ## 

Em MySQL, as variáveis locais são essenciais para armazenar e manipular valores temporários dentro de funções, procedimentos armazenados ou blocos BEGIN...END. O comando `DECLARE` é usado para criar variáveis locais e definir o seu tipo de dado.

Aqui está a sintaxe básica para declarar uma variável local em MySQL:

```sql
DECLARE nome_da_variavel tipo_de_dado [DEFAULT valor_inicial];
```


- `nome_da_variavel`: O nome que você deseja dar à variável.
- `tipo_de_dado`: O tipo de dado que a variável irá armazenar, como INT, VARCHAR, DECIMAL, entre outros.
- `DEFAULT valor_inicial` (opcional): Um valor inicial que pode ser atribuído à variável no momento da declaração.

Após declarada, a variável pode ser usada para armazenar valores temporários e realizar cálculos dentro do escopo em que foi definida. É importante notar que as variáveis locais têm um escopo limitado ao bloco em que foram declaradas. Isso significa que elas só podem ser acessadas e utilizadas dentro desse bloco, seja um procedimento armazenado, função ou um bloco BEGIN...END.

Aqui está um exemplo de como declarar e usar uma variável local em um procedimento armazenado simples:

```sql
DELIMITER //
CREATE PROCEDURE exemplo_procedimento()
BEGIN
    DECLARE contador INT DEFAULT 0;
    SET contador = 1;
    SELECT contador;
END //
DELIMITER ;
```

Neste exemplo, criamos uma variável local chamada `contador` do tipo INT e atribuímos o valor inicial 0. Dentro do procedimento, atualizamos o valor da variável para 1 e, em seguida, a selecionamos. A variável `contador` só é visível e acessível dentro deste procedimento.

Além disso, você pode usar variáveis locais em expressões, cálculos e em conjunto com comandos SQL para realizar tarefas mais complexas. Por exemplo:

```sql
DELIMITER //
CREATE PROCEDURE calcular_soma(IN num1 INT, IN num2 INT)
BEGIN
    DECLARE resultado INT DEFAULT 0;
    SET resultado = num1 + num2;
    SELECT resultado;
END //
DELIMITER ;
```

Neste procedimento, declaramos uma variável `resultado` para calcular a soma de dois números passados como parâmetros (num1 e num2). A variável `resultado` armazena o resultado da soma e é selecionada no final do procedimento.

As variáveis locais e o comando `DECLARE` são componentes poderosos para o desenvolvimento de procedimentos armazenados e funções em MySQL. Eles permitem armazenar e manipular temporariamente dados dentro do escopo de um bloco de código, o que é fundamental para executar operações complexas e eficazes em bancos de dados. Certifique-se de que as variáveis tenham nomes exclusivos para evitar conflitos em blocos de código maiores ou em chamadas de procedimentos aninhados.

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>