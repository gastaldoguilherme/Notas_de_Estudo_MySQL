> **Estruturas de Repetição – ITERATE**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Estruturas de Repetição – ITERATE 

Vamos finalizar nesta lição nosso estudo sobre estruturas de repetição em MySQL apresentando a declaração ITERATE, que pode ser usada nas estruturas LOOP, REPEAT e WHILE vistas anteriormente.

### Declaração ITERATE

ITERATE significa, dentro do contexto de uma estrutura de repetição, "inicie o loop novamente".

### Exemplo da Declaração ITERATE

```sql
DELIMITER //
CREATE PROCEDURE acumula_iterate (limite TINYINT UNSIGNED)
BEGIN
    DECLARE contador TINYINT UNSIGNED DEFAULT 0;
    DECLARE soma INT UNSIGNED DEFAULT 0;
    teste: LOOP
        SET contador = contador + 1;
        SET soma = soma + contador;
        IF contador < limite THEN
            ITERATE teste;
        END IF;
        LEAVE teste;
    END LOOP teste;
    SELECT soma;
END//
DELIMITER;

-- Vamos testar o exemplo apresentado:
CALL acumula_iterate (50);
```

### Vamos a outro exemplo de ITERATE:

```sql
DELIMITER //
CREATE PROCEDURE pares(limite TINYINT UNSIGNED)
main: BEGIN
    DECLARE contador TINYINT DEFAULT 0;
    meuloop: WHILE contador < limite DO
        SET contador = contador + 1;
        IF MOD(contador, 2) THEN
            ITERATE meuloop;
        END IF;
        SELECT CONCAT(contador, ' é um número par') AS Valor;
    END WHILE;
END//
DELIMITER;

-- Para testar:
CALL pares(12);
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>