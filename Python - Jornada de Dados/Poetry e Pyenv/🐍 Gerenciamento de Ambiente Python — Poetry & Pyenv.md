[[Jornada dos dados]]  #terminal
---

# 🔵 PYENV — Gerenciar versões do Python

## 📌 Instalar e listar versões
```bash
pyenv install --list         # Mostra todas as versões disponíveis
pyenv install 3.12.1         # Instala uma versão específica do Python
pyenv versions               # Lista as versões instaladas
pyenv version                # Mostra a versão ativa
````

## 📌 Definir versão do Python

```bash
pyenv global 3.12.1          # Define a versão global do sistema
pyenv local 3.11.5           # Define a versão para a pasta atual (.python-version)
pyenv shell 3.10.0           # Define versão apenas para a sessão atual
```

## 📌 Rehash (importante após instalar libs com binários)

```bash
pyenv rehash
```

## 📌 Remover uma versão

```bash
pyenv uninstall 3.11.5
```

---

# 🟣 POETRY — Gerenciar dependências e ambientes

## 📌 Criar projeto

```bash
poetry new meu_projeto                # Cria nova estrutura de projeto
poetry new --src meu_projeto          # Cria com pasta /src
```

## 📌 Inicializar Poetry num projeto existente

```bash
poetry init                           # Inicia e cria pyproject.toml
```

## 📌 Criar/ativar ambiente virtual

```bash
poetry install                        # Cria e instala dependências
poetry env list                       # Lista ambientes criados
poetry env use python3.12             # Força Poetry a usar versão específica
```

## 📌 Ativar ambiente virtual

```bash
poetry shell                          # Entra no ambiente virtual
exit                                  # Sai do ambiente
```

## 📌 Instalar pacotes

```bash
poetry add requests                   # Instala e adiciona ao projeto
poetry add numpy pandas               # Instala vários
poetry add django@4.2                 # Instala versão específica
poetry add pytest --dev               # Instala como dependência de desenvolvimento
```

## 📌 Remover pacotes

```bash
poetry remove requests
```

## 📌 Atualizar dependências

```bash
poetry update                         # Atualiza tudo
poetry update pandas                  # Atualiza pacote específico
```

## 📌 Rodar comandos no ambiente virtual

```bash
poetry run python main.py             # Executa script com env do Poetry
poetry run pytest                     # Roda testes
```

## 📌 Mostrar dependências

```bash
poetry show                           # Lista pacotes instalados
poetry show --tree                    # Árvore de dependências
poetry show numpy                     # Informações do pacote
```

## 📌 Exportar dependências para requirements.txt

```bash
poetry export -f requirements.txt --without-hashes > requirements.txt
```

---

# 🔗 Integração PYENV + POETRY

## 📌 Usar Poetry com Python gerenciado pelo pyenv

```bash
pyenv install 3.12.1
pyenv local 3.12.1
poetry env use python3.12
```

Isso garante que o ambiente virtual do Poetry use exatamente a versão definida pelo pyenv.

---

# ⭐ Dicas avançadas

## 📌 Ver onde está o venv criado pelo Poetry

```bash
poetry env info
```

## 📌 Colocar o venv dentro do projeto

```bash
poetry config virtualenvs.in-project true
```

Resultado: cria `.venv/` na pasta do projeto.

## 📌 Resetar ambiente do projeto

```bash
poetry env remove python
poetry install
```

---
