[[Aula_08 Utilizando Módulos(Biblioteca)|Aula anterior]]

![image 20.png|600](image%2020.png)

- Cada carácter ocupa 1 espaço e sempre começará a contar os espaços a partir do número 0(zero).
- IMPORTANTE: Python considera diferente uma letra maiúscula de minúscula

## ➖Fatiamento:

![image.png|150](image%201%202.png)

![image.png|600](image%202%202.png)

- Com a função: frase[9:13]: Será selecionado os espaços do texto em vermelho, lembrando que o ultimo valor, nesse caso o 13 não será selecionando, porque para selecionar o espaço 13 deverá adicionar +1 espaço. **O ultimo valor não entra no fatiamento!**

---

![image.png|150](image%203%201.png)

![image.png|600](image%204%201.png)

- Com a função: frase[9:21:2]: Irá selecionar do micro espaço 9 até o 20, mas irá pular a cada duas casa, como está no exemplo a cima.

---

![image.png|150](image%205%201.png)

- Com a função: frase[:5]: Irá selecionar desde o início, como se fosse; frase[0:5].

![image.png|600](image%206%201.png)

---

![image.png|150](image%207%201.png)

- Com a função: frase[15:]: Irá selecionar do 15 até o fim

![image.png|600](image%208%201.png)

---

![image.png|150](image%209%201.png)

- Com a função: frase[9::3]: Irá selecionar do 9 até o fim pulando 3 micro espaços.

![image.png|600](image%2010%201.png)

---

## ➖ Analise:

![image.png|150](image%2011%201.png)

- len(frase): Usado para contar o número de micro espaços.
    
    ![image.png|600](image%2012%201.png)
    

![image.png|150](image%2013%201.png)

- frase.find(’deo’):  Retorna o valor de onde está o “deo”. Caso a string dentro da função não seja achada, será retornado o valor **-1**.

![image.png|600](image%2014%201.png)

![image.png](image%2015.png)

- frase.count(’o’):  Mostra quantos “o” possuem na frese toda.
    
    ![image.png](image%2016.png)
    

![image.png](image%2017.png)

- frase.count(’o’):  Mostra quantos “o” possuem dentro do micro espaço 0 até o 12.
    
    ---
    
    ![image.png](image%2018%201.png)
    
    - ‘Curso’ in frase: Operador que retorna True ou False, caso possua a palavra curso na string.
        
        ---
        

---

## ➖ Transformação:

![image.png](image%2019%201.png)

- frase.replace(’Python’, ’Android’): Faz a troca da palavra **Python** por **Android** .
    
    ---
    

![image.png](image%2020%201.png)

- frase.upper(): Método usado para deixar o que está em minúsculo em maiúsculo.
    
    ![image.png](image%2021.png)
    

![image.png](image%2022.png)

- frase.lower(): Método usado deixar o que está em maiúsculo em minúsculo.
    
    ![image.png](image%2023.png)
    

![image.png](image%2024.png)

- frase.capitalize(): Método usado para deixar uma string inteira com letras minúsculas e apenas a primeira letra em maiúsculo .
    
    ![image.png](image%2025.png)
    

![image.png](image%2026.png)

- frase.capitalize(): Método usado para analisar a string e deixar cada palavra com sua primeira letra em maiúsculo.
    
    ![image.png](image%2027.png)
    

---

![image.png](image%2028.png)

- frase.strip( ): Método usado para excluir espaços inúteis, com no exemplo abaixo:
    
    ![image.png](image%2029.png)
    

![image.png](image%2030.png)

- frase.rstrip( ): Método usado para excluir espaços inúteis apenas os últimos espaços.

![image.png](image%2031.png)

---

![image.png](image%2032.png)

- frase.lstrip( ): Método usado para excluir espaços inúteis apenas os espaçoes iníciais.

---

## ➖ Divisão:

## ➖ Junção:

![image.png](image%2033.png)

- frase.split( ): 01- Identifica os espaços em branco na string. 02- Divide a string onde esses espaços ocorrem. 03- Cria uma lista onde cada elemento é uma palavra (ou sequência de caracteres) que estava separada por um espaço.

![image.png](image%2034.png)

![image.png](image%2035.png)

- ‘-’join(frase): Uni os elementos de frase colocando o símbolo **cinza** entre cada palavra ou espaço vazio.

---

<aside>
❌ função das (‘’’’’’frase’’’’’’) 3 aspas:

**Strings de Múltiplas Linhas**: Elas permitem que você crie strings que se estendem por várias linhas sem a necessidade de concatenar ou usar caracteres de escape para as quebras de linha. Isso é útil quando você precisa definir um texto longo.

```python
texto_longo = '''Este é um texto que
se estende por várias
linhas.'''
```

</aside>

❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌

---

