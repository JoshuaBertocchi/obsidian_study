[[Python - (01) Python, Git e VScode (Python do Zero)]]
Bem-vindo à segunda aula do bootcamp! 

![imagem_01](1.png)

Hoje, vamos explorar mais a fundo um dos conceitos mais fundamentais da programação: variáveis. As variáveis são essenciais para armazenar e manipular dados em qualquer linguagem de programação, e em Python não é diferente. Nesta aula, vamos entender o que são variáveis, como declará-las, os tipos de dados simples suportados por Python e algumas boas práticas para nomeá-las.

Além disso, vamos mostrar como lidar e trabalhar com erros usando TypeError, Type Check, Type Conversion, try-except e if

## 1. Tipos primitivos

Variáveis são espaços de memória designados para armazenar dados que podem ser modificados durante a execução de um programa. Em Python, a declaração de variáveis é dinâmica, o que significa que o tipo de dado é inferido durante a atribuição.

**Exemplo em Python:**

Python suporta vários tipos de dados simples, tais como:

- **Inteiros (`int`)**: Representam números inteiros.
- **Ponto Flutuante (`float`)**: Representam números reais.
- **Strings (`str`)**: Representam sequências de caracteres.
- **Booleanos (`bool`)**: Representam valores verdadeiros (`True`) ou falsos (`False`).

![imagem_02](2.png)

#### 1. Inteiros (`int`)

* **Métodos e operações:**
    1. `+` (adição)
    2. `-` (subtração)
    3. `*` (multiplicação)
    4. `//` (divisão inteira)
    5. `%` (módulo - resto da divisão)

#### 2. Números de Ponto Flutuante (`float`)

* **Métodos e operações:**
    1. `+` (adição)
    2. `-` (subtração)
    3. `*` (multiplicação)
    4. `/` (divisão)
    5. `**` (potenciação)

#### 3. Strings (`str`)

* **Métodos e operações:**
    1. `.upper()` (converte para maiúsculas)
    2. `.lower()` (converte para minúsculas)
    3. `.strip()` (remove espaços em branco no início e no final)
    4. `.split(sep)` (divide a string em uma lista, utilizando `sep` como delimitador)
    5. `+` (concatenação de strings)

#### 4. Booleanos (`bool`)

* **Operações lógicas:**
    1. `and` (E lógico)
    2. `or` (OU lógico)
    3. `not` (NÃO lógico)
    4. `==` (igualdade)
    5. `!=` (diferença)

### Exercícios

#### Inteiros (`int`)

1. Escreva um programa que soma dois números inteiros inseridos pelo usuário.
```python
valor_01 = int(input("Valor 01: "))
valor_02 = int(input("Valor 02: "))
usuario_soma = valor_01 + valor_02

print(f"A soma é {usuario_soma}")
```
2. Crie um programa que receba um número do usuário e calcule o resto da divisão desse número por 5.
```python
print(" Vamos calcular o resto da divisão! ")
valor_01 = int(input("Valor 01: "))
valor_02 = int(input("Valor 02: "))

divisao = valor_01 / valor_02
resto_divisao = valor_01 % valor_02

if resto_divisao > 0:
    print(f"O resultado da divisão é: {divisao} e o resto {resto_divisao}")
  else:
    print(f"O resultado da divisão é: {divisao}")

```
3. Desenvolva um programa que multiplique dois números fornecidos pelo usuário e mostre o resultado.
```python
print(" Vamos calcular o resto da multiplicacao! ")
valor_01 = int(input("Valor 01: "))
valor_02 = int(input("Valor 02: "))

multiplicacao = valor_01 * valor_02

print(f"O resultado da divisão é: {multiplicacao} ")
```
4. Faça um programa que peça dois números inteiros e imprima a divisão inteira do primeiro pelo segundo.
```python

valor_01 = int(input("Valor 01: "))
valor_02 = int(input("Valor 02: "))

divisao_inteira = valor_01 // valor_02

print(f"O resultado da divisão é: {divisao_inteira} ")
```
5. Escreva um programa que calcule o quadrado de um número fornecido pelo usuário.
```python

valor_01 = int(input("Valor 01: "))


numero_quadro = valor_01 * valor_01

print(f"O resultado da divisão é: {divisao_inteira} ")
```
#### Números de Ponto Flutuante (`float`)

6. Escreva um programa que receba dois números flutuantes e realize sua adição.
	```python
valor_01 = float(input("Valor 01: "))
valor_02 = float(input("Valor 02: "))
usuario_soma = valor_01 + valor_02

print(f"A soma é {usuario_soma}")
	```
