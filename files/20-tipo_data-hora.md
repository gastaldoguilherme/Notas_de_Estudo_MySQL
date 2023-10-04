> **Data e Hora**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Data e Hora no MySQL

Existem cinco tipos que permitem armazenar informações sobre tempo (data e hora) no MySQL. São eles: DATE, TIME, DATETIME, TIMESTAMP e YEAR.

No geral, usamos o tipo TIMESTAMP para armazenar informações sobre o momento em que um registro é inserido ou atualizado na tabela. Sempre que uma coluna do tipo TIMESTAMP é alterada, a hora e data atuais são armazenadas automaticamente.

Para armazenar outras datas comuns, como a data de nascimento de uma pessoa, devemos usar o tipo DATETIME ou ainda o tipo DATE, se a informação de horário não for importante.

O tipo TIMESTAMP possui um problema: só é possível armazenar datas até o ano 2038. Esse é o "problema do ano 2K38" ou ainda "Bug do Milênio do Unix". Caso seja necessário armazenar datas além desse ano, deve-se obrigatoriamente usar o tipo DATETIME - lembrando que esse tipo ocupa o dobro do espaço do TIMESTAMP.

A tabela a seguir mostra os tipos de data e hora no MySQL com informações sobre cada um:

| Tipo      | Tam. Bytes | Descrição                                                |
|-----------|------------|----------------------------------------------------------|
| DATE      | 3          | Datas entre 01/Jan/1000 até 31/Dez/9999. Formato padrão: "aaaa-mm-dd" |
| TIME      | 3          | Horas na faixa entre -838:59:59 até 838:59:59. Formato padrão: "hh;mm:ss" |
| DATETIME  | 8          | Combinação de data e hora. Faixa de 01/Jan/1970 até 31/Dez/9999. Formato padrão: "aaaa-mm-dd hh:mm:ss". |
| TIMESTAMP | 4          | Combinação de data e hora. Faixa de 01/Jan/1970 até o ano 2037. Formato padrão: "aaaa-mm-dd hh:mm:ss". |
| YEAR[(2|4)] | 1       | Ano nos formatos de 2 ou 4 dígitos. O padrão é ano com quatro dígitos, com valores permissíveis de 1901 a 2155. Já no formato de 2 dígitos, o intervalo aceito é de (19)70 até (20)69. |

### Exemplos

Vejamos um exemplo do emprego de tipos de data e hora em MySQL.

1. Vamos criar uma tabela chamada "venda" contendo quatro colunas: idVenda, horaVenda, dataEntrega e horaEntrega:

```sql
CREATE TABLE venda (
  idVenda SMALLINT PRIMARY KEY AUTO_INCREMENT,
  horaVenda TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  dataEntrega DATE,
  horaEntrega TIME
);
```

E vamos inserir um registro nesta tabela:

```sql
INSERT INTO venda (dataEntrega, horaEntrega)
VALUES ("2018-12-03", "13:40:00");
```

Note que não inserimos um valor para a coluna horaVenda, pois ela recebe o valor padrão CURRENT_TIMESTAMP, que significa a data e hora atuais do sistema no momento da inserção do registro. Podemos inserir um timestamp diferente se for necessário.

Também é possível ignorar os hífens e os sinais de dois-pontos ao inserir os dados com INSERT:

```sql
INSERT INTO venda (dataEntrega, horaEntrega)
VALUES ("20181203", "134000");
```

Consultando a tabela:

```sql
SELECT * FROM venda;
```

Como podemos ver, as datas e horário foram armazenados corretamente e pudemos consultar os dados na tabela sem problemas.

&nbsp;    

&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>