- Exercício/Desafio022: Crie um programa que leia o nome completo de uma pessoa e mostre: 
01- O nome com todas as letras maiúsculas.✅
02-O nome com todas minúsculas.✅
03-Contar quantas letras ao todo(sem considerar espaços).✅
04-Quantas letras tem o primeiro nome.✅
    
    ```python
    nome_complt=input('Escreva seu nome completo?:') 
    #01-Pergunte o nome
    frase01=('Esse é seu nome com Upper:')
    print(frase01, nome_complt.upper())
    #02-Escreve o nome com a função Upper 
    print('Esse é seu nome com Lower', nome_complt.lower())
    #03-Escreve o nome com a função Lower
    nome_complt01=(nome_complt.split())
     #04-Cria a separação das palavras e transforme em lista
    nome_complt02=''.join(nome_complt01)
    #05-Uni a lista sem espaços vazios entre elas
    print('Espaços totais sem contar espaços vazios:',(len(nome_complt02)))
    #06- Escreve a quantidade de espaços totais, sem contar os espaços vázios
    print('Espaços primeira letra:',len(nome_complt01[0]))
    #07- Conta os espaços da primeira palavra
    
    ```
    
    ![image.png](image%2036.png)
    
    ```python
    nome=str(input('Digite seu nome completo:')).strip()
    print('Analisando seu nome...')
    print(f'Seu nome em maiúsculo é {nome.upper()}.')
    print(f'Seu nome em minúsculo é {nome.lower()}.')
    print(f'Seu nome tem ao todo {len(nome)-nome.count(' ')} letras.')
    
    print(f'Seu primeiro nome tem {nome.find(' ')} letras.')
    #ou opção a baixo transformando em lista.
    separa=nome.split()
    print(f'Seu primeiro nome é {separa[0]} e ele tem {len(separa[0])} letras.')
    ```
    

❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌

---

- Exercício/Desafio023: Faça um programa que leia um número de 0 a 9999 e mostre na tela cada um dos dígitos separadas.
    
    ```python
    num=int((input('Digite um número de 0 até 9999:')))
    u= num // 1 % 10 # 
    d= num // 10 % 10
    c= num // 100 % 10
    m= num // 1000 % 10
    print(f'Número escolhido:{num}')
    print(f'Unidade:{u}')
    print(f'Dezena:{d}')
    print(f'Centena:{c}')
    print(f'Milhar:{m}')
    ```
    
    ![image.png](image%2037.png)
    

❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌

- Exercício/Desafio024: Crie um programa que leia o nome de uma cidade e diga se ela **começa** ou não com o nome “Santo”.
    
    ```python
    city=input('Me diga uma cidade?')
    #01- Pergunta a cidade
    city_lista=(city.split())
    #02-Converte em lista
    capitalize=city_lista[0].capitalize()
    #03-Converte a lista 0 para capitalize e evitar com que o úsuario que digitou com letras minúsculas dê a resposta False, devido "Santo" possui "S" em maiúsculo.
    res=('Santo' in capitalize)
    #04- Pergunta se possui Santo dentro de capitalize
    print(f'Possui "Santo" no primeiro nome? {res}')
    #05- Responde True ou False
    ```
    
    ![image.png](image%2038.png)
    
    ![image.png](image%2039.png)
    
    ![image.png](image%2040.png)
    
    ```python
    city=str(input('Me diga uma cidade?')).strip()
    print(city[:5].upper() == 'SANTO)')
    
    ```
    

❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌

- Exercício/Desafio025: Crie um programa que leia o nome de uma pessoa e diga se ela tem “SILVA” no nome.
    
    ```python
    nome=input('Qual é o seu nome completo?')
    #01- Pergunta o nome
    convert_cap=nome.title()  
    #02- Converte em title
    res=('Silva' in convert_cap)
    #03- Pergunta se possuí Silva dentro de convert_cap
    print(f'Esse nome possui Silva?: {res}')
    #04- Da a resposta
    ```
    
    ![image.png](image%2041.png)
    
    ![image.png](image%2042.png)
    
    ![image.png](image%2043.png)
    

❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌

- Exercício/Desafio026: Faça um programa que leia uma frase pelo teclado e mostre:
    - Quantas vezes aparece a letra “A”.
    - Em que posição ela aparece a primeira vez.
    - Em que posição ela aparece a última vez.
    
    ```python
    frase=input('Digite algo:')
    #01-Pergunta a frase
    frase_convert=frase.lower()
    #02- Transforma a frase em lower.
    print('Números de "A":',frase_convert.count('a'))
    #03- Conta quantos A possuem
    print('O primeiro "A" aparece no espaço:',frase_convert.find('a')+1)
    #04- Mostra quanto aparece o primeo A
    print('O último "A" aparece no espaço:',frase_convert.rfind('a')+1)
    #05- Mostra quanto o último A aparece contando da direita para esquerca, adicionando "R" no comando frase_convert.rfind('a')
    ```
    

❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌❌