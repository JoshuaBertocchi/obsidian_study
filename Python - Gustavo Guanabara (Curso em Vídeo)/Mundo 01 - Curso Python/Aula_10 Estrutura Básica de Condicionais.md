[[Aula_09 Manipulando Texto|Aula anterior]]

No Python, as estruturas de controle de fluxo `if`, `elif`, e `else` são fundamentais para a tomada de decisões no código. Elas permitem que o programa execute diferentes blocos de código com base em condições específicas.

- **`if`**: Avalia uma condição. Se a condição for verdadeira, o bloco de código associado ao `if` será executado.
- **`elif`**: É uma combinação de "else" e "if". Ele é usado para testar outras condições quando a condição anterior (`if` ou outro `elif`) é falsa. O `elif` permite que o programa avalie múltiplas condições em sequência, executando o bloco de código correspondente à primeira condição verdadeira.
- **`else`**: É usado para definir o que deve ser executado quando todas as condições anteriores (`if` e `elif`) forem falsas, oferecendo uma alternativa final.

Essas estruturas são essenciais para tornar os programas mais dinâmicos e responsivos a diferentes situações, pois permitem a execução de blocos de código específicos com base nas condições definidas.

```python
#01- Primeira forma!!!(Estrutura de condicional composta!)

tempo=int(input('Quantos anos tem seu carro?'))
if tempo <=3:
    print('Carro novo')
else:
    print('Carro velho')
print('--FIM--')
```

```python
#02- Segunda forma!!!CONDIÇÃO SIMPLIFICADA!!!

tempo=int(input('Quantos anos tem seu carro?'))
print('carro novo' if tempo<=3 else'carro velho')
print('--FIM--')
```

### 1. **Operadores de Comparação**

Estes operadores comparam dois valores e retornam `True` ou `False`:

- `==`: Igual a
    - Verifica se dois valores são iguais.
    - Exemplo: `if a == b:`
- `!=`: Diferente de
    - Verifica se dois valores são diferentes.
    - Exemplo: `if a != b:`
- `>`: Maior que
    - Verifica se o valor da esquerda é maior que o da direita.
    - Exemplo: `if a > b:`
- `<`: Menor que
    - Verifica se o valor da esquerda é menor que o da direita.
    - Exemplo: `if a < b:`
- `>=`: Maior ou igual a
    - Verifica se o valor da esquerda é maior ou igual ao da direita.
    - Exemplo: `if a >= b:`
- `<=`: Menor ou igual a
    - Verifica se o valor da esquerda é menor ou igual ao da direita.
    - Exemplo: `if a <= b:`

### 2. **Operadores Lógicos**

Estes operadores combinam múltiplas condições:

- `and`: E lógico
    - Retorna `True` se ambas as condições forem verdadeiras.
    - Exemplo: `if a > 0 and b < 5:`
- `or`: Ou lógico
    - Retorna `True` se pelo menos uma das condições for verdadeira.
    - Exemplo: `if a > 0 or b < 5:`
- `not`: Negação lógica
    - Inverte o valor lógico da condição.
    - Exemplo: `if not a > 0:`

### 3. **Operadores de Pertinência**

Estes operadores verificam se um elemento está contido em uma sequência (como listas, strings):

- `in`: Verifica se um elemento está presente em uma sequência.
    - Exemplo: `if 'a' in 'apple':`
- `not in`: Verifica se um elemento **não** está presente em uma sequência.
    - Exemplo: `if 'b' not in 'apple':`

### 4. **Operadores de Identidade**

Estes operadores verificam se duas referências apontam para o mesmo objeto:

- `is`: Verifica se duas variáveis referenciam o mesmo objeto.
    - Exemplo: `if a is b:`
- `is not`: Verifica se duas variáveis **não** referenciam o mesmo objeto.
    - Exemplo: `if a is not b:`

```python
# Comparação simples
if a == b:
    print("a é igual a b")

# Verificando múltiplas condições
if a > 0 and b < 5:
    print("a é positivo e b é menor que 5")

# Negação lógica
if not a > 0:
    print("a não é positivo")

# Verificando pertencimento
if 'x' in "texto":
    print("O caractere 'x' está na string")

# Verificando identidade de objetos
if a is b:
    print("a e b são o mesmo objeto")
```

