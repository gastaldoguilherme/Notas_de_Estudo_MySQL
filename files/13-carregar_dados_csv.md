> **Carregar Dados Arquivo CSV**     
> Repositório: Banco de Dados MySQL - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Carregar Dados a Partir de um Arquivo CSV em uma Tabela

### Carregar Arquivo CSV em uma Tabela no MySQL

Um arquivo .csv (comma-separated values / valores separados por vírgulas) é um arquivo de texto que contém dados tabulares organizados em colunas, separados por um caractere delimitador de campos, que geralmente é uma vírgula (daí seu nome), mas que pode ser outro caractere qualquer, como ponto-e-vírgula, tabulação ou mesmo espaços simples. A grande vantagem de usar arquivos CSV é que eles podem ser criados facilmente em qualquer editor de textos ou exportados a partir de planilhas eletrônicas, como o Microsoft Excel ou LibreOffice Calc, permitindo criar arquivos de dados de grande volume com rapidez e simplicidade.

Neste tutorial, vou mostrar como é possível usar um arquivo CSV para carregar (inserir) dados em uma tabela de banco de dados no MySQL. Para isso, usaremos a declaração LOAD DATA INFILE.

### O Arquivo .CSV

Vamos usar um arquivo CSV simples para carregar dados em uma tabela de autores de livros que contém três campos: ID do autor, Nome do autor e Sobrenome do autor, nesta ordem, usando o banco de dados db_biblioteca que usamos em outras lições.

Crie o arquivo usando um editor de textos ou planilha de sua preferência, mas certifique-se de salvá-lo com a extensão .csv, ou o processo de importação de registros irá falhar.

```

Nome_Autor; Sobrenome_Autor
William;Shakespeare
Charles;Dickens
Jane;Austen
Mark;Twain
Leo;Tolstoy
George;Orwell

```

A primeira linha contém cabeçalhos para identificação do conteúdo de cada coluna (é opcional, o MySQL não se importa com isso).

### Comando LOAD DATA INFILE

Para importar dados do arquivo CSV para a tabela no MySQL, usamos a declaração LOAD DATA INFILE, conforme a seguinte sintaxe:

```sql
LOAD DATA INFILE 'C:\\caminho\\do\\arquivo.csv'
INTO TABLE nome_tabela
FIELDS TERMINATED BY ';'
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```

- LOAD DATA INFILE: Define o local onde está o arquivo CSV que será importado. Basta alterar o caminho para apontar para o arquivo correto. Caso o arquivo esteja na máquina local, podemos usar também a declaração LOAD DATA LOCAL INFILE.

- INTO TABLE: Determina a tabela de destino na qual os dados do arquivo CSV serão importados.

- FIELDS TERMINATED BY: Por padrão, arquivos CSV têm seus dados separados por vírgulas. Se o arquivo usar um delimitador diferente, informe o valor nessa opção.

- ENCLOSED BY: Usado para especificar que aspas duplas englobam valores de dados, quando fazem parte do valor.

- LINES TERMINATED BY: Especifica o caractere usado para indicar quebra de linha.

- IGNORE 1 ROWS: É usado para ignorar a primeira linha do arquivo, que geralmente contém rótulos de colunas.

