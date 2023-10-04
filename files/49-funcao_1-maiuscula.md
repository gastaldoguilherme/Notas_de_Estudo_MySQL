> **Função para Capitalizar a Inicial de uma Frase ou Palavra**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Colocar a Inicial de uma Palavra ou String em Maiúscula

Ao inserirmos registros em uma tabela no MySQL, é comum que alguns campos precisem ser capitalizados da forma adequada. 
Por exemplo, siglas normalmente devem ser armazenadas em maiúsculas, e nomes próprios (pessoas, lugares, etc) com a primeira letra maiúscula apenas.

Para converter todas as letras de uma palavra para maiúsculas, o MySQL fornece uma função (muito útil), que é a função UCASE(). Porém, se precisarmos garantir que a primeira letra de uma string fique em maiúscula, sem no entanto alterar os demais caracteres, não encontraremos uma função pronta no MySQL. Nesse caso, devemos criar uma função própria para essa tarefa.

### Função para Capitalizar a Inicial de uma Frase ou Palavra

A função a seguir, batizada de `inicial_maiuscula`, recebe uma string de texto como argumento e converte a primeira letra dessa string para maiúscula:

```sql
DROP FUNCTION IF EXISTS inicial_maiuscula;
DELIMITER //
CREATE FUNCTION inicial_maiuscula(texto VARCHAR(100))
RETURNS VARCHAR(100)
BEGIN
    RETURN CONCAT(UPPER(LEFT(texto, 1)),SUBSTRING(texto, 2));
END //
DELIMITER ;
```

A função recebe uma string por meio do parâmetro `texto`, criado como um VARCHAR de até 100 caracteres. Esse tamanho pode ser alterado à vontade, de acordo com sua necessidade.

Nossa função também emprega quatro funções internas de manipulação de strings do MySQL:

- `CONCAT(string1, string2, …)`: Retorna uma string que resulta da concatenação dos argumentos (string1, string2, …) passados à função.
- `UPPER(string)`: Retorna a string passada como argumento com todos os caracteres alterados para caixa-alta (em maiúsculas), de acordo com o mapa de caracteres atual do banco de dados. A função UCASE é um sinônimo de UPPER.
- `LEFT(string, n)`: Retorna os n caracteres à esquerda de uma string passada como argumento, ou NULL se um dos argumentos for NULL.
- `SUBSTRING(string, pos)`: Retorna uma substring a partir de uma string passada como argumento, iniciando na posição pos.

A função `LEFT` retorna o primeiro caractere à esquerda da string passada à função, que no caso será o caractere inicial que desejamos converter para maiúscula. A função `SUBSTRING` retorna os caracteres subsequentes, do segundo até o último, que desejamos manter como estão, independente de estarem em maiúsculas ou minúsculas.

O caractere retornado por `LEFT` é passado à função `UPPER`, que retorna esse caractere convertido em caixa-alta (maiúscula).

Os retornos de `UPPER` e `SUBSTRING` são então concatenados com o emprego da função `CONCAT`, reconstruindo assim a string original, porém com o primeiro caractere convertido em maiúscula.

### Testando

```sql
SELECT inicial_maiuscula('fábio'),
inicial_maiuscula('frase iniciada em minúscula'),
inicial_maiuscula('PIZZA'),
inicial_maiuscula('pANDEMIA');
```

**Resultado:**

Inicial maiúscula em strings no MySQL


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>