---

- Exercício/Desafio028: Escreva um programa que faça o computador “pensar”  em um número inteiro, entre 0 e 5 e peça para o usuário tentar descobrir qual foi o número escolhido pelo computador. O programa deverá escrever na tela se o usuário venceu ou perdeu!
    
    ```python
    import random , emoji
    
    print("(",'='*30,'Vamos ver quem ganha!!!', '='*30,')')
    
    num=[0,1,2,3,4,5]
    #num=list(range(0,10,2))
    
    num_maquina=int(random.choice(num))
    
    num_use=int(input('Estou pensando em um número de 0 a 5, qual será?'))
    
    if num_maquina == num_use:
        print(emoji.emojize(f'Parabéns :smile: você acertou!!!!\n O número foi {num_maquina}', language='alias'))
    else:
        print(f'Você errou, o número é: {num_maquina}')
    ```
    
    ```python
    from random import randint
    from time import sleep
    computador = randint(0,5) #Faz o computador "PENSAR"
    print('-=-'*20)
    print('Vou pensar em um número entre 0 e 5. Tente adivinhar...')
    print('-=-'*20)
    jogador = int(input('Em que número eu pensei?')) #jogando tenta adivinhar
    print('PROCESSANDO...')
    sleep(5) #Usado para o computador esperar 5 seg antes de enviar a resposta
    if jogador == computador:
        print('Parabéns!!! Você conseguiu me vencer!')
    else:
        print(f'GANHEI! Eu pensei no número {computador} e não no {jogador}!')
    ```
    
    <aside>
    📌
    
    import time(sleep(seg)): adicionado a resposta do exercício para esperar 5 segundos antes de soltar a resposta.
    
    </aside>
    

---

- Exercício/Desafio029: Escreva um programa que leia a velocidade de um carro. Se ela ultrapassar 80Km/h, mostre uma mensagem dizendo que ele foi multado. A multa vai custa R$7,00 por cada Km acima do limite.
    
    ```python
    v=float(input('Qual foi a velocidade?'))
    
    if v >=80:
        print(f'Calma calabreso, você foi mutado em R$:{(v-80)*7}!!!')
    
    else:
        print('Muito bem, você é um bom motorista.')
    ```
    
    ```python
    velocidade = float(input('Qual é a velocidade atual do carro?'))
    
    if velocidade > 80:
        print('MULTADO! Você excedeu o limite permitido que é de 80km/h')
        multa = (velocidade - 80) * 7
        print(f'Você deve pagar um multa de R${multa:.2f}!')
    
    print('Tenha um bom dia! Dirija com segurança!')
    
    ```
    
- Exercício/Desafio030: Crie um programa que leia um número inteiro e mostre na tela se ele é PAR ou ÍMPAR.
    
    ```python
    n=int(input('Digite um número:'))
    n_calculado= n%2
    
    if n_calculado == 0:
        print(f'O número {n} é par!')
    
    else:
        print(f'O número {n} é impar')
    ```
    

---

- Exercício/Desafio031: Desenvolva um programa que pergunte a distância de um viagem em Km. Calcule o preço da passagem, cobrando R$0,50 por Km para viagens de até 200km e R$0,45 para viagens mais longas.
    
    ```python
    v=int(input('Diga quantos Km será sua viagem:'))
    
    if v <=200: #Se v for maior que 200 o if funciona, se for abaixo o else funciona.
        v_maior= v * 0.50
        print(f'Sua viagem é maior que 200km a taxa será:R${v_maior}.')
    else:
        v_menor= v * 0.45
        print(f'Sua viagem é menor que 200km a taxa será: R${v_menor}.')
    ```
    
    ```python
    distância=float(input('Diga quantos Km será sua viagem:'))
    
    print(f'Você está prestes a começar uma viagem de {v}')
    preço = distância * 0.50 if distância <= 200 else distância * 0.45
    print(f'E o preço da sua passagem será de R${preço:.2f}')
    ```
    

---

