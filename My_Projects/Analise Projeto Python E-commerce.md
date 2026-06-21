# Análise Exploratória — Online Retail Dataset

## 1. Visão geral do dataset

O dataset contém **541.909 registros** e **8 colunas**, representando transações de um e-commerce britânico entre 2010 e 2011.

| Coluna        | Tipo original | Descrição                                                     |
| ------------- | ------------- | ------------------------------------------------------------- |
| `InvoiceNo`   | str           | Identificador da nota fiscal. Prefixo `C` indica cancelamento |
| `StockCode`   | str           | Código do produto                                             |
| `Description` | str           | Nome do produto                                               |
| `Quantity`    | int64         | Quantidade vendida. Valores negativos indicam devoluções      |
| `InvoiceDate` | str           | Data e hora da transação (necessita conversão)                |
| `UnitPrice`   | float64       | Preço unitário em libras esterlinas                           |
| `CustomerID`  | float64       | ID do cliente (float por conta dos nulos)                     |
| `Country`     | str           | País do cliente                                               |

---

## 2. Qualidade dos dados

### 2.1 Valores nulos

|Coluna|Nulos|% do total|
|---|---|---|
|`Description`|1.454|0,27%|
|`CustomerID`|135.080|24,93%|
|Demais colunas|0|0%|

`CustomerID` é o ponto crítico: quase **25% das transações não têm cliente identificado**. Essas linhas foram mantidas e o campo preenchido com `'Anonimo'` para preservar o volume de vendas na análise agregada.

### 2.2 Valores inválidos

- **Quantity negativa** — mínimo de `-80.995`. Registros com quantidade negativa representam devoluções e foram separados em um dataframe próprio (`df_devolucoes`) antes da limpeza principal.
- **UnitPrice negativo ou zero** — mínimo de `-11.062`. Preço inválido sem interpretação de negócio clara; registros removidos.
- **Cancelamentos** — notas com prefixo `C` em `InvoiceNo` foram isoladas em `df_cancelamentos`.

### 2.3 Duplicatas

Foram identificadas duplicatas pela combinação `InvoiceNo + StockCode`. Exemplo encontrado:

|InvoiceNo|StockCode|Description|Quantity|UnitPrice|
|---|---|---|---|---|
|536381|71270|PHOTO CLIP LINE|1|1.25|
|536381|71270|PHOTO CLIP LINE|3|1.25|

Mesmo produto, mesma nota, mesmo horário — com `Quantity` divergente. Não é possível determinar qual valor é correto, portanto **ambas as linhas foram removidas** (`keep=False`).

---

## 3. Decisões de limpeza

```python
# 1. Separar cancelamentos
df_cancelamentos = df[df['InvoiceNo'].str.startswith('C')]
df = df[~df['InvoiceNo'].str.startswith('C')]

# 2. Remover registros com preço ou quantidade inválidos
df_devolucoes = df[df['Quantity'] < 0]
df = df[(df['Quantity'] > 0) & (df['UnitPrice'] > 0)]

# 3. Tratar nulos
df['Description'] = df['Description'].fillna('Sem descrição')
df['CustomerID'] = df['CustomerID'].fillna('Anonimo')

# 4. Converter tipos
df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'])
df['CustomerID'] = df['CustomerID'].astype(str)

# 5. Remover duplicatas
df = df.drop_duplicates(subset=['InvoiceNo', 'StockCode'], keep=False)

# 6. Criar coluna de receita
df['TotalPrice'] = df['Quantity'] * df['UnitPrice']
```

---

## 4. Dataset resultante

||Antes|Depois|
|---|---|---|
|Total de linhas|541.909|—|
|Cancelamentos separados|—|`df_cancelamentos`|
|Devoluções separadas|—|`df_devolucoes`|
|Duplicatas removidas|—|`keep=False`|
|Nulos em CustomerID|135.080|0|
|Colunas adicionadas|8|`TotalPrice`|

> **Nota:** os dataframes `df_cancelamentos` e `df_devolucoes` foram preservados para análise futura de taxa de cancelamento e volume de devoluções por período.