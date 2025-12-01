## Guia rápido: criação e uso do Poetry [[Gerenciamento de Ambiente|.]]

- Instalar o Poetry:
  - `pip install poetry`
  - ou seguir o instalador oficial: `https://python-poetry.org/docs/`

- Criar um novo projeto com Poetry:
  - `poetry new nome_do_projeto`

- Iniciar Poetry em um projeto existente:
  - `poetry init`

- Criar/gerenciar o ambiente virtual automaticamente:
  - `poetry install`
  - (Cria o `.venv` e instala dependências do `pyproject.toml`)

- Ver o caminho do ambiente virtual:
  - `poetry env info --path`

- Ativar o ambiente virtual:
  - `poetry shell`

- Executar comando dentro do ambiente sem ativar:
  - `poetry run python arquivo.py`
  - `poetry run comando`

- Adicionar dependências:
  - `poetry add nome-do-pacote`
  - `poetry add nome-do-pacote==1.2.3`

- Remover dependências:
  - `poetry remove nome-do-pacote`

- Atualizar dependências:
  - `poetry update`
  - `poetry update nome-do-pacote`

- Instalar dependências a partir do `pyproject.toml`:
  - `poetry install`

- Arquivos gerados automaticamente:
  - `pyproject.toml` → configurações do projeto e versões mínimas
  - `poetry.lock` → versões exatas instaladas

- Rodar scripts definidos no projeto:
  - `poetry run nome_do_script`

- Excluir o ambiente virtual gerenciado pelo Poetry:
  - `poetry env remove python`

- Ver dependências instaladas:
  - `poetry show`
