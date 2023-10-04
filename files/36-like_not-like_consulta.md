> **LIKE e NOT LIKE**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## LIKE e NOT LIKE

Quando realizamos uma consulta no MySQL, utilizamos a cláusula WHERE para realizar um filtro dos registros a retornar. Porém, com o WHERE, só podemos aplicar filtros de correspondência exata de palavras. E se precisarmos aplicar um filtro que verifique palavras de forma parcial, como palavras que iniciem ou terminem com determinados caracteres, ou que possuam sequências de caracteres específicas? Neste caso, usamos a cláusula LIKE:

A cláusula LIKE determina se uma cadeia de caracteres (string) corresponde a um padrão especificado. Um padrão pode incluir caracteres normais e curingas.
NOT LIKE inverte a comparação, verificando se a cadeia de caracteres NÃO corresponde ao padrão especificado.

## Padrões específicos (metacaracteres)

Usamos diversos conjuntos de caracteres para especificar os padrões a serem filtrados pelas cláusulas LIKE e NOT LIKE. Por exemplo:

- '%'  — Qualquer cadeia de 0 ou mais caracteres
- '_'   — Sublinhado: qualquer caracter único

### Exemplos:

**1.** Selecionar todos os registros da tabela tbl_livro cujo nome comece com a letra F:

```sql
SELECT * FROM tbl_Livro
WHERE Nome_Livro LIKE 'F%'; 
```

**2.** Selecionar todos os registros da tabela tbl_livro cujo nome não começa com a letra S:

```sql
SELECT * FROM tbl_Livro
WHERE Nome_Livro NOT LIKE 'S%'; 
```

**3.** Selecionar os nomes de livros da tabela tbl_livro cujo nome se inicie com uma letra qualquer e a segunda letra seja a letra i:

```sql
SELECT Nome_Livro
FROM tbl_Livro
WHERE Nome_Livro LIKE '_i%';
```

**4.** Selecionar os nomes dos livros e seus respectivos preços, na tabela de livros, cujo nome não comece com a letra F e que custem mais de R$ 60,00:

```sql
SELECT Nome_Livro AS Livro, Preco_Livro AS Valor
FROM tbl_livro
WHERE Nome_Livro NOT LIKE 'F%'
AND Preco_Livro > 60.00;
```


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>