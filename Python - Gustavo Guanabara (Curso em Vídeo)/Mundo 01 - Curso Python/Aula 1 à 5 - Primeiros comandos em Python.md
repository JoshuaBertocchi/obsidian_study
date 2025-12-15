[[Python - (03) TypeError, Type Check e Type Conversion em Python|Aula anterior]]
![imagem](print_aula_cursoemvideo01.png)
-Forma correta de se escrever Texto no Python
![imagem](print_aula_cursoemvideo02.png)
-Forma correta de se escrever **números** no **Python**
![imagem](print_aula_cursoemvideo03.png)

<aside> 
❌ OBS_01: Sempre escrever Python com letras **minúsculas no console!!**
</aside>

<aside> 
❌ OBS_02: “**=**” significa “Recebe”
</aside>

<aside> 👉🏼 print= Escreva input=Leia

</aside>

- O que são “Variáveis”? São dados, como nome, idade e sobrenome.

OBS: Toda “Variável” é um “Objeto” e o “Objeto é um pouco mais que uma Variável”

- Como registar uma variável com pergunta?(MODO_INTERATIVO)
    
    nome=input(’Qual é seu nome’)
    
    res: Joshua
    
    nome= Joshua
    
- Como salvar/registrar uma variável?
    

nome= ‘Joshua’

```
assim será salva a Variável “nome” como  “Joshua”, quando for pedir para o Python escrever “nome” ele informará o valor da variável.

ex: print(nome)
Joshua
```

- Como registar uma variável com pergunta?(MODO_INTERATIVO)
    
    nome=input(’Qual é seu nome’)
    
    res: Joshua
    
    nome= Joshua
    

Exercícios da aula:

DESAFIO_01: Crie um Script Python que leia o nome de uma pessoa e mostre uma mensagem de boas-vindas de acordo com o valor digitado.

Resposta:

```python
nome=input('Qual é seu nome completo?')
nome=print('Muito obrigado',nome, 'agora me fale mais sobre você!')
```

```python
msg01=('Digite seu nome:')
msg02=('É uma prazer lhe conhecer!')
nome=input(msg01)
nome=print(msg02)
```

```python
nome=input('Digite seu nome:')
print('É um prazer te conhecer,{}!'. format(nome))
```

```python
nome=input('Digite seu nome:')
print(f'É um prazer te conhecer {nome}')
```

DESAFIO_02: Crie um script Python que leia o dia, o mês e o ano de nascimento de uma pessoa e mostre uma mensagem com a data formatada.

Resposta:

```python
dia=input('Qual dia você nasceu?')
mês= input('Qual mês vocês nasceu?')
ano= input('E a última pergunta, qual o ano?')
ano=print ('Você nasceu no dia', dia,mês,ano,'Correto?')
```

DESAFIO_03: Crie um script Python que leia dois números e tenta mostrar a soma entre eles.

```python
numero01=int(input('Primeiro número'))
numero02=int(input('Segundo número'))
resultado= numero01 + numero02
print( resultado, 'é o valor')
```

```python
n1=int(input('Digite um número:'))
n2=int(input('Digite mais um número:'))
s=n1+n2
print('A soma vale',s) 
```

<aside> ❌ OBS: “int” foi usado para transformar os números que estão dentro do (__) em número inteiro, evitando o erro de 2+2=22 e sim 2+ 2=4

</aside>