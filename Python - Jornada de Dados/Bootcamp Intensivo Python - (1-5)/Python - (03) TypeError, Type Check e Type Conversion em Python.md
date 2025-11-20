Anotações: [[Python - (02) Tipos primitivos|Aula 02]]

# TypeError, Type Check e Type Conversion em Python

Python é uma linguagem de programação dinâmica, mas fortemente tipada, o que significa que não é necessário declarar tipos de variáveis explicitamente, mas o tipo de uma variável é determinado pelo valor que ela armazena. Isso introduz a necessidade de compreender como Python lida com diferentes tipos de dados, especialmente quando se trata de operações que envolvem múltiplos tipos. Vamos explorar três conceitos importantes: `TypeError`, verificação de tipo (`type check`), e conversão de tipo (`type conversion`).

## TypeError

Um `TypeError` ocorre em Python quando uma operação ou função é aplicada a um objeto de tipo inadequado. Python não sabe como aplicar a operação porque os tipos de dados não são compatíveis.

### Exemplo de TypeError

Um exemplo clássico é tentar utilizar a função `len()` com um inteiro, o que resulta em `TypeError`, pois `len()` espera um objeto iterável, como uma string, lista, ou tupla, não um inteiro.

```python
# Exemplo que causa TypeError
try:
    resultado = len(5)
except TypeError as e:
    print(e)  # Imprime a mensagem de erro
```

O código acima tenta obter o comprimento de um inteiro, o que não faz sentido, resultando na mensagem de erro: "object of type 'int' has no len()".

## Type Check

Verificação de tipo (`type check`) é o processo de verificar o tipo de uma variável. Isso pode ser útil para garantir que operações ou funções sejam aplicadas apenas a tipos de dados compatíveis, evitando erros em tempo de execução.

### Exemplo de Type Check

Para verificar o tipo de uma variável em Python, você pode usar a função `type()` ou `isinstance()`.

```python
numero = 10
if isinstance(numero, int):
    print("A variável é um inteiro.")
else:
    print("A variável não é um inteiro.")
```

Este código verifica se `numero` é uma instância de `int` e imprime uma mensagem apropriada.

## Type Conversion

Conversão de tipo (`type conversion`), também conhecida como casting, é o processo de converter o valor de uma variável de um tipo para outro. Python oferece várias funções integradas para realizar conversões explícitas de tipo, como `int()`, `float()`, `str()`, etc.

### Exemplo de Type Conversion

Se você quiser somar um inteiro e um número flutuante, pode ser necessário converter o inteiro para flutuante ou vice-versa para garantir que a operação de soma seja realizada corretamente.

```python
numero_inteiro = 5
numero_flutuante = 2.5
# Converte o inteiro para flutuante e realiza a soma
soma = float(numero_inteiro) + numero_flutuante
print(soma)  # Resultado: 7.5
```

### try-except

A estrutura `try-except` é usada para tratamento de exceções em Python. Uma exceção é um erro que ocorre durante a execução do programa e que, se não tratado, interrompe o fluxo normal do programa e termina sua execução. O tratamento de exceções permite que o programa lide com erros de maneira elegante, permitindo que continue a execução ou falhe de forma controlada.

* **try:** Este bloco é o primeiro na estrutura de tratamento de exceções. Python tenta executar o código dentro deste bloco.
* **except:** Se uma exceção ocorrer no bloco `try`, a execução imediatamente salta para o bloco `except`. Você pode especificar tipos de exceção específicos para capturar e tratar apenas essas exceções. Se nenhum tipo de exceção for especificado, ele captura todas as exceções.

#### Exemplo de try-except

```python
try:
    # Código que pode gerar uma exceção
    resultado = 10 / 0
except ZeroDivisionError:
    # Código que executa se a exceção ZeroDivisionError for levantada
    print("Divisão por zero não é permitida.")
```

### if

O `if` é uma estrutura de controle de fluxo que permite ao programa executar diferentes ações com base em diferentes condições. Se a condição avaliada pelo `if` for verdadeira (`True`), o bloco de código indentado sob ele será executado. Se a condição for falsa (`False`), o bloco de código será ignorado.

* **if:** Avalia uma condição. Se a condição for verdadeira, executa o bloco de código associado.
* **elif:** Abreviação de "else if". Permite verificar múltiplas condições em sequência.
* **else:** Executa um bloco de código se todas as condições anteriores no `if` e `elif` forem falsas.

#### Exemplo de if

```python
idade = 20
if idade < 18:
    print("Menor de idade")
elif idade == 18:
    print("Exatamente 18 anos")
else:
    print("Maior de idade")
```

Ambas as estruturas, `try-except` e `if`, são fundamentais para a criação de programas em Python que são capazes de lidar com situações inesperadas (como erros de execução) e tomar decisões com base em condições, permitindo assim que você construa programas mais robustos, flexíveis e seguros.

## Exercícios

Aqui estão cinco exercícios que envolvem `TypeError`, verificação de tipo (`type check`), o uso de `try-except` para tratamento de exceções e a utilização da estrutura condicional `if`. Esses exercícios aumentam progressivamente em dificuldade e abordam situações práticas onde você pode aplicar esses conceitos.

### Exercício 21: Conversor de Temperatura

Escreva um programa que converta a temperatura de Celsius para Fahrenheit. O programa deve solicitar ao usuário a temperatura em Celsius e, utilizando `try-except`, garantir que a entrada seja numérica, tratando qualquer `ValueError`. Imprima o resultado em Fahrenheit ou uma mensagem de erro se a entrada não for válida.

### Exercício 22: Verificador de Palíndromo

