[[Aula 6 - Tipos Primitivos|Aula anterior]]

![( + ) Operadores de soma/adição.|150](image%202%202.png)

( + ) Operadores de soma/adição.

Exemplo:⬇️

![image.png.|150](image%201%201.png)

![( - ) Operadores de subtração./10.|150](image%202%201.png)

( - ) Operadores de subtração.

Exemplo:⬇️

![image.png.|150](image%203%201.png)

---

![( * ) Operadores de Multiplicação..|150](image%204%201.png)

( * ) Operadores de Multiplicação.

Exemplo:⬇️

![image.png.|150](image%205%201.png)

![( / ) Operadores de Divisão..|150](image%206%201.png)

( / ) Operadores de Divisão.

Exemplo:⬇️

![image.png.|150](image%207%201.png)

---

![( ** ) Operadores de exponenciação ou potência. Ex: 5³= 5.5.5=125.|150](image%208%201.png)

( ** ) Operadores de exponenciação ou potência. Ex: 5³= 5.5.5=125

<aside>
❌ OBS: Sinal de igualdade deve ser usado com dois iguais. Ex: (==)

</aside>

![image.png](image%209.|150.png)

---

![( ** ) Operadores de divisão inteira. OBS: O resultado sempre dará um número inteiro. Ex: 5/2: 2.|150](image%2010%201.png)

( ** ) Operadores de divisão inteira. OBS: O resultado sempre dará um número inteiro. Ex: 5/2: 2

Exemplo:⬇️

![( % ) Operadores do resto da divisão](image%2011%201.png)

( % ) Operadores do resto da divisão

![image.png.|150](3df6ccb2-3e12-4a0f-b363-c2e185ce8fe5.png)

![image.png.|150](c148407b-c1f8-463a-b11b-31f63c2baff2.png)

- Nesse exemplo foi feito a divisão de **5/2**, devido a divisão ser feita com  ”// Divisão inteira“ a resposta só será com número inteiro e o que sobrar irá para o valor da “ % Resto da divisão” .

---

### Ordem da Precedência: **O que deve ser calculado primeiro!**

![image.png.|150](93efff73-f226-40ef-adf4-b6a60de368e9.png)

### 1- ( )

2- **

3- *,/,//, %

4- +, -

Exemplo:⬇️

1) 5 + 3 * 2==11

2) 3 * 5 + 4 ** 2 ==31 

3) 3*(5+4)**2==243

<aside>
❌ Como calcular a Raiz Quadrada: use a função: 81**(1/2):9.0 Lembrando:

</aside>

> “Calcular a raiz quadrada é a mesma coisa que pegar a potência do número e dividir por meio (1/2 ou 0,5).”by Guanabara
> 

<aside>
❌ Como calcular a Média: Soma os valores e divide pelo valor da quantidade de números. Exemplo: Nota_01: 2.0  Nota_02: 3.2 2.0+3.2= 5.2/2=2.6

</aside>

---

📝 Dica de formatação no Python(Alinhamento/centralização)

```python
nome=input('Qual é seu nome?')
print=('Prazer em lhe conhecer {}!'.format(nome))
```

- Para deixar o nome do input de maneira centralizada para direita, deve adicionar esse código dentro da máscara de substituição “ { } ”, assim: {:20}
{:<Valor do espaço} :Para esquerda 
{:>Valor do espaço} :Para direita
{:^Valor do espaço} :Centralizado
- Adicionar texto ou símbolo com o texto justificado/centralizado:
{:+<Valor do espaço}
{:=^Valor do espaço}
    
    ```python
    Prazer em lhe conhecer ====Joshua=====!
    ```
    

<aside>
📝 Dica de formatação no Python(Alinhamento/centralização)

```python
print(f'A soma é: {s}\n O Produto é {m} \n A Divisão é: {d:.3f} \n A Potência é: {p}', end='___')
```

\n : Usado para quebrar a linha

:.3f : Usado para converter a resposta em Float e deixar só 3 espaços para resposta. Ex: 3.00

