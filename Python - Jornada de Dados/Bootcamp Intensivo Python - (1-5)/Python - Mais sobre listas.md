[Documentação Python -  Mais sobre listas](https://docs.python.org/pt-br/3.7/tutorial/datastructures.html#more-on-lists)
[[Python - (05) Type hint, Tipos complexos (Dicionários vs DataFrames Vs Tabelas Vs Excel) e Funções | Aula do conteúdo]]

Aqui está o texto ajustado para o formato Markdown, com a formatação adequada para código, títulos e listas, mantendo o conteúdo original.

---

## 5.1. Mais sobre listas

O tipo de dado lista tem ainda mais métodos. Aqui estão apresentados todos os métodos de objetos do tipo lista:

- list.append(x)
    
    Adiciona um item ao fim da lista. Equivalente a a[len(a):] = [x].
    
- list.extend(iterable)
    
    Prolonga a lista, adicionando no fim todos os elementos do argumento iterable passado como parâmetro. Equivalente a a[len(a):] = iterable.
    
- list.insert(i, x)
    
    Insere um item em uma dada posição. O primeiro argumento é o índice do elemento anterior ao qual você deseja inserir, então a.insert(0, x) insere um elemento na frente da lista e a.insert(len(a), x) é equivalente a a.append(x).
    
- list.remove(x)
    
    Remove o primeiro item encontrado na lista cujo valor é igual a x. Se não existir valor igual, uma exceção ValueError é levantada.
    
- list.pop([i])
    
    Remove um item em uma dada posição na lista e o retorna. Se nenhum índice é especificado, a.pop() remove e retorna o último item da lista. (Os colchetes ao redor do i na demonstração do método indica que o parâmetro é opcional, e não que é necessário escrever estes colchetes ao chamar o método. Você verá este tipo de notação frequentemente na Biblioteca de Referência Python.)
    
- list.clear()
    
    Remove todos os itens de uma lista. Equivalente a del a[:].
    
- list.index(x[, start[, end]])
    
    Devolve o índice base-zero do primeiro item cujo valor é igual a x, levantando ValueError se este valor não existe.
    
    Os argumentos opcionais start e end são interpretados como nas notações de fatiamento e são usados para limitar a busca para uma subsequência específica da lista. O índice retornado é calculado relativo ao começo da sequência inteira e não referente ao argumento start.
    
- list.count(x)
    
    Retorna o número de vezes em que x aparece na lista.
    
- list.sort(key=None, reverse=False)
    
    Ordena os itens na lista (os argumentos podem ser usados para personalizar a ordenação, veja a função sorted() para maiores explicações).
    
- list.reverse()
    
    Inverte a ordem dos elementos na lista.
    
- list.copy()
    
    Devolve uma cópia rasa da lista. Equivalente a a[:].
    

Um exemplo que usa a maior parte dos métodos das listas:

Python

```python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.count('apple')
2
>>> fruits.count('tangerine')
0
>>> fruits.index('banana')
3
>>> fruits.index('banana', 4)  # Find next banana starting a position 4
6
>>> fruits.reverse()
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
>>> fruits.append('grape')
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']
>>> fruits.sort()
>>> fruits
['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']
>>> fruits.pop()
'pear'
```

Você pode ter percebido que métodos como `insert`, `remove` ou `sort`, que apenas modificam a lista, não têm valor de retorno impresso – eles retornam1 o `None` padrão. 1 Isto é um princípio de2 design para todas as estruturas de dados mutáveis em Python.3456

### 5.1.1. Usando listas como pilhas

Os 11métodos de lista tornam muito fácil utilizar listas como pilhas, onde o item adicionado por último é o primeiro a ser recuperado (política “último a entrar, pr12imeiro a sair”). Para adicionar um item ao topo da pilha, use `append()`. Para recupera13r um item do topo14 da pilha use `pop()` sem nenhum índice. Por exemplo:1516

Python

```python
>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
>>> stack
[3, 4, 5, 6]
>>> stack.pop()
6
>>> stack.pop()
5
>>> stack
[3, 4]
```

### 5.1.2. Usando listas como filas

Você também pode us19ar uma lista como uma fila, onde o primeiro item adicionado é o primeiro a ser recuperado (política “primeiro a entrar, primeiro a sair”); porém, lista20s não são eficientes para esta finalidade. Embora `appends` e `pops` no final da lista sejam rápidos, fazer `inserts` ou `pops` n21o início da lista é lento (porque todos os demais elementos têm que ser deslocados).

Para implementar uma fila, use a25 classe `collections.deque` que foi projetada para permitir `appends` e `pops` eficientes 26nas duas extremidades. Por exemplo:2728

Python

```python
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])
```

---
