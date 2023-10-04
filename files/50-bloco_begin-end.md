> **Funções e Procedimentos Armazenados - Blocos BEGIN .. END**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## Blocos BEGIN .. END em Funções e Procedimentos Armazenados

Em MySQL, os blocos `BEGIN...END` são usados para criar seções de código delimitadas que podem conter um ou mais comandos SQL, declarações de variáveis, estruturas de controle de fluxo e até mesmo chamadas de funções ou procedimentos. Eles são especialmente úteis quando se trabalha com funções e procedimentos armazenados, permitindo criar lógica personalizada para manipular os dados no banco de dados.


### Funções Armazenadas (stored functions)


Funções Armazendas em MySQL podem usar blocos `BEGIN ... END` para agrupar múltiplas instruções SQL e lógica condicional. Isso permite que você crie funções mais complexas que realizam várias operações dentro do corpo da função. Um bloco `BEGIN ... END` em uma função MySQL se parece com isto:


Vou fornecer um exemplo de aplicação de blocos `BEGIN ... END` em funções armazenadas em MySQL e como invocá-los:

**Exemplo de Aplicação (Função Armazenada):**

Suponha que você queira criar uma função que calcule o salário líquido de um funcionário com base em seu salário bruto e deduza os impostos e outras deduções. Você pode usar um bloco `BEGIN ... END` para organizar a lógica de cálculo em uma função.

```sql
DELIMITER //
CREATE FUNCTION calcular_salario_liquido(salario_bruto DECIMAL(10, 2))
RETURNS DECIMAL(10, 2)
BEGIN
    DECLARE salario_liquido DECIMAL(10, 2);

    -- Cálculos
    SET salario_liquido = salario_bruto - (salario_bruto * 0.2); -- Dedução de 20% para impostos

    -- Mais deduções e cálculos podem ser adicionados aqui

    RETURN salario_liquido;
END //
DELIMITER ;
```

Neste exemplo, a função `calcular_salario_liquido` recebe um salário bruto como entrada e calcula o salário líquido após deduções de impostos. A lógica está contida dentro do bloco `BEGIN ... END`.

**Exemplo de Invocação (Chamada da Função):**

Você pode invocar essa função passando um valor de salário bruto e obtendo o salário líquido calculado.

```sql
SELECT calcular_salario_liquido(5000.00); -- Chama a função com um salário bruto de 5000.00
```

Neste exemplo, a função é chamada com um salário bruto de 5000.00, e o resultado será o salário líquido calculado (após deduções) retornado pela função.

Este é um exemplo simples que demonstra como usar blocos `BEGIN ... END` em funções armazenadas para encapsular a lógica de cálculo e tornar o código mais organizado e reutilizável.



### Procedimentos Armazenados (stored procedure)

A sintaxe básica de um bloco `BEGIN...END` em MySQL é a seguinte:

```sql
DELIMITER //
CREATE PROCEDURE nome_procedimento()
BEGIN
    -- código SQL e lógica aqui
END //
DELIMITER ;
```

Aqui estão os elementos principais que compõem um bloco `BEGIN...END`:

1. **DELIMITER**: O comando `DELIMITER` é usado para alterar o delimitador padrão (`;`) para outro caractere, como `//`. Isso é necessário para que o MySQL interprete corretamente o bloco de código como um todo.

2. **CREATE PROCEDURE**: Este é o início da definição de um procedimento armazenado. Você pode substituir `PROCEDURE` por `FUNCTION` se estiver criando uma função em vez de um procedimento.

3. **nome_procedimento()**: Aqui, você fornece o nome do procedimento ou função que está criando, seguido de parênteses que podem conter parâmetros de entrada, se aplicável.

4. **BEGIN**: O comando `BEGIN` marca o início do bloco de código do procedimento ou função.

5. **-- código SQL e lógica aqui**: Dentro do bloco `BEGIN...END`, você escreve seu código SQL e lógica de programação. Isso pode incluir comandos SQL como SELECT, INSERT, UPDATE, DELETE, bem como declarações de variáveis, estruturas de controle (IF, WHILE, etc.), chamadas de outras funções ou procedimentos e muito mais.

6. **END**: O comando `END` marca o final do bloco de código do procedimento ou função.

7. **DELIMITER ;**: Este comando restaura o delimitador padrão para `;` após o bloco `BEGIN...END` ser definido. Isso é importante para evitar conflitos com os comandos SQL normais que usam `;` como delimitador.

Agora, vejamos um exemplo de como usar um bloco `BEGIN...END` em um procedimento armazenado que simplesmente atualiza o preço de todos os produtos em uma tabela multiplicando-o por 1,1 (aumento de 10%):

**Exemplo 1 de Aplicação (Procedimento Armazenado):**

```sql
DELIMITER //
CREATE PROCEDURE aumentar_preco_produtos()
BEGIN
    UPDATE produtos
    SET preco = preco * 1.1;
END //
DELIMITER ;
```

Neste exemplo, o bloco `BEGIN...END` contém um único comando SQL (UPDATE) que aumenta os preços dos produtos na tabela. Você pode criar procedimentos e funções mais complexos usando blocos `BEGIN...END` para agrupar várias instruções e lógica.

Os blocos `BEGIN...END` em MySQL são ferramentas poderosas para criar procedimentos e funções personalizados que podem executar tarefas específicas no banco de dados, proporcionando maior flexibilidade e reutilização de código. Eles são amplamente utilizados em cenários de programação de banco de dados para melhorar a eficiência e a manutenção do código.


**Exemplo 2 de Aplicação (Procedimento Armazenado):**

Suponha que você deseje criar um procedimento armazenado que atualize o salário de um funcionário e registre essa alteração em um histórico de salários. Você pode usar um bloco `BEGIN ... END` para organizar essa lógica em um procedimento.

```sql
DELIMITER //
CREATE PROCEDURE atualizar_salario(id_funcionario INT, novo_salario DECIMAL(10, 2))
BEGIN
    DECLARE salario_anterior DECIMAL(10, 2);

    -- Obter o salário anterior
    SELECT Salario INTO salario_anterior FROM funcionarios WHERE ID = id_funcionario;

    -- Atualizar o salário na tabela de funcionários
    UPDATE funcionarios SET Salario = novo_salario WHERE ID = id_funcionario;

    -- Registrar a alteração no histórico de salários
    INSERT INTO historico_salarios (ID_Funcionario, Salario_Anterior, Salario_Novo, Data) 
    VALUES (id_funcionario, salario_anterior, novo_salario, NOW());

    COMMIT;
END //
DELIMITER ;
```

Neste exemplo, o procedimento `atualizar_salario` recebe o ID do funcionário e o novo salário como parâmetros e utiliza um bloco `BEGIN ... END` para realizar as etapas de obtenção do salário anterior, atualização do salário na tabela de funcionários e registro da alteração no histórico de salários.

**Exemplo de Invocação (Chamada do Procedimento):**

Você pode invocar esse procedimento passando o ID do funcionário e o novo salário para efetuar a atualização e registro.

```sql
CALL atualizar_salario(1, 5500.00); -- Chama o procedimento para atualizar o salário do funcionário com ID 1 para 5500.00
```

Neste exemplo, o procedimento é chamado com o ID do funcionário e o novo salário desejado. O procedimento executará as operações definidas no bloco `BEGIN ... END` para atualizar o salário e registrar a alteração no histórico de salários.

Isso demonstra como os blocos `BEGIN ... END` são usados em procedimentos armazenados para organizar a lógica de manipulação de dados e realizar operações complexas no banco de dados MySQL.



&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>