end=’ escreva algo ou deixe espaços vazios ‘ : Usado para unir dois prints quando o comando for executado. Entre os ‘ ‘ 

</aside>

---

- Exercício/Desafio005: Faça um programa que leia um número Inteiro e mostre na tela o seu sucessor e seu antecessor!

Resposta: Minha maneira

```python
n1=int(input('Digite um número inteiros'))
n2=n1+1
n3=n1-1
print(f'O número foi: {n1}\n O antecessor é:{n3}\n O sucessor é {n2}')
```

![Comando executado!](8329d060-cd77-4f27-867e-f85543420885.png)

Comando executado!

```python
n1=int(input('Digite um número inteiros'))
print('O número foi: {n1}\n O antecessor é:{}\n O sucessor é {}'.format(n1, (n1-1),(n1+1)))
```

---

- Exercício/Desafio006: Crie um algoritmo que leia um número e mostre o seu dobro, triplo e raiz quadrada.

```python
n1=int(input('Digite um número')
n2=n1*2
n3=n1*3
n4=n1**(1/2)
print(f'Número escolhido:{n1}\n Seu dobro:{n2}\n Seu triplo:{n3}\n Sua raiz quadrada:{n4}')
```

![Comando executado!](image%2012%201.png)

Comando executado!

```python
n1=int(input('Digite um número')
n2=n1*2
n3=n1*3
n4=n1**(1/2)
print(f'Número escolhido:{n1}\n Seu dobro:{n2}\n Seu triplo:{n3}\n Sua raiz quadrada:{n4}')
```

---

- Exercício/Desafio007: Desenvolva um programa que leia as duas notas de um aluno, calcule e mostre a sua média!
    
    ```python
    nota01=float(input('Nota 1º semestre:'))
    nota02=float(input('Nota 2º semestre:'))
    nota03=(nota01+nota02)/2
    print(f'Sua média é:{nota03}'}
    ```
    
    ![Comando executado!](image%2013%201.png)
    
    Comando executado!
    

- Exercício/Desafio008: Escreva um programa que leia um valor em metros e o exiba convertido em centímetros!
    
    ```python
    medida=float(input('Valor em metros?')
    cm=m1*10
    mm=m2*100
    print(f'Valor em centímetros: {cm} cm\n Valor em milímetros: {mm}
    ```
    
    ![Comando executado!](image%2014%201.png)
    
    Comando executado!
    
    ```python
    medida=float(input('Valor em metros?'))
    print(f'Valor em Centímetros: {(medida*100)} cm\n Valor em Milímetros: {(medida*1000)} mm \n Valor em Decímetros:{(medida*10)} dm \n Valor em Decâmetros:{medida/10} dam\n Valor em Hectômetros:{medida/100}hm\n Valor em Quilômetros:{medida/1000}')
    ```
    

---

- Exercício/Desafio009: Faça um programa que leia um número inteiro qualquer e mostre na tela a sua tabuada.
    
    ```python
    print('='*25)
    n0=int(input('Veja a tabuada do número?'))
    n1=n0*1
    n2=n0*2
    n3=n0*3
    n4=n0*4
    n5=n0*5
    n6=n0*6
    n7=n0*7
    n8=n0*8
    n9=n0*9
    n10=n0*10
    print(f'Essa é a tabuada:\n{n0}x1={n1}\n{n0}x2={n2}\n{n0}x3={n3}\n{n0}x4={n4}\n{n0}x5={n5}\n{n0}x6={n6}\n{n0}x7={n7}\n{n0}x8={n8}\n{n0}x9={n9}\n{n0}x10={n10}')
    print('='*25)
    ```
    
    ![Comando executado!](image%2015.png)
    
    Comando executado!
    

---

