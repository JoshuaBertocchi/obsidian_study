
## **APOSTILA DE DOCKER** 

_Do zero ao deploy em produção_ com aplicação Python 

## **Conteúdo desta apostila** 

1. Conceitos Fundamentais  
2. Comandos Essenciais 
3. Exercícios Práticos  
4. Projeto Real com Python 
5. Diagramas e Referência Rápida 

_Nível: Iniciante ao Intermediário_ 

Apostila de Docker  —  Docker do Zero ao Deploy 

## **Módulo 1 — Conceitos Fundamentais** 

## **1.1  O que é Docker e para que ele serve?** 

Imagine que você desenvolveu um programa Python que funciona perfeitamente no seu computador. Mas quando você envia para um colega ou para um servidor, ele dá erro. O motivo? O ambiente é diferente: versão do Python, bibliotecas instaladas, sistema operacional... 

O Docker resolve exatamente esse problema. Ele permite que você empacote sua aplicação junto com todo o ambiente que ela precisa para funcionar — versão do Python, bibliotecas, configurações — dentro de uma espécie de 'caixinha' chamada container. 

## **📌 Resumo** 

O lema do Docker é: "Works on my machine? Ship the machine!" (Funciona na minha máquina? Manda a máquina!)  — e é literalmente isso que ele faz. 

Com Docker você consegue: 

- Garantir que sua aplicação rode igual em qualquer lugar 

- Isolar projetos diferentes sem conflitos de versão 

- Subir e derrubar ambientes rapidamente 

- Trabalhar em equipe sem o problema de "na minha máquina funciona" 

- Fazer deploy em servidores de forma previsível e controlada 

## **1.2  Docker vs. Máquina Virtual vs. Instalação Tradicional** 

Para entender Docker, é útil compará-lo com as alternativas que existiam antes: 

**==> picture [469 x 126] intentionally omitted <==**

**----- Start of picture text -----**<br>
╔══════════════════╦══════════════════════╦══════════════════════╗<br>║  INSTALAÇÃO      ║  MÁQUINA VIRTUAL     ║  DOCKER              ║<br>║  TRADICIONAL     ║  (VM)                ║  (Container)         ║<br>╠══════════════════╬══════════════════════╬══════════════════════╣<br>║ Instala direto   ║ Simula um PC inteiro ║ Compartilha o kernel ║<br>║ no sistema       ║ com SO próprio       ║ do sistema host      ║<br>║                  ║                      ║                      ║<br>║ Rápido, mas      ║ Pesada (GB de RAM)   ║ Leve (MB de RAM)     ║<br>║ gera conflitos   ║ Demora para iniciar  ║ Inicia em segundos   ║<br>║ entre versões    ║ Isolamento total     ║ Isolamento eficiente ║<br>╚══════════════════╩══════════════════════╩══════════════════════╝<br>**----- End of picture text -----**<br>


## **⚠️�  Atenção** 

Docker NÃO é uma máquina virtual. Uma VM emula um computador inteiro (inclusive o hardware). O Docker apenas isola processos, compartilhando o kernel do sistema operacional — por isso é muito mais leve e rápido. 

```
  MÁQUINA VIRTUAL                   DOCKER
  ─────────────────────             ───────────────────────────
```

Apostila de Docker  —  Docker do Zero ao Deploy 

```
  [ Sua App       ]                 [ Sua App   ][ Outra App ]
  [ SO convidado  ]                 [   Libs    ][   Libs    ]
  [ Hypervisor    ]                 [     Docker Engine      ]
  [ SO do Host    ]                 [    SO do Host (kernel) ]
  [ Hardware      ]                 [       Hardware         ]
```

## **1.3  Os 5 Conceitos Fundamentais do Docker** 

## **1.3.1  Dockerfile** 

É um arquivo de texto com instruções para construir uma imagem Docker. Pense nele como uma 'receita de bolo': você descreve passo a passo o que precisa instalar e configurar. 

```
# Exemplo simples de Dockerfile
FROM python:3.11-slim        # Começa com uma imagem base
WORKDIR /app                 # Define a pasta de trabalho
COPY . .                     # Copia seus arquivos
RUN pip install -r requirements.txt   # Instala dependências
CMD ["python", "app.py"]    # Comando para rodar a app
```

## **1.3.2  Imagem (Image)** 

É o resultado da 'receita' (Dockerfile). A imagem é estática — ela não muda. É como uma fotografia do ambiente pronto. Você pode compartilhar imagens no Docker Hub (repositório público, como o GitHub, mas para imagens Docker). 

## **1.3.3  Container** 

