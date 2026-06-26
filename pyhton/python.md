### 1. 🐍 Python

Python é uma linguagem de programação de alto nível, interpretada, multiplataforma e de propósito geral. Sua principal característica é a sintaxe simples e legível, tornando-a uma das linguagens mais utilizadas para automação, desenvolvimento web, ciência de dados, inteligência artificial, análise de dados e muito mais.

#### 🎯 O que você pode fazer com Python?

- 📊 Ciência e análise de dados
- 🤖 Inteligência Artificial e Machine Learning
- 🌐 Desenvolvimento Web
- ⚙️ Automação de tarefas
- 📈 Engenharia de Dados
- 🎮 Desenvolvimento de jogos
- 📱 Aplicações desktop
- 🔒 Segurança da Informação
- 📂 Manipulação de arquivos


#### ✅ Vantagens

- Sintaxe simples
- Fácil de aprender
- Grande comunidade
- Milhares de bibliotecas
- Multiplataforma
- Código muito legível

#### 📥 Instalação

Baixe em:

https://python.org

Durante a instalação marque:

> ✔ Add Python to PATH

Verifique:

```bash
python --version
```

ou

```bash
python3 --version
```

---

#### 🖥️ Executando Python

Modo interativo:

```bash
python
```

Arquivo:

```bash
python programa.py
```

---

### 2. 📦 Variáveis

Python não exige declarar o tipo.

```python
nome = "Josicleyton" # string
idade = 28           # númeiro inteiro
altura = 1.80        # float
aprovado = True      # booleano
```

#### 🔠 Tipos básicos

| Tipo | Exemplo |
|-------|----------|
| int | 10 |
| float | 3.14 |
| str | "Python" |
| bool | True |
| list | [1,2,3] |
| tuple | (1,2,3) |
| dict | {"a":1} |
| set | {1,2,3} |
| NoneType | None |


#### 📌 Conversão de tipos

```python
int("10")

float("3.14")

str(100)

bool(1)
```

---

### 3. 📖 Entrada de dados

```python
nome = input("Nome: ")
```

Como `input()` sempre retorna texto:

```python
idade = int(input("Idade: "))
altura = float(input("Altura: "))
```

---

### 4. 📤 Saída

```python
print("Olá")

print(nome)

print(nome, idade)
```

Interpolação:

```python
print(f"Meu nome é {nome}")
```

---

### 5. ➕ Operadores

#### Aritméticos

| Operador | Nome | Exemplo | Resultado |
|----------|------|----------|-----------|
| `+` | Adição | `5 + 3` | `8` |
| `-` | Subtração | `5 - 3` | `2` |
| `*` | Multiplicação | `5 * 3` | `15` |
| `/` | Divisão | `10 / 3` | `3.333...` |
| `//` | Divisão inteira | `10 // 3` | `3` |
| `%` | Módulo (resto da divisão) | `10 % 3` | `1` |
| `**` | Exponenciação | `2 ** 3` | `8` |

#### Comparação

| Operador | Nome | Exemplo | Resultado |
|----------|------|----------|-----------|
| `==` | Igual a | `5 == 5` | `True` |
| `!=` | Diferente de | `5 != 3` | `True` |
| `>` | Maior que | `10 > 8` | `True` |
| `<` | Menor que | `3 < 7` | `True` |
| `>=` | Maior ou igual | `5 >= 5` | `True` |
| `<=` | Menor ou igual | `4 <= 2` | `False` |

#### Lógicos

| Operador | Significado |
|----------|-------------|
| `and` | Verdadeiro se todas as condições forem verdadeiras |
| `or` | Verdadeiro se pelo menos uma condição for verdadeira |
| `not` | Inverte o valor lógico |

#### Atribuição

Os operadores de atribuição armazenam ou atualizam o valor de uma variável.

| Operador | Equivalente | Exemplo |
|----------|-------------|----------|
| `=` | Atribuição | `x = 10` |
| `+=` | `x = x + valor` | `x += 5` |
| `-=` | `x = x - valor` | `x -= 5` |
| `*=` | `x = x * valor` | `x *= 2` |
| `/=` | `x = x / valor` | `x /= 2` |
| `//=` | `x = x // valor` | `x //= 2` |
| `%=` | `x = x % valor` | `x %= 2` |
| `**=` | `x = x ** valor` | `x **= 2` |

---

### 6. 🔀 Condicionais

```python
idade = 18

if idade >= 18:
    print("Maior")

else:
    print("Menor")
```

#### elif

```python
nota = 8

if nota >= 9:
    print("Excelente")

elif nota >= 7:
    print("Aprovado")

else:
    print("Reprovado")
```

---

### 7. 🔁 Laços

Os **laços de repetição** permitem executar um bloco de código várias vezes.

---

#### `for`

Usado para percorrer uma sequência (lista, string, `range`, etc.).

```python
for i in range(5):
    print(i)
```

Resultado

```
0
1
2
3
4
```

Outro exemplo:

```python
nomes = ["Ana", "Carlos", "Maria"]

for nome in nomes:
    print(nome)
```

---

#### `while`

Executa o bloco enquanto uma condição for verdadeira.

