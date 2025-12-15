
[[Aula_7 Operadores Aritméticos|Aula anterior]])

### - Usado para trazer novas funcionalidades para código, trazendo módulos(bibliotecas) de fora do Python

![image 2.png|150](image%202%202.png)

![image.png|150](image%201%201.png)

- *import*: Usado para importar um módulo para o código.
- *from*: Usado para não ter que importar todo o módulo para dentro do código e sim trazendo algumas funcionalidades(economiza mais memória)

[Principais Funções e Constantes do Módulo `math` (1)](https://www.notion.so/Principais-Fun-es-e-Constantes-do-M-dulo-math-1-101f6b866a9d807db0aed838ac2a3a2d?pvs=21)

<aside>
<img src="https://www.notion.so/icons/graduate_green.svg" alt="https://www.notion.so/icons/graduate_green.svg" width="40px" /> Módulo *math*: 
-*ceil(teto)*:Faz arredondamento para cima.
-*floor(chão)*:Faz arredondamento para baixo.
-*trunc*(truncated):Faz o corte do número, tirando qualquer valor após a virgula de algum número. Ex 6.3 == 6
-*pow*(power): Calcula a potência
-*sqrt*(square root): Raiz quadrada
-*factorial*: Calculo de fatorial

</aside>

<aside>
<img src="https://www.notion.so/icons/graduate_green.svg" alt="https://www.notion.so/icons/graduate_green.svg" width="40px" /> *round*: Arredonda para o valor mais próximo. OBS: Não faz parte de nenhum modulo.

</aside>

<aside>
<img src="https://www.notion.so/icons/graduate_green.svg" alt="https://www.notion.so/icons/graduate_green.svg" width="40px" /> Comandos terminal:
instalar módulo: pip instal (nome do módulo)
não sei: -m pip
atualizar: - -upgrade pip

</aside>

```python
import match
num = int(input('Digite um número: ')
raiz = math.sqrt(num)
print(f'A raiz é {num}')
```

```python
import match
num = int(input('Digite um número: ')
raiz = math.sqrt(num)
print(f'A raiz é {math.floor(raiz)}')
```

---

- Exercício/Desafio016: Crie um programa que leia um número Real qualquer pelo teclado e mostre na tela sua porção inteira.
    
    ```python
    import math
    num = float(input('Digite um número flutuante:')
    print(f'Esse é o seu número inteiro:{math.trunc(num)}')
    ```
    
    ```python
    import math
    num = float(input('Digite um número flutuante:'))
    print(f'Esse é o seu número inteiro:{int(num)}')
    ```
    
    ```python
    from math import trunc
    num = float(input('Digite um número flutuante:'))
    print(f'Esse é o seu número inteiro:{trunc(num)}')
    ```
    

---

- Exercício/Desafio017: Crie um programa que leia o comprimento do cateto oposto e do cateto adjacente de um triângulo retângulo, calcule e mostre o comprimento da hipotenusa.
    
    ```python
    import math, emoji
    print(emoji.emojize(':triangular_ruler:'*20))
    cat = float(input('Digite o valor do cateto oposto:'))
    adja = float(input('Digite o valor do cateto adjacente:'))
    poten_soma = math.sqrt(cat**2 + adja**2)
    print(emoji.emojize(f'Valor hipotenusa:{poten_soma:.2f} :triangular_ruler:'))
    print(emoji.emojize(':triangular_ruler:'*20))
    ```
    
    ```python
    import math, emoji
    print(emoji.emojize(':triangular_ruler:'*20))
    cat = float(input('Digite o valor do cateto oposto:'))
    adja = float(input('Digite o valor do cateto adjacente:'))
    hi = math.hypot(cat, adja)
    print(emoji.emojize(f'Valor hipotenusa:{hi:.2f} :triangular_ruler:'))
    print(emoji.emojize(':triangular_ruler:'*20))
    ```
    

---

- Exercício/Desafio018: Faça um programa que leia um ângulo qualquer e mostre na tela o valor do **seno**, **cosseno** e **tangente** desse ângulo.
    
    ```python
    #1°- Faça a importação da biblioteca
    import math
    #2°- Crie o input para receber o valor do ângulo
    ang=float(input('Digite um ângulo:'))
    #3°- Uso o math.radians() para converter o valor de ângulos para radianos
    convert= math.radians(ang)
    #4°- Uso os comando math.sin(calcular o seno), math.cos(calcular o cosseno)
    # e math.tan(calcular a tangente).
    print(f'Resposta:'
    			f'\n Seno:{math.sin(convert):.3f}'
    			f'\n Cosseno:{math.cos(convert):.3f}'
    			f'\n Tangente:{math.tan(convert):.3f}')
    
    ```
    
    ```python
    from math import radians, sin, cos, tan
    ang=float(input('Digite um ângulo:'))
    convert=radians(ang)
    print(f'Resposta:'
          f'\n Seno:{sin(convert):.3f}'
          f'\n Cosseno:{cos(convert):.3f}'
          f'\n Tangente:{tan(convert):.3f}')
          #OBS: Quando importado apenas algumas funções da biblioteca não é necessário por o math. antes da função
    
    ```
    

---

- Exercício/Desafio019: Um professor quer sortear um dos seus quatro alunos para apagar o quadro. Faça um programa que ajude ele, lendo o nome deles e escrevendo o nome do escolhido.
    
    <aside>
    <img src="https://www.notion.so/icons/graduate_blue.svg" alt="https://www.notion.so/icons/graduate_blue.svg" width="40px" /> Lembrete: Nesse exercício deve ser usado o módulo ***random!!!*** Esse é o módulo que faz o **sorteio de números**.
    
    </aside>
    
    ```python
    #1°-Faça a importação da biblioteca
    import random
    #2°- Faça o input para saber o nome dos alunos, nesse caso são 4 alunos!!!
    aluno01=input('Nome do 1° aluno:')
    aluno02=input('Nome do 2° aluno:')
    aluno03=input('Nome do 3° aluno:')
    aluno04=input('Nome do 4° aluno;')
    #3°- Agora crie a parâmetro para sortear
    alunos=[aluno01, aluno02, aluno03, aluno04]
    #4°- |^|= foi criado o conjuto para ser sortado usando [ ]
    # alunos é o nome do valor que deve ser  
    sorteio=random.choice(alunos)
    print(f'O aluno sorteado foi {sorteio}')
    
    ```
    
    <aside>
    ❌ OBS: 
    Função: é uma sequência de instruções que executa uma tarefa específica
    Parâmetro:
    
    </aside>
    

 

---

- Exercício/Desafio020: O mesmo professor do desafio anterior quer sortear a ordem de apresentação de trabalhos dos alunos. Faça um programa que leia o nome dos quatro alunos e mostre a ordem sorteada.
    
    ```python
    #1°-Faça a importação da biblioteca
    
    import random
    #2°- Faça o input para saber o nome dos alunos, nesse caso são 4 alunos!!!
    aluno01=input('Nome do 1° aluno:')
    aluno02=input('Nome do 2° aluno:')
    aluno03=input('Nome do 3° aluno:')
    aluno04=input('Nome do 4° aluno;')
    #3°- Crie uma lista dos alunos usando colchetes [ ]
    alunos=[aluno01, aluno02, aluno03, aluno04]
    #4°- Faça o sorteio usando o parâmetro random.shuffle(x=alunos ou Lista para sortear).
    random.shuffle(alunos)
    #5°- Faça o print com as posições
    print(f'1°Aluno:{alunos[0]}\n'
          f'2°Aluno:{alunos[1]}\n'
          f'3°Aluno:{alunos[2]}\n'
          f'4°Aluno:{alunos[3]}')
    ```
    
    ```python
    import random
    #1°- Pergunte quantos alunos serão.
    qtd_alunos = int(input('Quantos alunos vamos sortear?'))
    #2°- Crie uma lista de alunos vazia, porque a função 
    for _ in range(qtd_alunos)
    #irá perguntar os nomes dos alunos baseado no número de alunos informados no input 
    alunos = []
    
    for _ in range(qtd_alunos):
        aluno = input(f"Informe o nome do aluno(a) {_+1}°:")
        alunos.append(aluno)
        
        #3°-função alunos.append(aluno): é usada para modificar a lista alunos=[], esse comando usa do input da variável aluno para adicionar o nome dos alunos dentro da lista alunos=[].
    
    #4- random.shuffle(x=alunos): Função que embaralha a lista alunos e cria o sorteio.
    random.shuffle(x=alunos)
    
    for aluno in alunos:
        print(aluno)
    ```
    

---

- Exercício/Desafio021: Faça um programa em Python que abra e reproduza o áudio de um arquivo MP3.
    
    ```python
    import pygame
    pygame.mixer.init() #1°-módulo para iniciar o pygame.
    pygame.mixer.music.load(R"C:\Users\joshu\Videos\aTubeCatcher\NAGALLI.mp3")#2°- módulo para carregar o arquivo mp3 para o código. R:usado para tratar o caminho como string, e não como caracteres especiais
    pygame.mixer.music.play() #3° Dar play na music(obs: por algum mótivo a música só será iniciado quando colocado os códigos abaixo)
    while pygame.mixer.music.get_busy(): #4°-Verifica se a música ainda está tocando. Retorna True enquanto a música estiver tocando e False quando a música parar.
        pygame.time.Clock().tick(10)#5°-Faz com que o loop espere 100 milissegundos (ou 0,1 segundo) antes de repetir a verificação. Isso limita o loop para rodar 10 vezes por segundo
        
        #resumo 4° e 5°: Esse código cria um loop que continua rodando enquanto a música está tocando, checando a cada 0,1 segundo se a reprodução terminou.
    ```