É uma imagem em execução. Quando você 'roda' uma imagem, ela vira um container — um processo isolado rodando no seu sistema. Você pode ter vários containers rodando a mesma imagem ao mesmo tempo. 

## **📌 Analogia** 

Analogia perfeita: • Dockerfile = receita de bolo • Imagem = bolo pronto (congelado) • Container = fatia do bolo servida no prato (em uso) 

## **1.3.4  Volume** 

Containers são temporários por natureza: quando você destrói um container, todos os dados dentro dele somem. Volumes resolvem isso — são como 'pastas compartilhadas' entre o container e o seu computador, onde os dados ficam salvos permanentemente. 

```
# Mapeia a pasta /dados do container para ./meus-dados no host
docker run -v ./meus-dados:/dados minha-imagem
```

Apostila de Docker  —  Docker do Zero ao Deploy 

## **1.3.5  Rede (Network)** 

Por padrão, containers são isolados. A rede Docker permite que containers se comuniquem entre si — por exemplo, um container com sua aplicação Python conversando com um container de banco de dados PostgreSQL. 

## **1.4  Como os Componentes se Relacionam** 

**==> picture [469 x 146] intentionally omitted <==**

**----- Start of picture text -----**<br>
  Você escreve                                           Aplicação<br>  ──────────                                            rodando!<br>                                                            ↑<br>  ┌─────────────┐   docker build   ┌──────────────┐  docker run  ┌───────────┐<br>  │  Dockerfile │ ──────────────  │    Imagem    │ ──────────── │ Container │ ▶ ▶<br>  └─────────────┘                  └──────────────┘               └───────────┘<br>       +                                  |                            |    |<br>  requirements.txt            docker push/pull                    Volume  Rede<br>                                          |<br>                                   ┌──────────────┐<br>                                   │  Docker Hub  │<br>                                   │  (Registry)  │<br>                                   └──────────────┘<br>**----- End of picture text -----**<br>


## O fluxo completo de trabalho com Docker é: 

1. Você escreve o Dockerfile (a receita) 

2. Executa docker build → Docker cria a Imagem 

3. Executa docker run → Docker cria e inicia o Container 

4. Sua aplicação está rodando, isolada e previsível 

5. (Opcional) Você envia a imagem para o Docker Hub com docker push 

6. Em outro computador/servidor, você faz docker pull + docker run 

Apostila de Docker  —  Docker do Zero ao Deploy 

## **Módulo 2 — Comandos Essenciais** 

## **2.1  Referência Visual Rápida** 

```
  CICLO DE VIDA DE UM CONTAINER
  ─────────────────────────────────────────────────────────────
  docker pull      →  Baixa uma imagem do Docker Hub
  docker build     →  Cria uma imagem a partir do Dockerfile
  docker run       →  Cria e inicia um container
  docker start     →  Inicia um container parado
  docker stop      →  Para um container em execução
  docker rm        →  Remove um container
  docker rmi       →  Remove uma imagem
```

## **2.2  Gerenciamento de Imagens** 

## **docker pull — Baixar uma imagem** 

Baixa uma imagem do Docker Hub (ou outro registry) para o seu computador. 

```
# Formato básico
docker pull <nome-da-imagem>:<tag>
# Exemplos reais
docker pull python:3.11-slim   # Imagem Python versão 3.11 (versão enxuta)
docker pull postgres:15        # Banco de dados PostgreSQL v15
docker pull nginx:latest       # Servidor web Nginx (versão mais recente)
docker pull ubuntu:22.04       # Sistema Ubuntu
```

## **📌 Dica** 

Se você não especificar a tag, o Docker baixa automaticamente a tag 'latest' (mais recente). Mas em produção, sempre especifique a versão exata para evitar surpresas! 

## **docker build — Construir uma imagem** 

Cria uma imagem Docker a partir de um Dockerfile. 

```
# Formato básico
docker build -t <nome>:<tag> <caminho-do-dockerfile>
```

```
# Exemplos reais
docker build -t minha-app:1.0 .       # Ponto (.) = pasta atual
docker build -t minha-app:latest .    # Tag 'latest'
docker build -t joao/projeto:v2 .     # Prefixo com seu usuário Docker Hub
docker build --no-cache -t app:1.0 . # Reconstrói do zero (sem cache)
```

Apostila de Docker  —  Docker do Zero ao Deploy 

## **docker images — Listar imagens** 

Mostra todas as imagens baixadas ou construídas no seu computador. 

```
docker images
# Saída esperada:
# REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
# minha-app     1.0       a1b2c3d4e5f6   2 hours ago    145MB
# python        3.11-slim f6e5d4c3b2a1   3 days ago     130MB
```

## **docker rmi — Remover imagem** 

```
docker rmi minha-app:1.0      # Remove pelo nome:tag
docker rmi a1b2c3d4e5f6       # Remove pelo ID
docker image prune            # Remove TODAS as imagens sem uso
```

## **2.3  Gerenciamento de Containers** 

## **docker run — O comando mais importante!** 

Cria e inicia um container a partir de uma imagem. Este é o comando que você mais vai usar. 

```
# Formato básico
docker run [opções] <imagem> [comando]
# Exemplos progressivos:
# 1. Mais simples possível
docker run hello-world
# 2. Modo interativo (você entra no terminal do container)
docker run -it ubuntu:22.04 bash
# 3. Em background (modo daemon, libera seu terminal)
docker run -d nginx
# 4. Com porta mapeada (host:container)
docker run -d -p 8080:80 nginx
# Agora acesse: http://localhost:8080
# 5. Com volume montado
docker run -d -p 5432:5432 -v ./dados:/var/lib/postgresql postgres:15
# 6. Com variáveis de ambiente
docker run -d -e POSTGRES_PASSWORD=senha123 postgres:15
```

Apostila de Docker  —  Docker do Zero ao Deploy 

```
# 7. Com nome personalizado
docker run -d --name meu-banco postgres:15
# 8. Completo (como em produção)
docker run -d \
  --name minha-app \
  -p 8000:8000 \
  -v ./logs:/app/logs \
  -e DEBUG=false \
  --restart unless-stopped \
  minha-app:1.0
```

**📌 Importante para produção** 

A flag --restart unless-stopped faz o container reiniciar automaticamente se o servidor reiniciar. Essencial em produção! 

## **docker ps — Ver containers em execução** 

```
docker ps            # Mostra apenas os containers RODANDO
docker ps -a         # Mostra TODOS (inclusive os parados)
docker ps -q         # Mostra apenas os IDs (útil em scripts)
# Saída do 'docker ps':
# CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS   PORTS   NAMES
# abc123def456   nginx     ...       1 min     Up 1m    80/tcp  meu-nginx
```

## **docker stop / start / restart** 

```
docker stop meu-container     # Para o container (graciosamente)
docker start meu-container    # Inicia um container parado
docker restart meu-container  # Para e reinicia
# Parar TODOS os containers em execução
docker stop $(docker ps -q)
```

## **docker rm — Remover container** 

```
docker rm meu-container       # Remove um container PARADO
docker rm -f meu-container    # Força a remoção (mesmo rodando)
docker container prune        # Remove TODOS os containers parados
```

## **docker logs — Ver logs do container** 

```
docker logs meu-container         # Mostra todos os logs
docker logs -f meu-container      # Fica exibindo em tempo real (follow)
docker logs --tail 50 meu-container  # Mostra as últimas 50 linhas
```

Apostila de Docker  —  Docker do Zero ao Deploy 

## **docker exec — Executar comandos dentro do container** 

```
# Abrir um terminal dentro do container (muito útil para debug!)
docker exec -it meu-container bash
```

```
docker exec -it meu-container sh     # Se bash não estiver disponível
```

```
# Executar um comando específico
docker exec meu-container python manage.py migrate
docker exec meu-container cat /app/config.py
```

## **2.4  Tabela de Referência Completa** 

|**Comando**|**O que faz**|**Quando usar**|
|---|---|---|
|`docker pull img`|Baixa imagem do registry|Antes de usar uma imagem nova|
|`docker build -t nome .`|Cria imagem do Dockerfile|Após alterar o Dockerfile ou código|
|`docker images`|Lista imagens locais|Para ver o que você tem baixado|
|`docker rmi nome`|Remove uma imagem|Para liberar espaço em disco|
|`docker run -d nome`|Cria e inicia container|Para subir uma aplicação|
|`docker run -it nome bash`|Entra no container|Para explorar ou debugar|
|`docker ps`|Lista containers ativos|Para ver o que está rodando|
|`docker ps -a`|Lista todos os containers|Para ver histórico completo|
|`docker stop nome`|Para o container|Para pausar sem apagar|
|`docker rm nome`|Remove o container|Para limpar containers parados|
|`docker logs -f nome`|Exibe logs ao vivo|Para monitorar a aplicação|
|`docker exec -it nome`<br>`bash`|Terminal no container|Para debugar problemas|
|`docker volume ls`|Lista os volumes|Para gerenciar persistência|
|`docker network ls`|Lista as redes|Para inspecionar conectividade|



Apostila de Docker  —  Docker do Zero ao Deploy 

## **Módulo 3 — Exercícios Práticos** 

Os exercícios a seguir são progressivos. Faça-os na ordem apresentada. Não pule etapas! 

