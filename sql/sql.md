### 1. O que é SQL?

**SQL (Structured Query Language)** é a linguagem padrão utilizada para criar, manipular e consultar dados em bancos de dados relacionais.

Com SQL, é possível realizar operações essenciais como:

* Criar estruturas de armazenamento (tabelas, índices e relacionamentos);
* Inserir dados;
* Consultar informações;
* Atualizar registros;
* Excluir dados.

Neste material utilizaremos o **MySQL**, mas os conceitos apresentados são amplamente aplicáveis a outros sistemas de gerenciamento de bancos de dados relacionais, como:

* MySQL
* PostgreSQL
* SQL Server
* Oracle Database
* SQLite

Os comandos SQL são tradicionalmente agrupados em categorias (claúsulas) de acordo com sua finalidade. Essa divisão facilita o entendimento do papel de cada comando dentro do banco de dados.

Podemos imaginar um banco de dados como uma grande planilha, onde cada grupo de comandos possui uma responsabilidade específica:

| Categoria                                | Descrição                                                                       |
| ---------------------------------------- | ------------------------------------------------------------------------------- |
| **DDL** (*Data Definition Language*)     | Define e altera a estrutura do banco de dados, como tabelas, colunas e índices. |
| **DML** (*Data Manipulation Language*)   | Manipula os dados armazenados nas tabelas.                                      |
| **DQL** (*Data Query Language*)          | Realiza consultas e recuperação de informações (segurança).                     |
| **TCL** (*Transaction Control Language*) | Controla transações, garantindo a consistência dos dados (forma atômica).       |
| **DCL** (*Data Control Language*)        | Gerencia permissões e níveis de acesso dos usuários.                            |

Nos próximos tópicos, estudaremos principalmente os comandos das categorias **DDL**, **DML** e **DQL**, que formam a base do desenvolvimento e da manipulação de bancos de dados relacionais.


---

### 2. ## Conceitos Básicos de Banco de Dados Relacional

Um **banco de dados relacional** organiza as informações em **tabelas**, compostas por **linhas** (registros) e **colunas** (campos).

Por exemplo, uma tabela de clientes pode armazenar:

| id | nome  | cidade |
| -- | ----- | ------ |
| 1  | João  | Natal  |
| 2  | Maria | Recife |

A principal característica dos bancos relacionais é a possibilidade de **relacionar tabelas entre si**, evitando a duplicação de informações e facilitando a manutenção dos dados.

#### Chave Primária (Primary Key)

A **chave primária (Primary Key ou PK)** é um campo que identifica cada registro de forma única dentro de uma tabela.

Características:

* Não pode ter valores repetidos;
* Não pode ser nula;
* Identifica exclusivamente cada registro.

Exemplo:

| id | nome    |
| -- | ------- |
| 1  | Apple   |
| 2  | Dell    |
| 3  | Samsung |

Nesse caso, a coluna `id` é a chave primária.

#### Chave Estrangeira (Foreign Key)

A **chave estrangeira (Foreign Key ou FK)** é utilizada para criar relacionamentos entre tabelas.

Ela armazena o valor da chave primária de outra tabela.

| id | nome  |
| -- | ----- |
| 1  | Apple |
| 2  | Dell  |

| id | nome        | id_marca |
| -- | ----------- | -------- |
| 1  | iPhone 16   | 1        |
| 2  | Inspiron 16 | 2        |

Nesse exemplo, `id_marca` é uma chave estrangeira que referencia a coluna `id` da tabela primeira tabela.

Assim, cada produto fica associado à sua respectiva marca.

#### Índices (Indexes)

Os **índices** são estruturas criadas para acelerar consultas em uma ou mais colunas.

Funcionam de forma semelhante ao índice de um livro: em vez de procurar página por página, o banco encontra a informação mais rapidamente.

Exemplo:

```sql
CREATE INDEX idx_produtos_nome
ON produtos(nome);
```

Esse índice melhora o desempenho de pesquisas realizadas pela coluna `nome`.

> Índices aumentam a velocidade das consultas, mas também podem tornar inserções e atualizações um pouco mais lentas. Por isso, devem ser criados apenas em colunas frequentemente utilizadas em pesquisas, filtros e relacionamentos.

---

### 3. Criando tabelas (DDL)

DDL significa **Data Definition Language**.

São comandos usados para definir a estrutura do banco.

Principais comandos:

| Comando  | Função   |
| -------- | -------- |
| CREATE   | Criar    |
| ALTER    | Alterar  |
| DROP     | Excluir  |
| TRUNCATE | Esvaziar |

---

### CREATE TABLE

Primeiro foi criada a tabela de marcas:

```sql
CREATE TABLE marcas (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL UNIQUE,
    site VARCHAR(100),
    telefone VARCHAR(15)
);
```

* **`id INTEGER PRIMARY KEY AUTO_INCREMENT`**: Cria a coluna **id**, que armazenará um número inteiro (**INTEGER**) usado para identificar cada registro de forma única (**PRIMARY KEY**). O valor é gerado automaticamente pelo banco (**AUTO_INCREMENT**).

* **`nome VARCHAR(100) NOT NULL UNIQUE`**: Cria a coluna **nome**, que armazenará textos de até 100 caracteres (**VARCHAR(100)**). O preenchimento é obrigatório (**NOT NULL**) e não permite valores repetidos (**UNIQUE**).

* **`site VARCHAR(100)`**: Cria a coluna **site**, que armazenará o endereço do site da marca em formato de texto, com até 100 caracteres (**VARCHAR(100)**). Como não possui restrições adicionais, o preenchimento é opcional.

* **`telefone VARCHAR(15)`**: Cria a coluna **telefone**, que armazenará o número de telefone em formato de texto, com até 15 caracteres (**VARCHAR(15)**). O preenchimento também é opcional.


Depois foi criada a tabela de produtos:

```sql
CREATE TABLE produtos (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    preco REAL,
    estoque INTEGER DEFAULT 0
);
```

* **`preco REAL`**: Cria a coluna **preco**, que armazenará valores numéricos com casas decimais (**REAL**), como preços de produtos.

* **`estoque INTEGER DEFAULT 0`**: Cria a coluna **estoque**, que armazenará a quantidade disponível do produto em números inteiros (**INTEGER**). Caso nenhum valor seja informado, o banco atribuirá automaticamente o valor **0** (**DEFAULT 0**).


---

## 3. Alterando tabelas

Usando `ALTER TABLE`.

### Adicionando coluna

```sql
ALTER TABLE produtos
ADD COLUMN id_marca INT NOT NULL;
```

* Antes: |id|nome|preco|estoque|

* Depois: |id|nome|preco|estoque|id_marca|

### Modificando coluna

```sql
ALTER TABLE produtos
MODIFY COLUMN nome VARCHAR(150);
```

Aumentou o tamanho do nome.


### Criando chave estrangeira

```sql
ALTER TABLE produtos
ADD FOREIGN KEY (id_marca)
REFERENCES marcas(id);
```

Significa:

> O valor de `id_marca` deve existir na tabela `marcas`.

Exemplo:

Se existe:

```text
marcas
1 Apple
2 Dell
```

Então:

```text
produtos
id_marca = 1
```

é válido.

Mas:

```text
id_marca = 99
```

gera erro.

---

# Módulo 4 — Índices

Índices aceleram buscas.

Criando:

```sql
CREATE INDEX idx_produtos_nome
ON produtos (nome);
```

Agora pesquisas pelo nome ficam mais rápidas.

---

# Módulo 5 — Inserindo dados (INSERT)

DML = Data Manipulation Language.

---

## Inserindo marcas

```sql
INSERT INTO marcas
(nome, site, telefone)
VALUES
('Apple', 'apple.com', '0800-761-0867'),
('Dell', 'dell.com.br', '0800-970-3355');
```

Resultado:

| id | nome  |
| -- | ----- |
| 1  | Apple |
| 2  | Dell  |

---

## Inserindo produtos

```sql
INSERT INTO produtos
(nome, preco, estoque, id_marca)
VALUES
('iPhone 15', 4599.00, 50, 1);
```

---

# Módulo 6 — Consultando dados (SELECT)

O comando mais usado.

---

## Mostrar tudo

```sql
SELECT * FROM produtos;
```

`*` significa:

> todas as colunas.

---

## Mostrar colunas específicas

```sql
SELECT id, nome
FROM marcas;
```

---

## Filtros (WHERE)

```sql
SELECT *
FROM produtos
WHERE estoque < 100;
```

---

## Operadores

Maior:

```sql
WHERE estoque > 10
```

Menor:

```sql
WHERE estoque < 10
```

Igual:

```sql
WHERE id = 1
```

Diferente:

```sql
WHERE estoque <> 100
```

---

# Módulo 7 — LIKE

Busca por texto.

Começa com:

```sql
WHERE nome LIKE 'iPhone%'
```

Contém:

```sql
WHERE nome LIKE '%Apple%'
```

Termina com:

```sql
WHERE nome LIKE '%Preto'
```

---

# Módulo 8 — ORDER BY e LIMIT

Ordenar resultados.

Maior preço:

```sql
SELECT *
FROM produtos
ORDER BY preco DESC;
```

Menor preço:

```sql
ORDER BY preco ASC;
```

---

Limitar quantidade:

```sql
LIMIT 5
```

Top 5 produtos:

```sql
SELECT *
FROM produtos
ORDER BY preco DESC
LIMIT 5;
```

---

# Módulo 9 — UPDATE

Atualizar registros.

Exemplo:

```sql
UPDATE produtos
SET nome = 'Microfone SM7B Preto'
WHERE id = 7;
```

Muito importante:

⚠️ Nunca esqueça do `WHERE`.

Sem ele:

```sql
UPDATE produtos
SET estoque = 0;
```

zera o estoque de TODOS os produtos.

---

# Módulo 10 — DELETE

Excluir registros.

```sql
DELETE FROM produtos
WHERE id = 1;
```

Também exige cuidado.

Sem `WHERE`, apaga tudo.

---

# Módulo 11 — TRUNCATE

Esvazia a tabela inteira.

```sql
TRUNCATE TABLE produtos_apple;
```

Remove todos os registros rapidamente.

A estrutura permanece.

---

# Módulo 12 — JOIN

Relacionar tabelas.

Esse é o coração do SQL.

---

## INNER JOIN

Somente registros que possuem correspondência.

```sql
SELECT clientes.nome,
       pedidos.valor_total
FROM clientes
INNER JOIN pedidos
ON clientes.id = pedidos.id_cliente;
```

---

## LEFT JOIN

Todos os clientes.

Mesmo sem pedido.

```sql
SELECT clientes.nome,
       pedidos.valor_total
FROM clientes
LEFT JOIN pedidos
ON clientes.id = pedidos.id_cliente;
```

---

## RIGHT JOIN

Todos os pedidos.

Mesmo sem cliente correspondente.

```sql
SELECT clientes.nome,
       pedidos.valor_total
FROM clientes
RIGHT JOIN pedidos
ON clientes.id = pedidos.id_cliente;
```

---

# Módulo 13 — Subqueries

Consultas dentro de consultas.

Exemplo:

Produtos Apple ou Dell:

```sql
SELECT nome, preco
FROM produtos
WHERE id_marca IN (
    SELECT id
    FROM marcas
    WHERE nome = 'Apple'
       OR nome = 'Dell'
);
```

---

# Módulo 14 — Funções agregadas

Usadas para relatórios.

---

## COUNT

Quantidade.

```sql
SELECT COUNT(*)
FROM clientes;
```

---

## SUM

Soma.

```sql
SELECT SUM(valor_total)
FROM pedidos;
```

---

## AVG

Média.

```sql
SELECT AVG(valor_total)
FROM pedidos;
```

---

## MAX

Maior valor.

```sql
SELECT MAX(valor_total)
FROM pedidos;
```

---

## MIN

Menor valor.

```sql
SELECT MIN(valor_total)
FROM pedidos;
```

---

# Módulo 15 — GROUP BY

Agrupar resultados.

Clientes por cidade:

```sql
SELECT cidade,
       COUNT(*) AS numero_clientes
FROM clientes
GROUP BY cidade;
```

Resultado:

| cidade              | numero_clientes |
| ------------------- | --------------- |
| São Paulo           | 1               |
| São José dos Campos | 2               |

---

# Módulo 16 — HAVING

Filtrar agrupamentos.

Exemplo:

```sql
SELECT c.cidade,
       SUM(p.valor_total) AS total_vendas
FROM clientes c
INNER JOIN pedidos p
    ON c.id = p.id_cliente
GROUP BY c.cidade
HAVING total_vendas < 7000;
```

`WHERE` filtra linhas.

`HAVING` filtra grupos.

---

### 👨‍💻 Author

**Josicleyton Santos**

🎓 Engenheiro de Produção e Mestre em Ciência da Computação <br>
📊 Análise de Dados | 💻 Programação | ⚙️ Otimização

📧 [santos.josicleyton@gmail.com](mailto:santos.josicleyton@gmail.com) <br>
💼 LinkedIn: linkedin.com/in/josicleyton-santos-0bb43b218