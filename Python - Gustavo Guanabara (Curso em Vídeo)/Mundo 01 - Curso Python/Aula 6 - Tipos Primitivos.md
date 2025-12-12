O que é Tipos Primitivos?

- **Números inteiro(int)**: 1, 7, 23, -453, 3453
- **Números reais ou ponto flutuante(float):** 23.12 , 204.0, -43.3, 7.0
- **Valor booleano ou valor lógico(bool):** True, False ❌OBS: deixar o T ou F em maiúscula.
- **STRING ou STR(’ESCREVA ENTRE ASPAS””’):** ‘Olá’ , ‘7.5’, ‘ ‘.

**Exemplo da aula:**

```python
n1=int(input('Digite um número:'))
n2=int(input('Digite mais um número:'))
s=n1+n2
print('A soma vale',s)
```

**Exemplo da aula:** Forma adicionando a função { }.

```python
print('A soma vale{}'.format(s))
```

<aside> ❌ OBS_01: Onde está o S, você adiciona o que você quer que apareça onde está as { }.

</aside>

<aside> ❌ OBS_02: A junção de 2 STRING/’STR’ são chamadas de concatenação ou concatenando.

</aside>

**Exercício aula 06: Crie uma soma, onde a frase da resposta seja: ‘A soma entre (número 01) e (número 02) é igual a {resposta}?’**

```python
n1=int(input('Digite um número))
n2=int(input('Digite o próximo número))
s=n1+n2
print(f'A soma entre {n1} e {n2} é igual a {s}'.)
												OU
print('A soma entre {n1} e {n2} é igual a {s}'.format(n1=n1,n2=n2,s=s))
												OU
print('A soma entre {} e {} é igual a {}.'.format(n1,n2,s))
```

---

# Tipos Primitivos(Conversão)

Usados para converter os valores

```python
n=float(input('Digite um valor:'))
print(n)
 
n=str(input('Digite um valor:'))
print(n)

n=bool(input('Digite um valor:'))
print(n)

n=int(input('Digite um valor:'))
print(n)
```

Ao colocar os comandos no início da expressão irá converter os valores do input:

- Float: converte o número em ponto flutuante. Ex: 4.0
- Str: converte o valor em stringer.
- bool(boleano): Apenas True ou False.

OBS: True=Quando possui algum valor atribuído. False= sem valor atribuído.

- int: Transforma em número inteiro

Comandos para identificação:

comando para retornar True ou False

```python
n=input('Digite algo:')
print(n.isalpha())
```

<aside> ❌ OBS: “.” É usado para chamar um método de um objeto.

</aside>

### - Exercício/Desafio004: Faça um programa que leia algo pelo teclado e mostre na tela o seu tipo primitivo e todas as informações possíveis sobre ela.

RESPOSTA: 

```python
P=input('Digite algo:')
print('1-É do tipo primitivo', type(p))
print('2-Possui apenas números?',p.isnumeric())
print('3-Possui apenas letras?',p.isalpha())
print('4-Possui letras ou número?',p.isalnum())
print('5-Possui todas a letras em maiúsculo?',p.isupper())
print('6-Está captalizada?',p.istitle())
```