## **📌 Pré-requisito** 

Antes de começar, verifique se o Docker está instalado: abra o terminal e execute 'docker --version'. Você deve ver algo como: Docker version 24.x.x 

## **Exercício 1 — Hello, Docker!** 🟢 **Iniciante** 

## **📌 Objetivo** 

Rodar seu primeiro container Docker e entender o ciclo básico de funcionamento. 

## **Passo a Passo** 

7. Abra o terminal do seu sistema operacional 

8. Execute o comando abaixo: 

```
docker run hello-world
```

9. Observe a saída no terminal. O Docker vai: 

   - Procurar a imagem 'hello-world' no seu computador 

   - Não encontrar (primeira execução) e baixar do Docker Hub 

   - Criar um container com essa imagem 

   - Executar o container (que imprime uma mensagem e termina) 

10. Agora rode: 

```
docker ps -a
```

11. Você verá o container com STATUS 'Exited'. Isso é normal — esse container faz sua tarefa e encerra. 

## **📌 Resultado esperado** 

Resultado esperado: uma mensagem começando com "Hello from Docker!" e uma explicação de como funcionou. Se aparecer isso, parabéns — o Docker está funcionando! 

🏆 **Desafio Extra** 

Desafio extra: Execute 'docker run hello-world' mais uma vez. Note que dessa vez é instantâneo — a imagem já está no seu computador. Execute 'docker images' para ver a imagem hello-world listada. 

## **Exercício 2 — Explorando um Container** 🟢 **Iniciante** 

## **📌 Objetivo** 

Entrar dentro de um container Linux e explorar seu ambiente isolado. 

Apostila de Docker  —  Docker do Zero ao Deploy 

## **Passo a Passo** 

12. Entre em um container Ubuntu interativo: 

```
docker run -it ubuntu:22.04 bash
```

13. Você agora está DENTRO do container! O prompt muda para algo como 'root@abc123:/# '. Explore: 

```
ls /                    # Veja a estrutura de pastas
cat /etc/os-release     # Confirme que é Ubuntu
pwd                     # Pasta atual
uname -a                # Versão do kernel
```

14. Crie um arquivo dentro do container: 

`echo 'Olá, Docker!' > /tmp/teste.txt cat /tmp/teste.txt` 15. Saia do container: `exit` 

16. O container parou. Liste-o: 

```
docker ps -a
```

17. Entre novamente no container (não crie um novo!): 

```
docker start -i <ID-DO-CONTAINER>
cat /tmp/teste.txt   # O arquivo ainda existe!
```

18. Agora REMOVA o container e crie um novo ubuntu. Tente acessar o arquivo: 

```
exit
docker rm <ID>
docker run -it ubuntu:22.04 bash
cat /tmp/teste.txt   # Arquivo não existe mais!
```

## **📌 Aprendizado** 

Resultado esperado: Você percebe que dados dentro do container são temporários. Quando o container é removido, os dados somem. É por isso que precisamos de volumes! 

🏆 **Desafio Extra** 

Desafio extra: Instale o 'curl' dentro do container (apt-get update && apt-get install -y curl) e faça uma requisição: curl https://httpbin.org/get. O container tem acesso à internet por padrão! 

## **Exercício 3 — Servidor Web com Porta** 🟡 **Básico** 

## **📌 Objetivo** 

Rodar um servidor Nginx e acessá-lo pelo navegador, entendendo o mapeamento de portas. 

## **Passo a Passo** 

## 19. Suba o Nginx em background: 

```
docker run -d --name meu-nginx -p 8080:80 nginx
```

20. Confirme que está rodando: 

```
docker ps
```

Apostila de Docker  —  Docker do Zero ao Deploy 

21. Abra o navegador e acesse: http://localhost:8080 

22. Você deve ver a página padrão do Nginx! Agora veja os logs: 

```
docker logs meu-nginx
```

```
docker logs -f meu-nginx  # Fique monitorando
```

23. Enquanto o logs -f está rodando, atualize a página no navegador várias vezes. Veja os logs aparecendo! 

24. Pressione Ctrl+C para parar o logs. Pare e remova o container: 

```
docker stop meu-nginx
```

```
docker rm meu-nginx
```

`MAPEAMENTO DE PORTAS ────────────────────────────────────────────── Seu computador          Container Nginx ┌──────────────┐        ┌──────────────────┐ │ localhost    │        │                  │ │ porta 8080   │──────│ porta 80 (nginx) │` ◀ ▶ `└──────────────┘        └──────────────────┘ flag: -p 8080:80 ↑     ↑ HOST  CONTAINER` 

🏆 **Desafio Extra** Desafio extra: Suba dois containers Nginx ao mesmo tempo, mas em portas diferentes: um na 8080 e outro na 8081. Acesse ambos no navegador! Dica: docker run -d -p 8081:80 --name nginx2 nginx 

## **Exercício 4 — Persistência com Volumes** 🟡 **Básico** 

## **📌 Objetivo** 

Usar volumes para persistir dados do banco de dados PostgreSQL entre containers. 

## **Passo a Passo** 

25. Crie uma pasta para os dados e suba o PostgreSQL: 

```
mkdir -p ~/docker-dados/postgres
docker run -d \
  --name meu-postgres \
  -e POSTGRES_PASSWORD=minhasenha \
  -e POSTGRES_DB=meubanco \
  -v ~/docker-dados/postgres:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres:15
```

26. Aguarde 5 segundos e conecte ao banco: 

```
docker exec -it meu-postgres psql -U postgres -d meubanco
```

27. Dentro do psql, crie uma tabela e insira dados: `CREATE TABLE usuarios (id SERIAL, nome TEXT); INSERT INTO usuarios (nome) VALUES ('Maria'), ('João'); SELECT * FROM usuarios;` 

Apostila de Docker  —  Docker do Zero ao Deploy 

```
\q
```

28. Destrua o container (sem destruir o volume!): 

```
docker stop meu-postgres
docker rm meu-postgres
```

29. Recrie o container com o MESMO volume: 

```
docker run -d \
  --name meu-postgres \
  -e POSTGRES_PASSWORD=minhasenha \
  -e POSTGRES_DB=meubanco \
  -v ~/docker-dados/postgres:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres:15
```

30. Conecte novamente e verifique os dados: `docker exec -it meu-postgres psql -U postgres -d meubanco SELECT * FROM usuarios;   -- Os dados ainda estão lá!` 

## **📌 Resultado esperado** 

Resultado esperado: Os dados da tabela persistiram! Isso acontece porque os dados ficam na pasta ~/docker-dados/postgres no seu computador, não dentro do container. 

🏆 **Desafio Extra** Desafio extra: Explore a pasta ~/docker-dados/postgres no seu computador. São os arquivos reais do PostgreSQL. Você pode até fazer backup copiando essa pasta! 

**Exercício 5 — Sua Primeira Imagem Customizada** 🟡 **Intermediário** 

## **📌 Objetivo** 

Criar seu próprio Dockerfile, construir uma imagem Python e rodar um script. 

## **Passo a Passo** 

31. Crie uma pasta para o projeto: `mkdir ~/primeiro-docker && cd ~/primeiro-docker` 32. Crie o arquivo app.py: `# Conteúdo de app.py: import platform print('=' * 40) print('  Olá do Docker!') print(f'  Python: {platform.python_version()}') print(f'  Sistema: {platform.system()}') print('=' * 40)` 33. Crie o Dockerfile (sem extensão!): `# Conteúdo do Dockerfile: FROM python:3.11-slim WORKDIR /app` 

Apostila de Docker  —  Docker do Zero ao Deploy 

`COPY app.py . CMD ["python", "app.py"]` 34. Construa a imagem: `docker build -t meu-primeiro-app:1.0 .` 35. Execute: `docker run meu-primeiro-app:1.0` 36. Veja sua imagem listada: `docker images` 

🏆 **Desafio Extra** Desafio extra: Modifique o app.py para receber um nome como variável de ambiente e exibir 'Olá, [NOME]!'. Use os.environ.get('NOME', 'Visitante') e rode com docker run -e NOME=Maria meuprimeiro-app:1.0 

Apostila de Docker  —  Docker do Zero ao Deploy 

## **Módulo 4 — Projeto Real com Python** 

Agora vamos criar um projeto Python completo e profissional usando Docker. Vamos construir uma API web com Flask, banco de dados PostgreSQL e tudo configurado com Docker Compose. 

## **4.1  O que é Docker Compose?** 

Docker Compose é uma ferramenta para definir e rodar múltiplos containers de uma vez só. Em vez de rodar vários docker run com dezenas de flags, você descreve tudo em um único arquivo YAML e sobe com um único comando. 

```
docker compose up    # Sobe todos os serviços
docker compose down  # Para e remove tudo
```

```
  SEM DOCKER COMPOSE                 COM DOCKER COMPOSE
  ──────────────────────             ───────────────────────────
  docker run postgres...             docker compose up
  docker run redis...                       ↓
  docker run app...                  Sobe tudo de uma vez!
  docker run nginx...                (postgres + app + nginx)
  (4 comandos enormes)
```

## **4.2  Estrutura do Projeto** 

Organize seu projeto assim: 

```
meu-projeto/
├── app/
│   ├── __init__.py
│   ├── main.py           # Código principal da aplicação
│   └── models.py         # Modelos do banco de dados
├── .env                  # Variáveis de ambiente (desenvolvimento)
├── .env.example          # Modelo de .env (vai para o Git!)
├── .gitignore            # NÃO commitar .env e outros
├── Dockerfile            # Como construir a imagem da app
├── docker-compose.yml    # Orquestração dos containers
├── requirements.txt      # Dependências Python
└── README.md             # Documentação do projeto
```

**⚠️�  Segurança** NUNCA adicione o arquivo .env ao Git! Ele contém senhas e chaves secretas. Adicione .env ao .gitignore e suba apenas o .env.example com valores fictícios como exemplo. 

## **4.3  Criando os Arquivos do Projeto** 

## **requirements.txt** 

Lista todas as dependências Python com versões fixas: 

Apostila de Docker  —  Docker do Zero ao Deploy 

```
flask==3.0.0
flask-sqlalchemy==3.1.1
psycopg2-binary==2.9.9
python-dotenv==1.0.0
gunicorn==21.2.0
```

## **📌 Boa Prática** 

Sempre fixe as versões no requirements.txt em produção. Isso garante que o ambiente seja sempre idêntico, independente de quando for feito o deploy. 

## **app/main.py** 

```
import os
from flask import Flask, jsonify
from flask_sqlalchemy import SQLAlchemy
app = Flask(__name__)
# Configuração do banco via variável de ambiente
app.config['SQLALCHEMY_DATABASE_URI'] = os.environ.get('DATABASE_URL')
db = SQLAlchemy(app)
class Produto(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    nome = db.Column(db.String(100), nullable=False)
    preco = db.Column(db.Float, nullable=False)
@app.route('/health')
def health():
    return jsonify({'status': 'ok', 'ambiente': os.environ.get('AMBIENTE')})
@app.route('/produtos')
def listar_produtos():
    produtos = Produto.query.all()
    return jsonify([{'id': p.id, 'nome': p.nome, 'preco': p.preco} for p in
produtos])
if __name__ == '__main__':
    with app.app_context():
        db.create_all()  # Cria as tabelas se não existirem
    app.run(host='0.0.0.0', port=5000)
```

## **Arquivo .env  (desenvolvimento local)** 

```
# Configurações do banco de dados
POSTGRES_USER=admin
POSTGRES_PASSWORD=senha_dev_123
POSTGRES_DB=meuprojeto
```

Apostila de Docker  —  Docker do Zero ao Deploy 

```
# URL de conexão (usada pela aplicação)
DATABASE_URL=postgresql://admin:senha_dev_123@db:5432/meuprojeto
```

```
# Configurações da aplicação
AMBIENTE=desenvolvimento
DEBUG=true
SECRET_KEY=chave-secreta-apenas-para-dev
```

## **Arquivo .env.example  (vai para o Git)** 

```
# Copie este arquivo para .env e preencha com seus valores
POSTGRES_USER=
POSTGRES_PASSWORD=
POSTGRES_DB=
DATABASE_URL=postgresql://USER:PASS@db:5432/DB
AMBIENTE=
DEBUG=
SECRET_KEY=
```

## **Dockerfile** 

```
# Imagem base: Python 3.11 versão enxuta
FROM python:3.11-slim
```

```
# Define variável de ambiente para não gerar arquivos .pyc
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
```

```
# Pasta de trabalho dentro do container
WORKDIR /app
# IMPORTANTE: copiar requirements ANTES do código
# Isso aproveita o cache do Docker — só reinstala libs se requirements mudar
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
```

```
# Agora copia o resto do código
COPY . .
# Cria usuário não-root para segurança
RUN adduser --disabled-password --gecos '' appuser
USER appuser
# Expõe a porta (documentação — não abre a porta sozinho)
EXPOSE 5000
```

Apostila de Docker  —  Docker do Zero ao Deploy 

```
# Comando de produção: Gunicorn (mais robusto que flask run)
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app.main:app"]
```

## **📌 Otimização de Cache** 

Copiar o requirements.txt ANTES do código-fonte é uma técnica importante! O Docker usa cache por camadas. Se você copiar tudo junto, qualquer mudança no código forçará a reinstalação de todas as libs — o que pode levar minutos. 

## **docker-compose.yml** 