7. Crie um programa que calcule a média de dois números flutuantes fornecidos pelo usuário.
```python
  
valor_01 = float(input("Valor 01: "))
valor_02 = float(input("Valor 02: "))
usuario_média = (valor_01 + valor_02)/ 2

print(f"A Média é {usuario_média}")
```
8. Desenvolva um programa que calcule a potência de um número (base e expoente fornecidos pelo usuário).
```python
valor_01 = float(input("Valor 01: "))
valor_02 = float(input("Potência 02: "))
potencia = valor_01**valor_02

print(f"Essa é o número digitado: {valor_01} Sua potência: {potencia}")
```
9. Faça um programa que converta a temperatura de Celsius para Fahrenheit.
```python
# Faça um programa que converta a temperatura de Celsius para Fahrenheit.

valor_01 = float(input("Temperatura em C°: "))
conversao = (valor_01*(9/5)) + 32

print(f"Fahrenheit {conversao}°f")
```
10. Escreva um programa que calcule a área de um círculo, recebendo o raio como entrada.
```python
valor_01 = float(input("Raio do círculo: "))
calculo = 3.4*(valor_01**2)


print(f"Área: {calculo} cm")
```

#### Strings (`str`)

11. Escreva um programa que receba uma string do usuário e a converta para maiúsculas.
	```python
	valor_01 = str(input("Fale algo: ")).upper()
	print(valor_01)
	```
12. Crie um programa que receba o nome completo do usuário e imprima o nome com todas as letras minúsculas.
	```python
	valor_01 = str(input("Seu nome: ")).lower()
	print(valor_01)
	```
13. Desenvolva um programa que peça ao usuário para inserir uma frase e, em seguida, imprima esta frase sem espaços em branco no início e no final.
	```python
	valor_01 = str(input("Seu nome: ")).strip()
	print(valor_01)
	```
14. Faça um programa que peça ao usuário para digitar uma data no formato "dd/mm/aaaa" e, em seguida, imprima o dia, o mês e o ano separadamente.
	```python
	data = input("Digite uma data no formato dd/mm/aaaa: ")
	dia, mes, ano = data.split("/")
	print("Dia:", dia)
	print("Mês:", mes)
	print("Ano:", ano)
	```

15. Escreva um programa que concatene duas strings fornecidas pelo usuário.
	```python
	str1 = input("Digite a primeira frase ou palavra: ")
	str2 = input("Digite a segunda frase ou palavra: ")
	resultado = str1 + str2
	print("Resultado da concatenação:", resultado)
	```

#### Booleanos (`bool`)

16. Escreva um programa que avalie duas expressões booleanas inseridas pelo usuário e retorne o resultado da operação AND entre elas.
17. Crie um programa que receba dois valores booleanos do usuário e retorne o resultado da operação OR.
18. Desenvolva um programa que peça ao usuário para inserir um valor booleano e, em seguida, inverta esse valor.
19. Faça um programa que compare se dois números fornecidos pelo usuário são iguais.
20. Escreva um programa que verifique se dois números fornecidos pelo usuário são diferentes.

### Exercícios Resolução

### Exercício 1: Soma de Dois Números Inteiros

```python
# num1 = int(input("Digite o primeiro número inteiro: "))
# num2 = int(input("Digite o segundo número inteiro: "))
num1 = 8  # Exemplo de entrada
num2 = 12  # Exemplo de entrada
resultado_soma = num1 + num2
print("A soma é:", resultado_soma)
```

### Exercício 2: Resto da Divisão por 5

```python
# num = int(input("Digite um número: "))
num = 18  # Exemplo de entrada
resultado_resto = num % 5
print("O resto da divisão por 5 é:", resultado_resto)
```

### Exercício 3: Multiplicação de Dois Números

```python
# num1 = int(input("Digite o primeiro número: "))
# num2 = int(input("Digite o segundo número: "))
num1 = 5  # Exemplo de entrada
num2 = 7  # Exemplo de entrada
resultado_multiplicacao = num1 * num2
print("O resultado da multiplicação é:", resultado_multiplicacao)
```

### Exercício 4: Divisão Inteira do Primeiro pelo Segundo Número

```python
# num1 = int(input("Digite o primeiro número inteiro: "))
# num2 = int(input("Digite o segundo número inteiro: "))
num1 = 20  # Exemplo de entrada
num2 = 3  # Exemplo de entrada
resultado_divisao_inteira = num1 // num2
print("O resultado da divisão inteira é:", resultado_divisao_inteira)
```