- Exercício/Desafio032: Faça um programa que leia um ano qualquer e mostre se ele é BISSEXTO.
    
    ```python
    
    print('='*30, 'ANO BISSEXTO!!!','='*30)
    
    ano=int(input('Me informe o ano:'))
    
    calculo_01= ano % 4
    calculo_02= ano % 100
    calculo_03= ano % 400
    
    if (calculo_01 == 0) **and** (calculo_02 != 0) **or** (calculo_03 == 0):
        print(f'{ano} É um ano Bissexto!!!')
    
    else:
        print(f'O ano {ano} Não é Bissexto.')
    ```
    
    ```python
    from datetime import date #01-Usado para chamar o Parâmetro que identifica a data do pc que está rodando o código!
    print('='*30, 'ANO BISSEXTO!!!','='*30)
    
    ano=int(input('Me informe o ano:'))
    if ano == 0:
    		ano = **date.today().year** # date
    if (ano % 4 == 0) **and** (ano % 100 != 0) **or** (ano % 400 == 0):
        print(f'{ano} É um ano Bissexto!!!')
    
    else:
        print(f'O ano {ano} Não é Bissexto.')
    ```
    

---

- Exercício/Desafio033: Faça um programa que leia três números e mostre qual é o maior e qual é o menor .
    
    ```python
    n_01=int(input('Digite o 1° número:')) #01:Pergunta os números
    n_02=int(input('Digite o 2° número:'))
    n_03=int(input('Digite o 3° número:'))
    
    lista_n=[n_01, n_02, n_03] #02:Cria uma lista com os números informados
    lista_n.sort()#03: Usa o .sort para organizar a lista do menor para o maior número em ordem crescente, ex: 0, 1, 2, 3...
    
    print(f' O maior número é:{lista_n[2]}.' 
          f'\nO menor número é:{lista_n[0]}')
    ```
    
    ```python
    a=int(input('Digite o 1° número:'))
    b=int(input('Digite o 2° número:'))
    c=int(input('Digite o 3° número:'))
    # Verificando o menor valor
    menor = a
    if b < a and b < c:
          menor = b
    if c < a and c < b:
          menor = c
    # Verificando o maior valor
    maior = a
    if b > a and b > c:
          maior = b
    if c > a and c > b:
          maior = c
    print(f'O maior número é:{maior}.'
          f'\nO menor número é:{menor}.')
    
    ```
    

---

- Exercício/Desafio034: Escreva um programa que pergunte o salário de um funcionário e calcule o valor do seu aumento. Para salários superiores a R$ 1.250,00, calcule um aumento de 10%. Para os inferiores ou iguais aumento é de 15%.
    
    ```python
    salario=float(input('Me informe seu salário:'))
    
    calculo10= ((salario*10)/100)
    calculo15= ((salario*15)/100)
    salario10= salario+calculo10
    salario15= salario+calculo15
    
    if salario > 1249:
        print(f'Você ganhou um aumento de 10%({calculo10:.2f}), seu salário atual será:R${salario10:.2f}')
    
    else:
        print(f'Você ganhou um aumento de 15%({calculo15:.2f}), seu salário atual será:R${salario15:.2f}')
    ```
    
    ```python
    salário=float(input('Me informe seu salário:'))
    
    if salário <= 1250:
        novo = salário + (salário * 15 /100)
    else:
        novo = salário + (salário * 10 /100)
    
    print(f'Quem ganhava R$ {salário:.2f} passa a ganhar R${novo} agora.')
    ```
    

---

- Exercício/Desafio035: Desenvolva um programa que leia o comprimento de três retas e diga ao usuário se elas podem ou não formar um triângulo.
    
    ```python
    medida_a=float(input('Me diga a 1° médida do triângulo:'))
    medida_b=float(input('Me diga a 2° médida do triângulo:'))
    medida_c=float(input('Me diga a 3° médida do triângulo:'))
    
    if (medida_a + medida_b >= medida_c) and (medida_b + medida_c >= medida_a) and (medida_c + medida_a>= medida_b):
        print('O triângulo será formado')
    
    else:
        print('O triângulo não será formado')
    ```