- Exercício/Desafio010: Crie um programa que leia quanto dinheiro uma pessoa tem na carteira e mostre quantos Dólares ela pode comprar.
    
    ```python
    n0=float(input('Dólar($) para Reais(R$)?(Dolar:$5,47)R$:'))
    n1=n0/5.47
    print(f'Esse é o valor:${n1:.2f}')
    ```
    
    ![Comando executado!](image%2016.png)
    
    Comando executado!
    
    ---
    
    <aside>
    ❌ Segunda resposta:
    
    </aside>
    
    ```python
    n0=float(input('Dólar($) para Reais(R$)?R$:'))
    n1=float(input('Qual é o valor do Dólar($)atual:'))
    n2=n0/n1
    print(f'Esse é o valor:${n2}')
    ```
    
    ![Comando executado!](image%2017.png)
    
    Comando executado!
    

---

- Exercício/Desafio011: Faça um programa que leia a largura e a altura de uma parede em metros, calcule a sua área e a quantidade de tinta necessária para pintá-la, sabendo que cada litro de tinta, pinta uma área de 2m².
    
    ```python
    m1=float(input('Qual é a largura da parede?'))
    m2=float(input('Qual é a altura da parede?'))
    m3=m1*m2
    print(f'Esse é valor da área {m3}m²')
    valorfinal=m3/2
    print(f'Essa é a quantidade de tinta necessária:{valorfinal}L')
    print('='*50)
    ```
    
    ---
    
- Exercício/Desafio012: Faça um algoritmo que leia o preço de um produto e mostre seu novo preço, com 5% de desconto.
    
    ```python
    try:
        n1=float(input('Você ganhou 5% de desconto. Me diga o valor da sua compra:'))
        desconto01=n1*5/100
        desconto02=n1-desconto01
        print(f'Você ganhou R${desconto01:.2f} de desconto!!! Seu valor final ficou R${desconto02:.2f}')
    except:
        print('Apenas VALORES BURRO!!!')
    ```
    
    ![Comando executado!](image%2018%201.png)
    
    Comando executado!
    
    <aside>
    ❌ try e except: Usados para iniciar um loop caso a resposta esteja errado. Resposta certa vai para TRY respondeu errado vai para EXCEPT.
    
    </aside>
    
    <aside>
    ❌ Para calcular a % use essa fórmula:  (**Valor * %/100)**:Valor multiplicado pelo valor  da % dividido por 100
    
    </aside>
    
    ---
    
- Exercício/Desafio013: Faça um algoritmo que leia o salário de um funcionário e mostre seu novo salário, com 15% de aumento
    
    ```python
    aumento01=float(input('Parabéns você ganhou 15% de aumento no sálario!!! Qual é seu sálario atual?'))
    aumento02=(15/100)*aumento01
    aumento03=aumento02+aumento01
    print(f'Você ganhou 15% de aumento!!! Seu salário atual será R${aumento03}')
    ```
    
    ![Comando executado! ](image%2019%201.png)
    
    Comando executado! 
    
    ---
    
- Exercício/Desafio014: Escreva um programa que converta uma temperatura digitada em ºC e converta para ºF.
    
    <aside>
    ❌
    
    Formula para converter °C para °F: °F=(°C×9/5)+32
    
    </aside>
    
    ```python
    try:
    	c=float(input('Me diga o valor em °C:')
    	convertido= ((c*9)/5)+32
    	print(f'Esse é o valor final:{convertido}°F')
    except:
    print('='*40)
    print('Apenas números e (.) cabeça!!!')
    print('='*40)
    ```
    
    ---
    

- Exercício/Desafio015: Escreva um programa que pergunte a quantidade de Km percorridos por um carro alugado e a quantidade de dias pelos quais ele foi alugado. Calcule o preço a pagar, sabendo que o carro custa R$60 por dia e R$0,15 por Km rodado.
    
    ```python
    try:
        print('=' * 60)
        day = int(input('Quantos dias você ficou com o carro?'))
        print('=' * 60)
        km=float(input('Quantos Km você percorreu?'))
        print('=' * 60)
        v_day= day*60
        v_km= km*0.15
        v_total=v_day+v_km
        print(f'O valor a ser pago por dia é:{v_day:.2f}\n O valor a ser pago por Km é:{v_km:.2f}\n Valor total:{v_total:.2f}')
        print('=' * 60)
    except:
        print('Xx'*90)
        print('Apenas números!!!')
        print('Xx' * 90)
    ```
    
    ---