### Exercício 5: Quadrado de um Número

```python
# num = int(input("Digite um número: "))
num = 6  # Exemplo de entrada
resultado_quadrado = num ** 2
print("O quadrado do número é:", resultado_quadrado)
```

### Exercício 6: Adição de Dois Números Flutuantes

```python
# num1 = float(input("Digite o primeiro número flutuante: "))
# num2 = float(input("Digite o segundo número flutuante: "))
num1 = 2.5  # Exemplo de entrada
num2 = 4.5  # Exemplo de entrada
resultado_soma = num1 + num2
print("A soma é:", resultado_soma)
```

### Exercício 7: Média de Dois Números Flutuantes

```python
# num1 = float(input("Digite o primeiro número flutuante: "))
# num2 = float(input("Digite o segundo número flutuante: "))
num1 = 3.5  # Exemplo de entrada
num2 = 7.5  # Exemplo de entrada
media = (num1 + num2) / 2
print("A média é:", media)
```

### Exercício 8: Potência de um Número

```python
# base = float(input("Digite a base: "))
# expoente = float(input("Digite o expoente: "))
base = 2.0  # Exemplo de entrada
expoente = 3.0  # Exemplo de entrada
potencia = base ** expoente
print("O resultado da potência é:", potencia)
```

### Exercício 9: Conversão de Celsius para Fahrenheit

```python
# celsius = float(input("Digite a temperatura em Celsius: "))
celsius = 30.0  # Exemplo de entrada
fahrenheit = (celsius * 9/5) + 32
print(f"{celsius}°C é igual a {fahrenheit}°F")
```

### Exercício 10: Área de um Círculo

```python
# raio = float(input("Digite o raio do círculo: "))
raio = 5.0  # Exemplo de entrada
area = 3.14159 * raio ** 2
print("A área do círculo é:", area)
```

### Exercício 11: Converter String para Maiúsculas

```python
# texto = input("Digite um texto: ")
texto = "Olá, mundo!"  # Exemplo de entrada
texto_maiusculas = texto.upper()
print("Texto em maiúsculas:", texto_maiusculas)
```

### Exercício 12: Imprimir Nome Completo em Minúsculas

```python
# nome_completo = input("Digite seu nome completo: ")
nome_completo = "Fulano de Tal"  # Exemplo de entrada
nome_minusculas = nome_completo.lower()
print("Nome em minúsculas:", nome_minusculas)
```

### Exercício 13: Remover Espaços em Branco de uma Frase

```python
# frase = input("Digite uma frase: ")
frase = "  Olá, mundo!  "  # Exemplo de entrada
frase_sem_espacos = frase.strip()
print("Frase sem espaços no início e no final:", frase_sem_espacos)
```

### Exercício 14: Separar Dia, Mês e Ano de uma Data

```python
# data = input("Digite uma data no formato dd/mm/aaaa: ")
data = "01/01/2024"  # Exemplo de entrada
dia, mes, ano = data.split("/")
print("Dia:", dia)
print("Mês:", mes)
print("Ano:", ano)
```

### Exercício 15: Concatenar Duas Strings

```python
# parte1 = input("Digite a primeira parte do texto: ")
# parte2 = input("Digite a segunda parte do texto: ")
parte1 = "Olá,"  # Exemplo de entrada
parte2 = " mundo!"  # Exemplo de entrada
texto_concatenado = parte1 + parte2
print("Texto concatenado:", texto_concatenado)
```

#### Exercício 16. Operador `and` (E lógico)

```python
# Exemplo de entrada
valor1 = True
valor2 = False
resultado_and = valor1 and valor2
print("Resultado do AND lógico:", resultado_and)
```

#### Exercício 17. Operador `or` (OU lógico)

```python
# Exemplo de entrada
resultado_or = valor1 or valor2
print("Resultado do OR lógico:", resultado_or)
```

#### Exercício  18. Operador `not` (NÃO lógico)

```python
# Exemplo de entrada
resultado_not = not valor1
print("Resultado do NOT lógico:", resultado_not)
```

#### Exercício 19.  Operador == (Igualdade)

```python
# Exemplo de entrada
num1 = 5
num2 = 5
resultado_igualdade = (num1 == num2)
print("Resultado da igualdade:", resultado_igualdade)
```

#### Exercício 20. Operador `!=` (Diferença)

```python
# Exemplo de entrada
resultado_diferenca = (num1 != num2)
print("Resultado da diferença:", resultado_diferenca)
```