Crie um programa que verifica se uma palavra ou frase é um palíndromo (lê-se igualmente de trás para frente, desconsiderando espaços e pontuações). Utilize `try-except` para garantir que a entrada seja uma string. Dica: Utilize a função `isinstance()` para verificar o tipo da entrada.

### Exercício 23: Calculadora Simples

Desenvolva uma calculadora simples que aceite duas entradas numéricas e um operador (+, -, *, /) do usuário. Use `try-except` para lidar com divisões por zero e entradas não numéricas. Utilize `if-elif-else` para realizar a operação matemática baseada no operador fornecido. Imprima o resultado ou uma mensagem de erro apropriada.

### Exercício 24: Classificador de Números

Escreva um programa que solicite ao usuário para digitar um número. Utilize `try-except` para assegurar que a entrada seja numérica e utilize `if-elif-else` para classificar o número como "positivo", "negativo" ou "zero". Adicionalmente, identifique se o número é "par" ou "ímpar".

### Exercício 25: Conversão de Tipo com Validação

Crie um script que solicite ao usuário uma lista de números separados por vírgula. O programa deve converter a string de entrada em uma lista de números inteiros. Utilize `try-except` para tratar a conversão de cada número e validar que cada elemento da lista convertida é um inteiro. Se a conversão falhar ou um elemento não for um inteiro, imprima uma mensagem de erro. Se a conversão for bem-sucedida para todos os elementos, imprima a lista de inteiros.

## Exercícios Resolvidos

### Exercício 21: Conversor de Temperatura

```python
try:
    celsius = float(input("Digite a temperatura em Celsius: "))
    fahrenheit = (celsius * 9/5) + 32
    print(f"{celsius}°C é igual a {fahrenheit}°F.")
except ValueError:
    print("Por favor, digite um número válido para a temperatura.")
```

### Exercício 22: Verificador de Palíndromo

```python
entrada = input("Digite uma palavra ou frase: ")
if isinstance(entrada, str):
    formatado = entrada.replace(" ", "").lower()
    if formatado == formatado[::-1]:
        print("É um palíndromo.")
    else:
        print("Não é um palíndromo.")
else:
    print("Entrada inválida. Por favor, digite uma palavra ou frase.")
```

### Exercício 23: Calculadora Simples

```python
try:
    num1 = float(input("Digite o primeiro número: "))
    num2 = float(input("Digite o segundo número: "))
    operador = input("Digite o operador (+, -, *, /): ")
    if operador == '+':
        resultado = num1 + num2
    elif operador == '-':
        resultado = num1 - num2
    elif operador == '*':
        resultado = num1 * num2
    elif operador == '/' and num2 != 0:
        resultado = num1 / num2
    else:
        print("Operador inválido ou divisão por zero.")
    print("Resultado:", resultado)
except ValueError:
    print("Erro: Entrada inválida. Certifique-se de inserir números.")
```

### Exercício 24: Classificador de Números

```python
try:
    numero = int(input("Digite um número: "))
    if numero > 0:
        print("Positivo")
    elif numero < 0:
        print("Negativo")
    else:
        print("Zero")
    if numero % 2 == 0:
        print("Par")
    else:
        print("Ímpar")
except ValueError:
    print("Por favor, digite um número inteiro válido.")
```

### Exercício 25: Conversão de Tipo com Validação

```python
entrada_lista = input("Digite uma lista de números separados por vírgula: ")
numeros_str = entrada_lista.split(",")
numeros_int = []
try:
    for num in numeros_str:
        numeros_int.append(int(num.strip()))
    print("Lista de inteiros:", numeros_int)
except ValueError:
    print("Erro: certifique-se de que todos os elementos são números inteiros válidos.")
```

![imagem_03](3.png)

### Desafio - Refatorar o projeto da aula anterior evitando Bugs!

Para resolver os bugs identificados — tratamento de entradas inválidas que não podem ser convertidas para um número de ponto flutuante e prevenção de valores negativos para salário e bônus, você pode modificar o código diretamente. Isso envolve adicionar verificações adicionais após a tentativa de conversão para garantir que os valores sejam positivos.

![imagem_05](5.png)

```python
# Solicita ao usuário que digite seu nome
try:
    nome = input("Digite seu nome: ")

    # Verifica se o nome está vazio
    if len(nome) == 0:
        raise ValueError("O nome não pode estar vazio.")
    # Verifica se há números no nome
    elif any(char.isdigit() for char in nome):
        raise ValueError("O nome não deve conter números.")
    else:
        print("Nome válido:", nome)
except ValueError as e:
    print(e)

# Solicita ao usuário que digite o valor do seu salário e converte para float

try:
    salario = float(input("Digite o valor do seu salário: "))
    if salario < 0:
        print("Por favor, digite um valor positivo para o salário.")
except ValueError:
    print("Entrada inválida para o salário. Por favor, digite um número.")

# Solicita ao usuário que digite o valor do bônus recebido e converte para float
try:
    bonus_recebido = float(input("Digite o valor do bônus recebido: "))
    if bonus_recebido < 0:
        print("Por favor, digite um valor positivo para o bônus.")
except ValueError:
    print("Entrada inválida para o bônus. Por favor, digite um número.")

# Assumindo uma lógica de cálculo para o bônus final e KPI
bonus_final = bonus_recebido * 1.2  # Exemplo, ajuste conforme necessário
kpi = (salario + bonus_final) / 1000  # Exemplo simples de KPI

# Imprime as informações para o usuário
print(f"Seu KPI é: {kpi:.2f}")
print(f"{nome}, seu salário é R${salario:.2f} e seu bônus final é R${bonus_final:.2f}.")
```

