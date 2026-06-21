# Operadores Lógicos em Python

> Aula completa para iniciantes — do básico às aplicações práticas

---

## Índice

1. [[#O que são operadores lógicos?]]
2. [[#Os três operadores]]
3. [[#Tabelas verdade]]
4. [[#Operadores relacionais vs lógicos]]
5. [[#Uso em estruturas condicionais]]
6. [[#Exemplos práticos do mundo real]]
7. [[#Curto-circuito (short-circuit evaluation)]]
8. [[#Boas práticas]]
9. [[#Erros comuns de iniciantes]]
10. [[#Exercícios práticos]]
11. [[#Mini desafios]]

---

## O que são operadores lógicos?

Operadores lógicos são usados para **combinar condições** e tomar decisões no código. Em Python, são escritos em inglês simples, ao contrário de linguagens como C ou JavaScript que usam símbolos (`&&`, `||`, `!`).

> 💡 Python usa `and`, `or` e `not` — palavras legíveis como frases em inglês.

---

## Os três operadores

### `and` — E lógico

Retorna `True` **somente se ambas** as condições forem verdadeiras.

> 🔐 Analogia: uma porta com **duas fechaduras** — ambas precisam estar abertas.

```python
# AND: as duas condições devem ser True
tem_cnh = True
tem_carro = True

if tem_cnh and tem_carro:
    print("Pode dirigir!")     # ← executa aqui

# E se uma for False?
tem_carro = False
if tem_cnh and tem_carro:
    print("Pode dirigir!")     # ← NÃO executa
```

---

### `or` — OU lógico

Retorna `True` se **pelo menos uma** das condições for verdadeira.

> 🚪 Analogia: uma porta com **duas maçanetas** — basta girar qualquer uma.

```python
# OR: basta uma condição ser True
tem_dinheiro = False
tem_cartao = True

if tem_dinheiro or tem_cartao:
    print("Pode pagar!")      # ← executa aqui

# Só False or False resulta em False
tem_dinheiro = False
tem_cartao = False
if tem_dinheiro or tem_cartao:
    print("Pode pagar!")      # ← NÃO executa
```

---

### `not` — NÃO lógico

**Inverte** o valor lógico de uma condição.

> 🪞 Analogia: um **espelho** — reflete o oposto do que vê.

```python
# NOT: inverte o valor lógico
chovendo = True

if not chovendo:
    print("Vá ao parque!")    # ← NÃO executa

chovendo = False
if not chovendo:
    print("Vá ao parque!")    # ← executa aqui

# not True  → False
# not False → True
```

---

## Tabelas verdade

### `and`

| A     | B     | A and B |
|-------|-------|---------|
| True  | True  | **True**  |
| True  | False | False   |
| False | True  | False   |
| False | False | False   |

> True **apenas** quando ambos são True.

---

### `or`

| A     | B     | A or B  |
|-------|-------|---------|
| True  | True  | **True**  |
| True  | False | **True**  |
| False | True  | **True**  |
| False | False | False   |

> False **apenas** quando ambos são False.

---

### `not`

| A     | not A |
|-------|-------|
| True  | False |
| False | True  |

---

## Operadores relacionais vs lógicos

Operadores **relacionais** comparam valores e produzem `True` ou `False`.  
Operadores **lógicos** combinam esses resultados.

| Tipo       | Operadores                          | Exemplo              | Resultado |
|------------|-------------------------------------|----------------------|-----------|
| Relacional | `>`, `<`, `==`, `!=`, `>=`, `<=`   | `idade >= 18`        | True/False |
| Lógico     | `and`, `or`, `not`                 | `a and b`            | True/False |

```python
idade = 20
altura = 1.75

# Operadores RELACIONAIS: comparam valores → produzem True/False
print(idade >= 18)        # True  (relacional)
print(altura > 1.80)      # False (relacional)

# Operadores LÓGICOS: combinam os resultados relacionais
print(idade >= 18 and altura > 1.70)  # True
print(idade >= 18 and altura > 1.80)  # False
print(idade >= 18 or  altura > 1.80)  # True
```

---

## Uso em estruturas condicionais

### Nível básico — verificação de acesso

```python
usuario = "admin"
senha = "1234"

if usuario == "admin" and senha == "1234":
    print("Bem-vindo ao sistema!")
else:
    print("Usuário ou senha incorretos.")
```

---

### Nível intermediário — sistema de notas

```python
nota = 7.5
frequencia = 80   # em %

if nota >= 7.0 and frequencia >= 75:
    print("Aprovado!")
elif nota >= 5.0 and frequencia >= 75:
    print("Recuperação!")
elif frequencia < 75:
    print("Reprovado por falta.")
else:
    print("Reprovado por nota.")
```

---

### Nível avançado — sistema de desconto em e-commerce

```python
valor_compra = 350
cliente_premium = True
tem_cupom = False
primeiro_compra = False

if cliente_premium and valor_compra >= 300:
    desconto = 0.15   # 15% para premium + valor alto
elif tem_cupom or primeiro_compra:
    desconto = 0.10   # 10% com cupom ou 1ª compra
elif valor_compra >= 200:
    desconto = 0.05   # 5% acima de R$200
else:
    desconto = 0

total = valor_compra * (1 - desconto)
print(f"Total: R$ {total:.2f}")  # R$ 297.50
```

---

## Exemplos práticos do mundo real

### Validação de formulário

```python
nome = "Ana"
email = "ana@email.com"
idade = 25

nome_valido = len(nome) >= 2
email_valido = "@" in email and "." in email
maior_de_idade = idade >= 18

if nome_valido and email_valido and maior_de_idade:
    print("Cadastro realizado com sucesso!")
else:
    print("Verifique os dados informados.")
```

---

### Sistema de permissões

```python
usuario = "joao"
eh_admin = False
eh_moderador = True
conteudo_proprio = True

# Admin ou moderador podem editar qualquer coisa
# Usuário comum só pode editar o próprio conteúdo
if eh_admin or eh_moderador or (not eh_admin and conteudo_proprio):
    print("Edição permitida!")
else:
    print("Sem permissão.")
```

---

### Verificação de horário de funcionamento

```python
hora_atual = 14  # 14h

dia_util = True
horario_comercial = 8 <= hora_atual <= 18
feriado = False

if dia_util and horario_comercial and not feriado:
    print("Loja aberta!")
else:
    print("Loja fechada.")
```

---

## Curto-circuito (short-circuit evaluation)

Python **para de avaliar** uma expressão assim que o resultado já é conhecido.

### Regras do curto-circuito

| Expressão            | O que Python faz                              | Resultado |
|----------------------|-----------------------------------------------|-----------|
| `False and True`     | Vê False → para. Não avalia o True.           | False     |
| `True and False`     | Vê True → continua. Avalia False.             | False     |
| `True or False`      | Vê True → para. Não avalia o False.           | True      |
| `False or True`      | Vê False → continua. Avalia True.             | True      |

### Uso prático: evitando erros

```python
# ❌ Sem short-circuit: pode causar erro
lista = []
# lista[0] > 10  ← IndexError! lista está vazia

# ✅ Com short-circuit: seguro
lista = []
if len(lista) > 0 and lista[0] > 10:
    print("Primeiro item é maior que 10")
# len([]) > 0 → False → para aqui, não acessa lista[0]
```

### Padrão idiomático: valor padrão com `or`

```python
nome = None
exibir = nome or "Visitante"
print(exibir)  # "Visitante"

nome = "Ana"
exibir = nome or "Visitante"
print(exibir)  # "Ana"
```

> 💡 `x or padrão` é um padrão idiomático do Python para definir valores padrão quando `x` pode ser `None`, vazio ou `0`.

---

## Boas práticas

### 1. Use parênteses para clareza

A precedência dos operadores é: `not` > `and` > `or`.

```python
# ❌ Difícil de ler
if a or b and c:   # and tem maior precedência que or

# ✅ Fácil de ler
if a or (b and c):  # intenção clara
```

---

### 2. Prefira condições positivas

```python
# ❌ Dupla negação confunde
if not not usuario_ativo:
    ...

# ✅ Direto ao ponto
if usuario_ativo:
    ...

# ❌ Negação desnecessária com else
if not erro:
    print("sucesso")
else:
    print("falhou")

# ✅ Lógica direta
if erro:
    print("falhou")
else:
    print("sucesso")
```

---

### 3. Extraia condições complexas em variáveis com nomes descritivos

```python
# ❌ Difícil de entender num relance
if idade >= 18 and renda >= 2000 and score >= 700 and not inadimplente:
    aprovar_credito()

# ✅ Autoexplicativo
maior_de_idade = idade >= 18
renda_adequada = renda >= 2000
bom_score      = score >= 700
sem_dividas    = not inadimplente

if maior_de_idade and renda_adequada and bom_score and sem_dividas:
    aprovar_credito()
```

---

### 4. Aproveite o curto-circuito para eficiência

```python
# Com and: coloque a condição que FALHA MAIS RÁPIDO primeiro
if arquivo_existe() and processar_arquivo():
    ...   # só processa se o arquivo existir

# Com or: coloque a condição que SUCEDE MAIS RÁPIDO primeiro
if cache_disponivel() or buscar_no_banco():
    ...   # evita busca no banco se cache funcionar
```

---

### 5. Use `in` para múltiplas comparações de igualdade

```python
# ❌ Verboso
if cor == "azul" or cor == "verde" or cor == "amarelo":
    ...

# ✅ Idiomático e legível
if cor in ("azul", "verde", "amarelo"):
    ...
```

---

## Erros comuns de iniciantes

### ❌ Erro 1: Esquecer de repetir a variável

```python
cor = "azul"

# ❌ ERRADO: "verde" é uma string não-vazia → sempre True!
if cor == "azul" or "verde":
    print("era azul ou verde")   # SEMPRE executa, independente do valor

# ✅ CORRETO
if cor == "azul" or cor == "verde":
    print("era azul ou verde")

# ✅ AINDA MELHOR
if cor in ("azul", "verde"):
    print("era azul ou verde")
```

> ⚠️ Uma string não-vazia como `"verde"` é sempre `True` em Python. Por isso `or "verde"` sempre passa.

---

### ❌ Erro 2: Usar `=` em vez de `==`

```python
x = 5
# if x = 5 and y = 3:  ← SyntaxError!

# ✅ CORRETO: == para comparar, = para atribuir
if x == 5 and x != 10:
    print("x é 5 e não é 10")
```

---

### ❌ Erro 3: Comparar booleano com `==`

```python
ativo = True

# ❌ Redundante
if ativo == True:
    ...

# ✅ Idiomático
if ativo:
    ...

# ❌ Também redundante
if ativo == False:
    ...

# ✅ Idiomático
if not ativo:
    ...
```

---

### ❌ Erro 4: Condição impossível ou sempre verdadeira

```python
n = 5

# ❌ Condição impossível (nunca será True)
if n < 0 and n > 0:
    print("impossível")   # nunca executa

# ❌ Condição sempre verdadeira
if n < 0 or n >= 0:
    print("sempre")       # sempre executa

# 💡 Dica: substitua valores concretos para validar sua lógica
# Se n=5: 5<0 (False) AND 5>0 (True) → False. Lógica correta!
```

---

## Exercícios práticos

### Exercício 1 — Fácil

**Qual é o resultado de `True and False or True`?**

```python
resultado = True and False or True
print(resultado)  # ?
```

<details>
<summary>Ver resposta</summary>

**Resultado: `True`**

O `and` tem precedência sobre o `or`, então Python avalia assim:
1. `True and False` → `False`
2. `False or True` → `True`

</details>

---

### Exercício 2 — Fácil

**Sem executar o código, qual será a saída?**

```python
x = 10
y = 5

if x > 8 and y < 10:
    print("A")
elif x > 8 or y > 10:
    print("B")
else:
    print("C")
```

<details>
<summary>Ver resposta</summary>

**Saída: `A`**

- `x > 8` → `True`
- `y < 10` → `True`
- `True and True` → `True` → entra no primeiro `if`

</details>

---

### Exercício 3 — Médio

**O código abaixo tem um bug. Encontre e corrija:**

```python
cor_favorita = "vermelho"

if cor_favorita == "azul" or "vermelho":
    print("Cor válida!")
```

<details>
<summary>Ver resposta</summary>

**Bug:** `"vermelho"` é uma string não-vazia, sempre `True`. A condição sempre passa.

```python
# ✅ Correto
if cor_favorita == "azul" or cor_favorita == "vermelho":
    print("Cor válida!")

# ✅ Melhor ainda
if cor_favorita in ("azul", "vermelho"):
    print("Cor válida!")
```

</details>

---

### Exercício 4 — Médio

**Dada `lista = []`, o que acontece com a expressão abaixo? Por quê?**

```python
lista = []
if len(lista) > 0 and lista[0] == 5:
    print("Primeiro item é 5")
```

<details>
<summary>Ver resposta</summary>

**Resultado:** Não imprime nada, e **não lança erro**.

Graças ao **short-circuit**: `len([]) > 0` é `False`, então Python para a avaliação e nunca acessa `lista[0]`, evitando o `IndexError`.

</details>

---

### Exercício 5 — Difícil

**Escreva o código que verifica se um número `n` está fora do intervalo [0, 100].**

<details>
<summary>Ver resposta</summary>

```python
n = 150

# Opção 1: com or
if n < 0 or n > 100:
    print("Fora do intervalo!")

# Opção 2: com not (nega o intervalo válido)
if not (0 <= n <= 100):
    print("Fora do intervalo!")
```

</details>

---

## Mini desafios

### 🧩 Desafio 1

Um sistema de votação aceita cadastro se:
- Maior de 18 anos **OU** estudante universitário
- **E** não tem pendências

Escreva a condição correta.

<details>
<summary>Ver resposta</summary>

```python
maior_18 = True
universitario = False
pendencias = False

if (maior_18 or universitario) and not pendencias:
    print("Cadastro aceito!")
else:
    print("Cadastro negado.")
```

> ⚠️ Os parênteses são essenciais! Sem eles, o `and` teria precedência e a lógica seria incorreta.

</details>

---

### 🧩 Desafio 2

Escreva uma função que retorna `True` se uma senha é válida. Critérios:
- Pelo menos 8 caracteres
- Contém pelo menos um número
- Não contém espaços

<details>
<summary>Ver resposta</summary>

```python
def senha_valida(senha):
    tem_tamanho = len(senha) >= 8
    tem_numero  = any(c.isdigit() for c in senha)
    sem_espacos = " " not in senha

    return tem_tamanho and tem_numero and sem_espacos

# Testes
print(senha_valida("abc123"))        # False (menos de 8 chars)
print(senha_valida("abcdefgh"))      # False (sem número)
print(senha_valida("abc 1234x"))     # False (tem espaço)
print(senha_valida("abc12345"))      # True ✅
```

</details>

---

### 🧩 Desafio 3

Um parque cobra entrada conforme a idade:
- Gratuito: menor de 5 anos **ou** maior de 65 anos
- Meia entrada: entre 5 e 17 anos **ou** estudante
- Inteira: demais casos

Escreva o sistema de cobrança.

<details>
<summary>Ver resposta</summary>

```python
def calcular_entrada(idade, estudante=False):
    gratuito     = idade < 5 or idade > 65
    meia_entrada = (5 <= idade <= 17) or estudante

    if gratuito:
        return "Gratuito"
    elif meia_entrada:
        return "Meia entrada: R$ 15,00"
    else:
        return "Inteira: R$ 30,00"

# Testes
print(calcular_entrada(3))           # Gratuito
print(calcular_entrada(70))          # Gratuito
print(calcular_entrada(15))          # Meia entrada
print(calcular_entrada(25, True))    # Meia entrada
print(calcular_entrada(30))          # Inteira
```

</details>

---

## Resumo rápido

| Operador | Retorna True quando...         | Retorna False quando...        |
|----------|-------------------------------|-------------------------------|
| `and`    | Ambos são True                | Pelo menos um é False         |
| `or`     | Pelo menos um é True          | Ambos são False               |
| `not`    | O valor original é False      | O valor original é True       |

### Precedência (maior para menor)

```
not  >  and  >  or
```

### Dicas de ouro

- Use **parênteses** sempre que misturar `and` e `or`
- Aproveite o **short-circuit** para evitar erros e ganhar eficiência
- Nomeie condições complexas em **variáveis descritivas**
- Prefira **condições positivas** — são mais fáceis de ler
- Use `in` para verificar **múltiplos valores** de igualdade

---

*Aula gerada com Claude — Anthropic*
