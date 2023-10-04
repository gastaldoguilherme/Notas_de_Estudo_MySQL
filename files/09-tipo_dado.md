> **Tipos de Dados**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Tipos de Dados Comuns no MySQL

### Tipos Numéricos com Ponto Decimal

- **DECIMAL(M,D):** Ponto decimal com M dígitos no total (precisão) e D casas decimais (escala); o padrão é 10,0; M vai até 65 e D até 30.
- **FLOAT(M,D):** Ponto flutuante com precisão M e escala D; o padrão é 10,2; D vai até 24.

### Tipos de Dados de Texto

- **CHAR(M):** String que ocupa tamanho fixo entre 0 e 255 caracteres.
- **BOOL / BOOLEAN:** Valores binários 0 / 1; na verdade, é um alias para o tipo TINYINT(1).
- **VARCHAR(M):** String de tamanho variável, até 65535 caracteres.
- **BLOB / MEDIUMBLOB / TINYBLOB:** Campo com tamanho máximo de 65535 caracteres binários; 'Binary Large Objects', são usados para armazenar grandes quantidades de dados, como imagens.
- **MEDIUMTEXT:** Permite armazenar até 16.777.215 caracteres.
- **LONGTEXT:** Permite armazenar até 4.294.967.295 caracteres.

### Tipos de Dados de Data e Hora

- **DATE:** Uma data de 01/01/1000 a 31/12/9999, no formato YYYY-MM-DD.
- **DATETIME:** Uma combinação de data e hora de 01/01/1000 00:00:00 a 31/12/9999 23:59:59, no formato YYYY-MM-DD HH:MM:SS.
- **TIME:** Hora apenas, no formato HH:MM:SS.
- **YEAR(M):** Ano nos formatos de 2 ou 4 dígitos; se forem 2 (YEAR(2)), o ano vai de 1970 a 2069; para 4 (YEAR(4)), vai de 1901 a 2155. O padrão é 4.

### Tipos Inteiros em MySQL

Os tipos inteiros são tipos que não incluem a parte decimal. Por padrão, esses tipos podem armazenar números positivos e negativos. Mas é possível aplicar o atributo UNSIGNED na criação da tabela para impedir que valores negativos sejam armazenados na coluna. Além disso, ao usar esse atributo, a faixa de valores positivos permissíveis para armazenamento é duplicada.

Outro atributo que podemos utilizar com os tipos inteiros é o atributo ZEROFILL. Este atributo faz com que o número seja exibido com preenchimento de zeros à esquerda em uma consulta, até o tamanho máximo de 10 dígitos; esse tamanho máximo pode ser modificado especificando-se o número de dígitos desejados entre parênteses durante a criação da tabela.

Se o atributo ZEROFILL for empregado, a coluna automaticamente terá o atributo UNSIGNED ativado.

A seguir temos os tipos inteiros disponíveis em MySQL:

| Tipo      | Tamanho em Bytes | Faixas de Valores                                |
|-----------|------------------|-------------------------------------------------|
| BIGINT    | 8                | SIGNED: -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807<br>UNSIGNED: 0 a 18.446.744.073.709.551.615 |
| INT       | 4                | SIGNED: -2.147.483.648 a 2.147.483.647<br>UNSIGNED: 0 a 4.294.967.295                  |
| MEDIUMINT | 3                | SIGNED: -8.388.608 a 8.388.607<br>UNSIGNED: 0 a 16.777.215                             |
| SMALLINT  | 2                | SIGNED: -32.768 a 32.767<br>UNSIGNED: 0 a 65.535                                        |
| TINYINT   | 1                | SIGNED: -128 a 127<br>UNSIGNED: 0 a 255                                              |

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>