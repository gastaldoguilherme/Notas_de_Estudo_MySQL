> **Expressões Regulares (REGEXP)**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Expressões Regulares (REGEXP) no MySQL

Na aula anterior, vimos como realizar filtros específicos em uma consulta acrescentando a cláusula LIKE. O MySQL suporta também um tipo de operação de busca de padrões baseada em expressões regulares com o operador REGEXP.

Alguns exemplos de caracteres para expressões regulares estão listados abaixo:

- `[...]` - Qualquer caracter único no intervalo ou conjunto especificado ([a-h]; [aeiou])
- `[^…]` - Qualquer caracter único que não esteja no intervalo ou conjunto especificado ([^a-h]; [^aeiou])
- `^` - Início da string (fora dos colchetes); Negação (dentro dos colchetes)
- `$` - Fim da string
- `a|b|c` - Alternação (a ou b ou c) (caractere pipe – |)
- `*` - Zero ou mais ocorrências do elemento precedente
- `+` - Uma ou mais ocorrências do elemento precedente
- `{n}` - N instâncias do elemento precedente
- `{m,n}` - De M até N instâncias do elemento precedente

### Exemplos de consultas usando Expressões Regulares no MySQL:

**1.** Retornar os nomes dos livros da tabela tbl_livro, onde o nome do livro se inicie com uma das letras F ou S:

```sql
SELECT Nome_Livro
FROM tbl_Livro
WHERE Nome_Livro REGEXP '^[FS]';
```

**2.** Trazer os livros cujos nomes não se iniciam nem com o caractere F, nem com o caractere S:

```sql
SELECT Nome_Livro
FROM tbl_Livro
WHERE Nome_Livro REGEXP '^[^FS]';
```

**3.** Retornar nomes de livros que finalizem com as letras n ou g:

```sql
SELECT Nome_Livro
FROM tbl_Livro
WHERE Nome_Livro REGEXP '[ng]$';
```

**4.** Consultar os livros cujos nomes comecem com as letras F ou S, ou ainda com a sequência de caracteres Mi:

```sql
SELECT Nome_Livro
FROM tbl_Livro
WHERE Nome_Livro REGEXP '^[FS]|Mi';
```



&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>