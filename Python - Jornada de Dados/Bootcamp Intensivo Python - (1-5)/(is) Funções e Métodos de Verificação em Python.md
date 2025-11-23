Python: [[Python - (01) Python, Git e VScode (Python do Zero)|Python]] #python 
## 🔹 Comparação e Identidade

- **`is`**  
    Verifica se duas variáveis apontam para o _mesmo objeto_ na memória.
    
    ```python
    a is b
    ```
    
- **`is not`**  
    Verifica se _não_ são o mesmo objeto.
    
    ```python
    a is not b
    ```
    

---

## 🔹 Verificação de Tipo

- **`isinstance(obj, tipo)`**  
    Retorna `True` se o objeto for de um tipo específico.
    
    ```python
    isinstance(10, int)  # True
    ```
    
- **`issubclass(classe, classe_pai)`**  
    Verifica se uma classe é filha de outra.
    
    ```python
    issubclass(bool, int)  # True
    ```
    

---

## 🔹 Métodos de Strings (checagens)

Esses métodos retornam **True/False**.

### 🔤 Conteúdo de texto

- **`str.isalpha()`**  
    Verifica se só tem letras (A–Z, a–z).
    
- **`str.isdigit()`**  
    Verifica se só tem números (0–9).
    
- **`str.isnumeric()`**  
    Verifica números inclusive fracionários/romanos.
    
- **`str.isdecimal()`**  
    Verifica decimal puro (0–9), mais restrito que `isdigit()`.
    
- **`str.isalnum()`**  
    Verifica se contém somente letras e números.
    
- **`str.isascii()`**  
    Verifica se todos os caracteres são ASCII.
    

### 🔡 Caixa de texto

- **`str.islower()`**  
    Verifica se todas são minúsculas.
    
- **`str.isupper()`**  
    Verifica se todas são MAIÚSCULAS.
    
- **`str.istitle()`**  
    Verifica se está em formato Título (Cada Palavra Começa com Letra Maiúscula).
    

---

## 🔹 Métodos sobre Espaços

- **`str.isspace()`**  
    Verifica se a string contém apenas espaços/brancos.
    
- **`str.isprintable()`**  
    Verifica se todos os caracteres são imprimíveis.
    
- **`str.isidentifier()`**  
    Verifica se a string pode ser usada como nome de variável.
    

---

## 🔹 Verificações Numéricas (nativas)

- **`math.isnan(x)`**  
    Verifica se valor é NaN.
    
- **`math.isinf(x)`**  
    Verifica se é infinito.
    
- **`math.isfinite(x)`**  
    Verifica se é um número finito.
    

---

## 🔹 Verificação de Coleções

- **`in`**  
    Verifica se um item existe em uma lista, string, tupla, etc.
    
    ```python
    if "a" in "banana": ...
    ```
    
- **`not in`**  
    Inverso do anterior.
    

---

## 🔹 Verificações Booleanas

- **`bool(obj)`**  
    Converte para booleano seguindo regras de "verdade" em Python.  
    Objetos vazios → False  
    Objetos com valor → True
    

---

## 🔹 Verificação de Atributos

- **`hasattr(obj, "atributo")`**  
    Verifica se o objeto possui um atributo.
    
- **`callable(obj)`**  
    Verifica se o objeto pode ser chamado como função.
    

---

## 🔹 Verificação de Arquivos (módulo os)

- **`os.path.exists(caminho)`**
    
- **`os.path.isfile(caminho)`**
    
- **`os.path.isdir(caminho)`**
    

---
