## Guia rápido: criação e uso de `.venv` no Python[[Gerenciamento de Ambiente|.]]

- Criar um ambiente virtual:
  - `python -m venv .venv`

- Ativar o ambiente virtual:
  - **Windows:** `.venv\Scripts\activate`
  - **Linux/Mac:** `source .venv/bin/activate`

- Desativar o ambiente virtual:
  - `deactivate`

- Instalar pacotes dentro do `.venv`:
  - `pip install nome-do-pacote`

- Gerar lista de dependências:
  - `pip freeze > requirements.txt`

- Instalar dependências do arquivo:
  - `pip install -r requirements.txt`

- Apagar o `.venv`:
  - basta excluir a pasta `.venv` inteira

- Verificar se está usando o `.venv` correto:
  - `where python` (Windows)
  - `which python` (Linux/Mac)

---
## 🔍 Diferença entre usar `.venv` e usar **Poetry**

### 🟦 **Usando `.venv` manualmente**

Quando você cria um `.venv` com:

```
python -m venv .venv
```

Você mesmo cuida de:

- ativar o ambiente
    
- instalar pacotes (`pip install ...`)
    
- gerar o `requirements.txt`
    
- controlar versões
    
- atualizar dependências manualmente
    
- lidar com conflitos de pacotes
    

Ou seja: **você controla tudo**, mas também **faz tudo sozinho**.

---

### 🟪 **Usando Poetry**

O **Poetry** é um gerenciador de dependências e ambientes Python mais moderno.  
Ele **cria e gerencia o `.venv` automaticamente** e ainda faz muito mais:

#### ✔️ Vantagens do Poetry

- Cria e ativa o ambiente automaticamente
    
- Controla as dependências de forma inteligente
    
- Garante versões compatíveis usando o arquivo `pyproject.toml`
    
- Substitui o `requirements.txt` por algo mais organizado
    
- Permite rodar scripts facilmente
    
- Faz publicação em repositórios (PyPI) se necessário
    

Exemplo de instalação de pacote:

```
poetry add pandas
```

Ele:

- instala o pacote no `.venv`
    
- salva a versão exata no `poetry.lock`
    
- atualiza o `pyproject.toml`
    

---

### 🟦 Comparação Rápida

|Recurso|`.venv` manual|Poetry|
|---|---|---|
|Criação de ambiente|manual|automático|
|Instalação de pacotes|pip install|poetry add|
|Controle de versões|requirements.txt|pyproject.toml + poetry.lock|
|Resolver conflitos|difícil|automático|
|Configurar scripts|manual|integrado|
|Reprodutibilidade do projeto|média|muito alta|
|Facilidade|simples|mais completo|
|Boa prática para projetos grandes|❌ não ideal|✔️ recomendado|

---

### 🎯 Resumo Final

- **.venv** = simples, manual, bom para projetos pequenos ou estudo.
    
- **Poetry** = gerenciador completo; cria `.venv`, controla versões, pacotes e organização. Excelente para projetos profissionais.
    

---