Observação: a opção LOAD DATA INFILE deve usar a barra `/` em vez de `\`, mesmo no Windows.


## `--secure-file-priv`

O servidor MySQL está configurado com a opção `--secure-file-priv`, o que limita a capacidade de usar a instrução `LOAD DATA INFILE` para carregar dados de um arquivo em uma tabela.

A opção `--secure-file-priv` é uma medida de segurança que restringe onde o MySQL pode ler e gravar arquivos no sistema de arquivos do servidor. Ela é usada para prevenir possíveis vulnerabilidades de segurança.

## Soluções para o Erro

Para resolver esse erro, você tem algumas opções:

1. **Mover o Arquivo para o Diretório Permitido:**
   A maneira mais segura de lidar com isso é mover o arquivo CSV para o diretório permitido pela opção `--secure-file-priv`. O MySQL permite a leitura de arquivos apenas a partir desse diretório.

2. **Desativar Temporariamente a Opção Secure File Privileges (não recomendado em produção):**
   Se você estiver em um ambiente de desenvolvimento ou teste e estiver disposto a abrir mão temporariamente da segurança, poderá desativar temporariamente a opção `--secure-file-priv` e, em seguida, executar sua instrução `LOAD DATA INFILE`. No entanto, isso não é recomendado em ambientes de produção por razões de segurança.

   Para desativar temporariamente a opção, você pode reiniciar o MySQL com o seguinte comando:

   ```
   mysqld --secure-file-priv=""
   ```

   Certifique-se de que compreende os riscos associados à desativação dessa opção.

3. **Usar OUTFILE em vez de LOAD DATA INFILE:**
   Se você estiver tentando exportar dados para um arquivo CSV, em vez de importá-los, você pode usar a instrução `SELECT ... INTO OUTFILE` para criar o arquivo CSV a partir de uma consulta SQL. Isso não será afetado pela configuração `--secure-file-priv`. Exemplo:

   ```sql
   SELECT *
   INTO OUTFILE 'C:\\caminho\\do\\arquivo.csv'
   FIELDS TERMINATED BY ';'
   ENCLOSED BY '"'
   LINES TERMINATED BY '\n'
   FROM tbl_autores;

   ```


   Isso exportará os dados da tabela `tbl_autores` para o arquivo CSV especificado.

Lembre-se de que a primeira opção (mover o arquivo para o diretório permitido) é a mais segura e é recomendada em ambientes de produção. As outras opções devem ser usadas com cautela e apenas em ambientes de desenvolvimento ou teste, uma vez que podem apresentar riscos de segurança.



## Mover um Arquivo CSV para o Diretório Permitido no MySQL

Para mover o arquivo CSV para o diretório permitido pela opção `--secure-file-priv` no MySQL, siga estas etapas:

1. **Descubra o Diretório Permitido:**

   Primeiro, você precisa descobrir o diretório permitido pelo MySQL para leitura e gravação de arquivos. Você pode verificar essa configuração executando o seguinte comando SQL no MySQL:

   ```sql
   SHOW VARIABLES LIKE 'secure_file_priv';
   ```

   Isso retornará o diretório permitido. Anote o caminho exibido, pois você precisará dele.

2. **Mova o Arquivo CSV para o Diretório Permitido:**

   Agora que você conhece o diretório permitido, mova o arquivo CSV para esse diretório usando comandos do sistema operacional. 
   - Navegue até o diretório permitido pelo MySQL (o caminho que você anotou na etapa anterior).
   - Cole o arquivo (Ctrl + V) na pasta do diretório permitido.

3. **Verifique as Permissões do Arquivo:**

   Certifique-se de que o arquivo CSV que você moveu para o diretório permitido tenha permissões de leitura que permitam ao MySQL acessá-lo. Geralmente, o MySQL deve ter permissão de leitura no arquivo.

4. **Execute a Instrução `LOAD DATA INFILE`:**

#### Exemplo

Para carregar os dados presentes no arquivo `autores.csv` na tabela de autores, usaremos a declaração LOAD DATA INFILE como segue:

Agora que o arquivo CSV está no diretório permitido, você pode executar sua instrução `LOAD DATA INFILE` como originalmente planejado:

```sql

   LOAD DATA INFILE 'C:\\caminho\\para\\diretório_permitido\\autores.csv'
   INTO TABLE tbl_autores
   FIELDS TERMINATED BY ';'
   ENCLOSED BY '"'
   LINES TERMINATED BY '\n'
   IGNORE 1 ROWS
   (Nome_Autor, Sobrenome_Autor);
  
   ```

Lembre-se de substituir `'C:\\caminho\\para\\diretório_permitido\\autores.csv'` pelo caminho completo do arquivo CSV no diretório permitido.

Ao seguir essas etapas, você deve ser capaz de carregar o arquivo CSV no MySQL com segurança, aproveitando o diretório permitido pela opção `--secure-file-priv`. Certifique-se de manter a segurança e as permissões adequadas nos arquivos e diretórios envolvidos.

Para verificar se os dados foram carregados na tabela, basta fazer uma consulta simples com SELECT:

```sql
SELECT * FROM tbl_autores;
```

Isso permitirá verificar se os dados foram inseridos com sucesso na tabela de autores do banco de dados.


&nbsp;    

<div align="center">
   
[Retornar ao índice](/README.md)

</div>