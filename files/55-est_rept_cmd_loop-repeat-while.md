> **Estruturas de Repetição: LOOP - REPEAT - WHILE**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Estruturas de Repetição: LOOP - REPEAT - WHILE

### Blocos Iterativos

Um bloco iterativo é um bloco de código que é executado repetidamente por um comando especial até que uma condição de parada o interrompa.

Um bloco iterativo pode ser aninhado com outros blocos iterativos.

O MySQL possui três tipos básicos de blocos iterativos:

- LOOP
- REPEAT
- WHILE

---
## Comando LOOP

### Sintaxe:

```
[<rótulo>:] LOOP
declarações
END LOOP [<rótulo>];
```

### Exemplo do Comando LOOP

```sql
DELIMITER //
CREATE PROCEDURE acumula (limite INT)
BEGIN
    DECLARE contador INT DEFAULT 0;
    DECLARE soma INT DEFAULT 0;
    loop_teste: LOOP
        SET contador = contador + 1;
        SET soma = soma + contador;
        IF contador >= limite THEN
            LEAVE loop_teste;
        END IF;
    END LOOP loop_teste;
    SELECT soma;
END//
DELIMITER ;

-- Testando
CALL acumula(10);
```
&nbsp;

---
## Comando REPEAT

### Sintaxe:

```
[<rótulo>:] REPEAT
declarações
UNTIL condição
END REPEAT [<rótulo>];
```

### Exemplo do Comando REPEAT no MySQL

```sql
CREATE PROCEDURE acumula_repita (limite TINYINT UNSIGNED)
BEGIN
    DECLARE contador TINYINT UNSIGNED DEFAULT 0;
    DECLARE soma INT DEFAULT 0;
    REPEAT
        SET contador = contador + 1;
        SET soma = soma + contador;
    UNTIL contador >= limite
    END REPEAT;
    SELECT soma;
END//
DELIMITER ;

-- Testando a estrutura REPITA:
CALL acumula_repita(10);
CALL acumula_repita(0); -- Este resulta em valor errado, pois
-- o contador é incrementado ANTES do teste condicional.
```

### Exemplo do Comando REPEAT com a Cláusula LEAVE:

```sql
-- Resolvendo o problema do teste de REPITA
DROP PROCEDURE IF EXISTS acumula_repita;
DELIMITER //
CREATE PROCEDURE acumula_repita (limite TINYINT UNSIGNED)
main: BEGIN
    DECLARE contador TINYINT UNSIGNED DEFAULT 0;
    DECLARE soma INT DEFAULT 0;
    IF limite < 1 THEN
        SELECT 'O valor deve ser maior que zero.' AS Erro;
        LEAVE main;
    END IF;
    REPEAT
        SET contador = contador + 1;
        SET soma = soma + contador;
    UNTIL contador >= limite
    END REPEAT;
    SELECT soma;
END//
DELIMITER ;

-- Testando a estrutura REPITA:
CALL acumula_repita(10);
CALL acumula_repita(0); -- Agora o erro é reportado.
```
&nbsp;

---
## Comando WHILE

O comando WHILE somente executa as declarações contidas em seu corpo se a condição testada retornar o valor TRUE (verdadeiro).

### Sintaxe:

```
[<rótulo>:] WHILE condição DO
    declarações
END WHILE [<rótulo>];
```

### Exemplo do Comando WHILE

```sql
DELIMITER //
CREATE PROCEDURE acumula_while (limite TINYINT UNSIGNED)
BEGIN
    DECLARE contador TINYINT UNSIGNED DEFAULT 0;
    DECLARE soma INT DEFAULT 0;
    WHILE contador < limite DO
        SET contador = contador + 1;
        SET soma = soma + contador;
    END WHILE;
    SELECT soma;
END//
DELIMITER ;

-- Testando:
CALL acumula_while(10);
CALL acumula_while(0);
```

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>