```
version: '3.9'
services:
  # Serviço 1: Banco de dados PostgreSQL
  db:
    image: postgres:15-alpine
    env_file: .env                # Carrega variáveis do .env
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U $POSTGRES_USER"]
      interval: 5s
      timeout: 5s
      retries: 5
    restart: unless-stopped
  # Serviço 2: Nossa aplicação Python
  app:
    build: .                      # Constrói a partir do Dockerfile
    env_file: .env
    ports:
      - "5000:5000"
    depends_on:
      db:
        condition: service_healthy  # Espera o banco estar pronto!
    volumes:
      - ./app:/app/app            # Hot-reload em desenvolvimento
    restart: unless-stopped
# Volumes nomeados (gerenciados pelo Docker)
volumes:
  postgres_data:
```

**📌 Muito importante** 

O 'depends_on' com 'condition: service_healthy' garante que a aplicação só sobe DEPOIS que o banco de dados estiver pronto para aceitar conexões. Sem isso, a app pode tentar conectar antes do banco estar pronto e travar. 

Apostila de Docker  —  Docker do Zero ao Deploy 

## **4.4  Subindo o Projeto** 

```
# Entre na pasta do projeto
cd meu-projeto
# 1. Copie o .env.example e preencha
cp .env.example .env
# Edite o .env com suas configurações
# 2. Suba tudo (construindo a imagem se necessário)
docker compose up --build
# 3. Para subir em background (modo daemon)
docker compose up -d --build
# 4. Verificar o status
docker compose ps
# 5. Ver logs
docker compose logs -f
docker compose logs -f app   # Apenas logs da aplicação
# 6. Testar a API
curl http://localhost:5000/health
```

## **4.5  Como Atualizar a Aplicação** 

Quando você muda o código e quer fazer deploy da atualização: 

```
# 1. Faça suas alterações no código
```

```
# 2. Reconstrua a imagem com as mudanças
docker compose build app
# 3. Reinicie apenas o container da aplicação
docker compose up -d --no-deps app
# Alternativa: uma linha só
docker compose up -d --build
# 4. Verifique se subiu corretamente
docker compose ps
docker compose logs -f app
```

Apostila de Docker  —  Docker do Zero ao Deploy 

## **4.6  Deploy em Servidor (VPS/Cloud)** 

Para publicar sua aplicação em um servidor na nuvem (DigitalOcean, AWS, Hetzner, etc.): 

## **Passo 1 — Prepare o servidor** 

```
# No servidor (Ubuntu 22.04), instale o Docker
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
newgrp docker
# Verifique a instalação
docker --version
docker compose version
```

## **Passo 2 — Envie o código (sem o .env!)** 

```
# Opção A: via Git (recomendado)
git clone https://github.com/seu-usuario/seu-projeto.git
cd seu-projeto
# Opção B: via scp (cópia direta)
scp -r ./meu-projeto usuario@ip-do-servidor:/home/usuario/
```

## **Passo 3 — Configure as variáveis no servidor** 

```
# No servidor, crie o .env de PRODUÇÃO
cp .env.example .env
nano .env   # Edite com valores de produção
# Exemplo de .env em produção:
POSTGRES_USER=admin_prod
POSTGRES_PASSWORD=SenhaForte_Prod_789!
POSTGRES_DB=meuprojeto_prod
DATABASE_URL=postgresql://admin_prod:SenhaForte_Prod_789!@db:5432/
meuprojeto_prod
AMBIENTE=producao
DEBUG=false
SECRET_KEY=chave-super-secreta-gerada-aleatoriamente
```

## **Passo 4 — Suba em produção** 

```
docker compose up -d --build
```

```
# Verifique
docker compose ps
docker compose logs -f
```

Apostila de Docker  —  Docker do Zero ao Deploy 

## **4.7  Boas Práticas de Segurança** 

## 🔒 **Regras de Ouro** 

1. NUNCA suba o .env para o Git — use .gitignore 

2. Use usuário não-root no Dockerfile (USER appuser) 

3. Use imagens 'slim' ou 'alpine' — menos vulnerabilidades 

4. Sempre fixe versões no requirements.txt 

5. Nunca exponha portas desnecessárias (ex: banco de dados não precisa de -p em produção) 

6. Use secrets do Docker para dados muito sensíveis em produção 

7. Mantenha as imagens base atualizadas regularmente 

8. Não instale ferramentas de desenvolvimento na imagem de produção 

Apostila de Docker  —  Docker do Zero ao Deploy 

## **Módulo 5 — Diagramas e Referência Rápida** 

## **5.1  Fluxo Completo do Docker** 