```python
contador = 0

while contador < 5:
    print(contador)
    contador += 1
```

> **Atenção:** sempre altere a condição dentro do `while`, caso contrário ele poderá entrar em um **loop infinito**.

---

#### `break`

Interrompe o laço imediatamente.

```python
for i in range(10):
    if i == 5:
        break

    print(i)
```

Resultado

```
0
1
2
3
4
```

---

#### `continue`

Pula a iteração atual e continua para a próxima.

```python
for i in range(5):

    if i == 2:
        continue

    print(i)
```

Resultado

```
0
1
3
4
```

---

### 8. 📚 Strings

```python
texto = "Python"
```

Acessando caracteres

```python
texto[0]
```

Último

```python
texto[-1]
```

Fatiamento

```python
texto[1:4]
```

---

## Métodos úteis

```python
texto.upper()         # Converte todas as letras para maiúsculas.

texto.lower()         # Converte todas as letras para minúsculas.

texto.capitalize()    # Deixa apenas a primeira letra maiúscula.

texto.strip()         # Remove espaços do início e do fim da string.

texto.replace()       # Substitui uma parte do texto por outra.

texto.split()         # Divide a string em uma lista.

len(texto)            # Retorna a quantidade de caracteres da string.
```

---

### 10. 📋 Listas

```python
numeros = [10,20,30]
```

Adicionar

```python
numeros.append(40)
```

Remover

```python
numeros.remove(20)
```

Ordenar

```python
numeros.sort()
```

Tamanho

```python
len(numeros)
```

Percorrer

```python
for numero in numeros:
    print(numero)
```

---

### 11. 🔒 Tuplas

Imutáveis.

```python
cores = ("Azul", "Verde", "Vermelho")
```

---

### 12. 🎲 Sets

Não possuem elementos repetidos.

```python
numeros = {1,2,3,3,3}

print(numeros)
```

Resultado

```
{1,2,3}
```

---

### 13. 📖 Dicionários

Estrutura chave-valor.

```python
pessoa = {
    "nome": "Maria",
    "idade": 20
}
```

Acessando

```python
pessoa["nome"]
```

Adicionando

```python
pessoa["cidade"] = "Natal"
```

Percorrendo

```python
for chave, valor in pessoa.items():
    print(chave, valor)
```

---

### 14. ⚙️ Funções

```python
def saudacao(nome):
    print(f"Olá {nome}")
```

Chamando

```python
saudacao("João")
```
#### Retorno

```python
def soma(a, b):
    return a + b
```

#### Valor padrão

```python
def saudacao(nome="Visitante"):
    print(nome)
```

---

### 15. 📦 Importando módulos

```python
import math
```

```python
math.sqrt(25)
```

Importando apenas uma função

```python
from math import sqrt

sqrt(25)
```

---

### 16. 📂 Manipulação de arquivos

Escrevendo

```python
with open("arquivo.txt", "w") as arquivo:
    arquivo.write("Olá")
```

Lendo

```python
with open("arquivo.txt", "r") as arquivo:
    texto = arquivo.read()
```

---

### 17. 🏛️ Classes

```python
class Pessoa:

    def __init__(self, nome):
        self.nome = nome

    def apresentar(self):
        print(self.nome)
```

Criando objeto

```python
p = Pessoa("Carlos")

p.apresentar()
```

---

# 📚 List Comprehension

Forma compacta de criar listas.

```python
quadrados = [x**2 for x in range(10)]
```

---

# 🎯 Expressão condicional

```python
idade = 20

resultado = "Maior" if idade >= 18 else "Menor"
```

---

# 🔍 Enumerate

```python
nomes = ["Ana", "João"]

for indice, nome in enumerate(nomes):
    print(indice, nome)
```

---

# 🔄 Zip

```python
nomes = ["Ana", "João"]

idades = [20, 25]

for nome, idade in zip(nomes, idades):
    print(nome, idade)
```


---

### 🗂️ Principais Bibliotecas

| Biblioteca | Uso |
|------------|-----|
| NumPy | Computação numérica |
| Pandas | Manipulação de dados |
| Matplotlib | Gráficos |
| Scikit-Learn | Machine Learning |
| TensorFlow | IA |
| PyTorch | Deep Learning |
| OpenCV | Visão Computacional |
| Flask | Desenvolvimento Web |
| FastAPI | APIs |
| Django | Desenvolvimento Web |
| Requests | Requisições HTTP |
| Selenium | Automação |

### 💡 Boas práticas

- Utilize nomes descritivos.
- Escreva funções pequenas.
- Evite repetição de código.
- Utilize comentários apenas quando necessário.
- Prefira `with open()` para arquivos.
- Siga o padrão PEP 8.
- Utilize ambientes virtuais (`venv`).

---

### 👨‍💻 Author

**Josicleyton Santos**

🎓 Engenheiro de Produção e Mestre em Ciência da Computação <br>
📊 Análise de Dados | 💻 Programação | ⚙️ Otimização

📧 [santos.josicleyton@gmail.com](mailto:santos.josicleyton@gmail.com) <br>
💼 LinkedIn: linkedin.com/in/josicleyton-santos-0bb43b218