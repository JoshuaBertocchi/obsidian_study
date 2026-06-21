# Lambda em Python

## O que é uma função lambda?

Uma **função lambda** é uma função anônima — ou seja, uma função _sem nome_ — definida em uma única linha. Ela é útil quando você precisa de uma função simples e rápida, sem querer (ou precisar) defini-la formalmente com `def`.

### Sintaxe

```python
lambda argumentos: expressão
```

- **`lambda`** → palavra-chave que declara a função anônima
- **`argumentos`** → parâmetros de entrada (igual ao `def`)
- **`expressão`** → o que será calculado e retornado automaticamente (não usa `return`)

---

## Comparação: `def` vs `lambda`

```python
# Função tradicional
def dobrar(x):
    return x * 2

# Função lambda equivalente
dobrar = lambda x: x * 2

# Ambas funcionam igual:
dobrar(5)  # → 10
```

> [!tip] Lambda retorna automaticamente Ao contrário do `def`, a lambda não usa `return`. O resultado da expressão já é o valor retornado.

---

## Lambda com condição (if/else)

Lambdas podem conter um **operador ternário** (if/else em linha):

```python
lambda x: "par" if x % 2 == 0 else "ímpar"
```

Isso é equivalente a:

```python
def par_ou_impar(x):
    if x % 2 == 0:
        return "par"
    else:
        return "ímpar"
```

---

## O método `.apply()` no Pandas

O `.apply()` aplica uma função a cada elemento de uma **Series** (coluna) ou linha de um **DataFrame**.

```python
df['coluna'].apply(alguma_função)
```

O Pandas vai passar cada valor da coluna como argumento para a função, um por vez, e montar uma nova Series com os resultados.

---

## Quebrando o seu código

```python
df['CustomerID'] = df['CustomerID'].fillna('Anonimo')
df['CustomerID'] = df['CustomerID'].apply(
    lambda x: str(int(x)) if x != 'Anonimo' else x
)
```

### Passo 1 — `fillna('Anonimo')`

```python
df['CustomerID'] = df['CustomerID'].fillna('Anonimo')
```

Substitui todos os valores `NaN` (nulos) da coluna pelo texto `'Anonimo'`.

Isso é necessário porque a coluna vem como `float` — e converter `NaN` direto para `int` gera um erro em Python.

|Antes|Depois|
|---|---|
|`17850.0`|`17850.0`|
|`NaN`|`'Anonimo'`|
|`13047.0`|`13047.0`|

### Passo 2 — `.apply(lambda ...)`

```python
df['CustomerID'].apply(
    lambda x: str(int(x)) if x != 'Anonimo' else x
)
```

Para **cada valor `x`** da coluna, a lambda faz:

```
Se x NÃO for 'Anonimo':
    → converte para int (remove o .0) → depois para str
Caso contrário (x == 'Anonimo'):
    → mantém 'Anonimo' como está
```

| Valor de entrada | Caminho percorrido        | Resultado   |
| ---------------- | ------------------------- | ----------- |
| `17850.0`        | `str(int(17850.0))`       | `'17850'`   |
| `'Anonimo'`      | retorna `x` sem alteração | `'Anonimo'` |
| `13047.0`        | `str(int(13047.0))`       | `'13047'`   |

### Por que `int()` antes de `str()`?

Sem o `int()` intermediário:

```python
str(17850.0)  # → '17850.0'  ← indesejado, mantém o ponto flutuante
```

Com o `int()`:

```python
str(int(17850.0))  # → '17850'  ← correto
```

---

## Resumo visual do fluxo

```
Coluna original (float com NaN)
         ↓
    .fillna('Anonimo')
         ↓
Coluna com NaN → 'Anonimo'
         ↓
    .apply(lambda x: ...)
         ↓
  Para cada x na coluna:
    ├── x != 'Anonimo' → str(int(x))   ex: '17850'
    └── x == 'Anonimo' → x             ex: 'Anonimo'
         ↓
Coluna final (string limpa)
```

---

## Quando usar lambda vs `def`?

|Situação|Recomendação|
|---|---|
|Lógica simples, usada uma vez|`lambda`|
|Lógica complexa ou reutilizável|`def`|
|Dentro de `.apply()`, `.map()`, `.filter()`|`lambda` costuma ser idiomático|
|Precisa de múltiplas linhas|`def` (lambda não suporta)|

---

## Outros exemplos práticos com `.apply()`

```python
# Colocar texto em maiúsculas
df['nome'].apply(lambda x: x.upper())

# Calcular faixa de idade
df['idade'].apply(lambda x: 'jovem' if x < 30 else 'adulto')

# Limpar espaços extras
df['cidade'].apply(lambda x: x.strip() if isinstance(x, str) else x)
```