`┌─────────────────────────────────────────────────────────┐ │                   FLUXO COMPLETO                       │ └─────────────────────────────────────────────────────────┘ Código Python        Dockerfile          requirements.txt │                    │                     │ └────────────────────┴─────────────────────┘ │ docker build │ ▼ ┌─────────────┐ │   IMAGEM    │  ── camadas sobrepostas` ◀ `│  (estática) │ └─────────────┘ │           │ docker run       docker push │           │ ▼           ▼ ┌─────────────┐  ┌──────────────┐ │  CONTAINER  │  │  Docker Hub  │ │  (rodando)  │  │  (registry)  │ └─────────────┘  └──────────────┘ │     │    │              │ Porta  Volume Rede       docker pull (acesso) (dados) (comunicação)` 

## **5.2  Arquitetura com Docker Compose** 

`┌─────────────────────────────────────────────────────────┐ │              docker-compose.yml                         │ │                                                         │ │  ┌──────────────┐      ┌──────────────────────┐        │ │  │  Serviço: db │      │  Serviço: app        │        │ │  │  postgres:15 │────│  python:3.11-slim    │        │` ◀ ▶ `│  │  porta interna│     │  porta 5000:5000     │─ HTTP │` ◀ `│  │  volume:data │      │  depende do db       │        │ │  └──────────────┘      └──────────────────────┘        │ │         │                          │                    │ │    postgres_data              ./app/app                 │ │    (volume Docker)          (bind mount)                │ └─────────────────────────────────────────────────────────┘` 

## **5.3  Como as Variáveis de Ambiente Fluem** 

```
  DESENVOLVIMENTO                    PRODUÇÃO
  ───────────────────                ─────────────────────────
  .env (local)                       .env (no servidor)
     │                                    │
     ▼                                    ▼
```

Apostila de Docker  —  Docker do Zero ao Deploy 

```
  docker-compose.yml               docker-compose.yml
  (env_file: .env)                 (env_file: .env)
     │                                    │
     ▼                                    ▼
  Container recebe                  Container recebe
  as variáveis                      as variáveis
     │                                    │
     ▼                                    ▼
  app.py lê com                     app.py lê com
  os.environ.get(...)               os.environ.get(...)
```

## **5.4  Comandos do Docker Compose** 

```
docker compose up            # Sobe todos os serviços (em primeiro plano)
docker compose up -d         # Em background
docker compose up --build    # Reconstrói imagens antes de subir
docker compose down          # Para e remove containers e redes
docker compose down -v       # Também remove volumes!
docker compose ps            # Lista status dos serviços
docker compose logs -f       # Logs de todos os serviços
docker compose logs -f app   # Logs de um serviço específico
docker compose exec app bash # Terminal dentro de um serviço
docker compose restart app   # Reinicia um serviço
docker compose build         # Reconstrói as imagens sem subir
docker compose pull          # Atualiza imagens base
docker compose stop          # Para sem remover os containers
```

## **5.5  Checklist de Deploy em Produção** 

- **📌 Antes de fazer deploy, verifique:** 

- O .env de produção tem senhas fortes e diferentes do desenvolvimento 

- O .env NÃO está no repositório Git (.gitignore configurado) 

- O Dockerfile usa usuário não-root (USER appuser) 

- DEBUG=false no ambiente de produção 

- As versões de todas as dependências estão fixadas 

- O healthcheck está configurado no docker-compose.yml 

- O restart: unless-stopped está em todos os serviços críticos 

- O banco de dados não expõe porta para fora (sem -p no serviço db) 

- Você testou o processo de build no ambiente de produção 

- Você sabe como reverter (rollback) em caso de problema 

## **5.6  Solução de Problemas Comuns** 

Apostila de Docker  —  Docker do Zero ao Deploy 

## **Container não sobe / sai imediatamente** 

```
# Veja os logs para entender o erro
docker compose logs app
docker logs meu-container
```

```
# Entre no container interativamente para debugar
docker run -it --entrypoint bash minha-imagem
```

## **'Port already in use' — Porta já em uso** 

```
# Descubra qual processo usa a porta (ex: 5000)
sudo lsof -i :5000
# Ou mude a porta no docker-compose.yml: '5001:5000'
```

## **Mudanças no código não aparecem** 

```
# Reconstrua a imagem
docker compose build app
docker compose up -d app
```

```
# Ou force a reconstrução sem cache
docker compose build --no-cache app
```

## **Limpeza geral do sistema** 

```
docker system prune          # Remove containers, redes e imagens não usadas
docker system prune -a       # Remove TUDO que não está em uso (cuidado!)
docker volume prune          # Remove volumes não usados
```

## **5.7  Espaço para Anotações** 

**Minhas anotações e dúvidas:** 

Apostila de Docker  —  Docker do Zero ao Deploy 

**==> picture [469 x 64] intentionally omitted <==**

## **📌  Bons estudos e bom coding!** 

_Gerado com Claude · Apostila de Docker_ 

Apostila de Docker  —  Docker do Zero ao Deploy 

