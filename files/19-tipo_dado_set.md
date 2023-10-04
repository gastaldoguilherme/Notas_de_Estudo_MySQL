> **Tipo de Dados SET**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Tipo de Dados SET 

O tipo de dados SET em MySQL é um objeto string que pode ter zero ou mais valores (membros), cada um dos quais deve ser escolhido a partir de uma lista de valores permitidos, que são especificados quando a tabela é criada.

Ao criar uma coluna do tipo SET, especificamos seus membros – os valores válidos – separando cada item com vírgulas. Desta forma, não é possível usar vírgulas nos nomes dos próprios itens.

Uma coluna do tipo SET pode ter no máximo 64 membros. Além disso, uma tabela não pode ter mais de 255 elementos do tipo listas de itens, como ENUM e SET. Os valores SET são armazenados como valores numéricos pelo MySQL.

| Tipo  | Tam. em Bytes | Descrição                               |
|-------|---------------|-----------------------------------------|
| SET   | 1-8           | Permite armazenar zero ou mais valores selecionados de uma lista de valores aceitáveis. |

### Exemplo de Aplicação

Vamos supor uma tabela de cadastro de pedidos de lanches em uma lanchonete, que oferece a possibilidade aos clientes de selecionar quais temperos serão adicionados a cada lanche, podendo-se acrescentar de 1 a 5 temperos, ou mesmo não acrescentar nenhum. Os temperos serão sempre os mesmos, não sendo necessário acrescentar nem tirar nenhum deles desta lista.

Neste caso, podemos inserir os temperos como um conjunto do tipo SET ao criarmos a tabela (que chamaremos de "pedidos"), configurando uma coluna com esse tipo de dado (chamaremos a essa coluna de "tempero").

Os temperos disponíveis em nosso exemplo serão os seguintes:
- Azeite
- Vinagre
- Sal
- Orégano
- Pimenta

Usaremos uma enumeração para criar a coluna de lanches, pois os lanches também são “fixos”, ou seja, não há a possibilidade de escolher lanches que não estejam no cardápio.

Precisamos criar a tabela de pedidos para realizarmos nossos testes:

```sql
CREATE TABLE pedidos (
  idPedido SMALLINT PRIMARY KEY AUTO_INCREMENT,
  lanche ENUM ('Presunto','Frango','Salame'),
  tempero SET ('Azeite','Vinagre','Sal','Orégano','Pimenta')
);
```

Vamos inserir quatro registros de pedidos na tabela. Um dos lanches não terá nenhum tempero, e os demais terão entre dois e três temperos escolhidos:

```sql
INSERT INTO pedidos (lanche, tempero)
VALUES
('Presunto','Sal,Orégano'),
('Salame','Azeite,Pimenta'),
('Frango','Azeite,Sal,Orégano'),
('Presunto','');
```

Vamos consultar os registros inseridos na tabela de pedidos:

```sql
SELECT * FROM pedidos;
```



Note que, como o pedido #4 é um lanche de presunto sem nenhum tempero desejado, a coluna "tempero" aparece vazia neste registro.

### Tratamento de Valores Não Permitidos

O que acontece se tentarmos inserir um valor que não está presente na lista de valores permissíveis da coluna de temperos, como, por exemplo, Mostarda? Vejamos o que ocorre:

```sql
INSERT INTO pedidos (lanche, tempero)
VALUES ('Frango','Sal,Mostarda');
```

### Consultando Valores em Colunas SET

Podemos consultar os pedidos que levam algum tempero em particular usando o operador LIKE. Por exemplo, para ver os pedidos que devem levar Azeite, executamos:

```sql
SELECT * FROM pedidos
WHERE tempero LIKE '%Azeite%';
```

Ou ainda usando a função do MySQL FIND_IN_SET():

```sql
SELECT * FROM pedidos
WHERE FIND_IN_SET('Azeite',tempero) > 0;
```


E para retornar os pedidos que possuem mais de um tempero adicionado, como por exemplo lanches que levem Pimenta e Azeite, podemos combinar operadores LIKE:

```sql
SELECT * FROM pedidos
WHERE tempero LIKE '%Pimenta%' AND tempero LIKE '%Azeite%';
```



&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>