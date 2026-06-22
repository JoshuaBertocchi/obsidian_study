# 🐧 Apostila de Linux
## Administração e Uso Prático do Sistema Operacional

> **Nível:** Iniciante a Intermediário  
> **Pré-requisitos:** Familiaridade com `cd`, `ls`, `mkdir`, `cp`, `mv` e `rm`  
> **Objetivo:** Aprofundar conhecimentos em administração e uso profissional do Linux

---

## Sumário

1. [Gerenciamento de Privilégios e Usuários](#cap1)
2. [Gerenciamento de Serviços e Inicialização](#cap2)
3. [Rede e Conectividade](#cap3)
4. [Gerenciamento de Dispositivos e Hardware](#cap4)
5. [Processos e Monitoramento do Sistema](#cap5)
6. [Gerenciamento de Pacotes](#cap6)
7. [Sistema de Arquivos e Permissões](#cap7)
8. [Automação e Produtividade](#cap8)
9. [Tópicos Intermediários e Avançados](#cap9)

---

<a name="cap1"></a>
# Capítulo 1 — Gerenciamento de Privilégios e Usuários

## Introdução

No Linux, a segurança é baseada em um sistema de usuários e permissões. Existe sempre um usuário especial chamado **root**, que tem acesso total ao sistema. Para tarefas administrativas, você precisa de privilégios elevados — e é aí que entram os comandos deste capítulo.

> ⚠️ **Regra de ouro:** Nunca trabalhe como root o tempo todo. Use `sudo` apenas quando necessário.

---

## 1.1 `sudo` — Executar Comandos como Superusuário

### O que faz
Permite que um usuário comum execute um comando com privilégios de root (ou de outro usuário), sem precisar saber a senha do root.

### Sintaxe
```bash
sudo [opções] comando [argumentos]
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-u usuario` | Executa como outro usuário (não root) |
| `-i` | Abre um shell de login como root |
| `-s` | Abre um shell como root sem login |
| `-l` | Lista os comandos permitidos para o usuário |
| `-k` | Invalida o cache de autenticação (pede senha na próxima vez) |

### Exemplos Práticos

```bash
# Instalar um pacote (requer root)
sudo apt install htop

# Editar arquivo de sistema
sudo nano /etc/hosts

# Executar como outro usuário
sudo -u www-data ls /var/www

# Abrir shell root interativo
sudo -i

# Ver o que você pode fazer com sudo
sudo -l
```

### Cenários Reais de Uso

**Cenário 1:** Você precisa editar o arquivo `/etc/fstab` para adicionar uma partição:
```bash
sudo nano /etc/fstab
```

**Cenário 2:** Reiniciar um serviço de rede:
```bash
sudo systemctl restart NetworkManager
```

### Exercícios Propostos

1. Liste os arquivos de `/root` usando `sudo`.
2. Use `sudo -l` para verificar quais comandos você tem permissão de executar.
3. Crie um arquivo em `/tmp` e tente criá-lo em `/etc` sem `sudo`. Observe o erro.

### Erros Comuns e Soluções

| Erro | Causa | Solução |
|------|-------|---------|
| `username is not in the sudoers file` | Usuário não tem permissão de sudo | Adicione o usuário ao grupo `sudo` com `usermod -aG sudo username` (como root) |
| `sudo: command not found` | sudo não instalado | Instale com `apt install sudo` como root |
| Pede senha repetidamente | Cache expirou | Normal — padrão é 15 min. Use `sudo -v` para renovar |

---

## 1.2 `su` — Trocar de Usuário

### O que faz
Permite trocar para outro usuário durante a sessão atual. Diferente do `sudo`, ele requer a senha do usuário de destino.

### Sintaxe
```bash
su [opções] [usuario]
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-` ou `-l` | Simula um login completo (carrega o ambiente do usuário) |
| `-c "comando"` | Executa um comando como o usuário e volta |
| `-s /bin/bash` | Especifica o shell a usar |

### Exemplos Práticos

```bash
# Trocar para root (pede a senha do root)
su

# Trocar para root com ambiente completo
su -

# Trocar para outro usuário
su - joao

# Executar um único comando como root e voltar
su -c "cat /etc/shadow" root

# Trocar para usuário sem carregar ambiente
su joao
```

### Diferença entre `su` e `su -`

```
su          → Mantém as variáveis de ambiente atuais
su -        → Carrega o ambiente completo do usuário destino (recomendado)
```

### Cenários Reais de Uso

**Cenário:** Você está em um servidor sem `sudo` configurado e precisa de acesso root:
```bash
su -
# Digite a senha do root
# Agora você é root com ambiente completo
exit  # Para voltar ao usuário original
```

### Exercícios Propostos

1. Use `su -` para entrar como root, execute `whoami`, e saia com `exit`.
2. Compare `env` antes e depois de `su` vs `su -` e observe as diferenças.

### Erros Comuns e Soluções

| Erro | Causa | Solução |
|------|-------|---------|
| `Authentication failure` | Senha errada ou root bloqueado | Verifique a senha; em alguns sistemas, root é bloqueado por padrão |
| Shell diferente do esperado | Usuário usa outro shell | Use `-s /bin/bash` |

---

## 1.3 `passwd` — Alterar Senhas

### O que faz
Altera a senha de um usuário. Usuários comuns só podem alterar a própria senha; root pode alterar a de qualquer um.

### Sintaxe
```bash
passwd [opções] [usuario]
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-l` | Bloqueia (lock) a senha do usuário |
| `-u` | Desbloqueia (unlock) a senha |
| `-d` | Remove a senha (conta sem senha) |
| `-e` | Expira a senha (usuário deve trocar no próximo login) |
| `-S` | Mostra o status da senha |

### Exemplos Práticos

```bash
# Mudar sua própria senha
passwd

# Mudar a senha de outro usuário (como root)
sudo passwd joao

# Bloquear conta de um usuário
sudo passwd -l joao

# Verificar status da senha
sudo passwd -S joao

# Forçar troca de senha no próximo login
sudo passwd -e joao
```

### Exercícios Propostos

1. Altere sua própria senha com `passwd`.
2. Crie um usuário de teste e expire a senha dele com `passwd -e`.

---

## 1.4 `groups` — Ver Grupos de um Usuário

### O que faz
Exibe os grupos aos quais um usuário pertence.

### Sintaxe
```bash
groups [usuario]
```

### Exemplos Práticos

```bash
# Ver seus próprios grupos
groups

# Ver grupos de outro usuário
groups joao

# Outra forma: ver o arquivo /etc/group
cat /etc/group | grep joao
```

### Saída típica
```
joao : joao sudo audio video plugdev
```
Isso significa que `joao` pertence aos grupos: `joao` (primário), `sudo`, `audio`, `video` e `plugdev`.

---

## 1.5 `usermod` — Modificar Usuários Existentes

### O que faz
Modifica as configurações de um usuário já existente no sistema.

### Sintaxe
```bash
sudo usermod [opções] usuario
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-aG grupo` | Adiciona o usuário a um grupo (sem remover dos outros) |
| `-g grupo` | Muda o grupo primário |
| `-d /novo/home` | Muda o diretório home |
| `-m` | Move o conteúdo do home antigo para o novo |
| `-l novo_nome` | Renomeia o usuário |
| `-s /bin/bash` | Muda o shell padrão |
| `-L` | Bloqueia a conta |
| `-U` | Desbloqueia a conta |

### Exemplos Práticos

```bash
# Adicionar usuário ao grupo sudo (dar poderes administrativos)
sudo usermod -aG sudo joao

# Adicionar ao grupo docker
sudo usermod -aG docker joao

# Mudar o shell padrão para zsh
sudo usermod -s /bin/zsh joao

# Renomear usuário
sudo usermod -l joao_novo joao

# Bloquear conta
sudo usermod -L joao
```

> ⚠️ **IMPORTANTE:** Sempre use `-aG` (com o `a` de append/adicionar). Se usar apenas `-G`, o usuário será REMOVIDO de todos os outros grupos!

### Cenários Reais de Uso

**Cenário:** Novo desenvolvedor na equipe precisa usar Docker:
```bash
sudo usermod -aG docker novo_dev
# O usuário deve fazer logout e login novamente para as mudanças surtirem efeito
```

### Exercícios Propostos

1. Adicione seu usuário ao grupo `audio` usando `usermod -aG`.
2. Verifique com `groups` se a mudança foi aplicada (após novo login).

---

## 1.6 `useradd` — Criar Novos Usuários

### O que faz
Cria um novo usuário no sistema.

### Sintaxe
```bash
sudo useradd [opções] nome_usuario
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-m` | Cria o diretório home |
| `-d /caminho` | Define o caminho do home |
| `-s /bin/bash` | Define o shell padrão |
| `-g grupo` | Define o grupo primário |
| `-G grupo1,grupo2` | Define grupos secundários |
| `-c "comentário"` | Adiciona comentário/nome completo |
| `-e data` | Data de expiração (AAAA-MM-DD) |

### Exemplos Práticos

```bash
# Criar usuário básico (sem home)
sudo useradd joao

# Criar usuário completo (forma recomendada)
sudo useradd -m -s /bin/bash -c "João Silva" joao

# Criar usuário com grupos
sudo useradd -m -s /bin/bash -G sudo,docker -c "Admin User" admin_user

# Definir senha logo após criar
sudo passwd joao
```

> 💡 **Dica:** No Ubuntu/Debian, prefira `adduser` (versão interativa e amigável de `useradd`):
> ```bash
> sudo adduser joao
> ```

### Exercícios Propostos

1. Crie um usuário `teste` com home em `/home/teste` e shell bash.
2. Defina uma senha para ele.
3. Faça login como esse usuário com `su - teste`.
4. Delete o usuário ao final: `sudo userdel -r teste`.

---

## 1.7 `groupadd` — Criar Grupos

### O que faz
Cria um novo grupo de usuários no sistema.

### Sintaxe
```bash
sudo groupadd [opções] nome_grupo
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-g GID` | Define um ID numérico específico para o grupo |
| `-r` | Cria um grupo de sistema (GID < 1000) |

### Exemplos Práticos

```bash
# Criar grupo para a equipe de desenvolvimento
sudo groupadd desenvolvedores

# Criar grupo com GID específico
sudo groupadd -g 1500 projetos

# Criar grupo de sistema
sudo groupadd -r aplicacao

# Adicionar usuários ao grupo criado
sudo usermod -aG desenvolvedores joao
sudo usermod -aG desenvolvedores maria

# Ver grupos do sistema
cat /etc/group | grep desenvolvedores
```

### Exercícios Propostos

1. Crie um grupo chamado `estagiarios`.
2. Adicione dois usuários a esse grupo.
3. Use `getent group estagiarios` para verificar os membros.

---

## Resumo do Capítulo 1

| Comando | Uso principal |
|---------|---------------|
| `sudo comando` | Executar com privilégios de root |
| `su - usuario` | Trocar de usuário |
| `passwd usuario` | Alterar senha |
| `groups usuario` | Ver grupos de um usuário |
| `usermod -aG grupo usuario` | Adicionar usuário a grupo |
| `useradd -m -s /bin/bash usuario` | Criar usuário |
| `groupadd grupo` | Criar grupo |

---

<a name="cap2"></a>
# Capítulo 2 — Gerenciamento de Serviços e Inicialização

## Introdução

No Linux moderno, o **systemd** é o sistema de inicialização padrão na maioria das distribuições (Ubuntu, Fedora, Debian, Arch, etc.). Ele gerencia serviços, processos de boot e logs do sistema. Entender o systemd é essencial para qualquer administrador de sistemas.

---

## 2.1 `systemctl` — Controlar o systemd

### O que faz
É o comando principal para interagir com o systemd: iniciar, parar, reiniciar, habilitar e monitorar serviços.

### Sintaxe
```bash
systemctl [subcomando] [nome_do_servico]
```

### Subcomandos Principais

| Subcomando | Descrição |
|------------|-----------|
| `start` | Inicia um serviço |
| `stop` | Para um serviço |
| `restart` | Para e reinicia um serviço |
| `reload` | Recarrega configuração sem parar |
| `enable` | Habilita na inicialização do sistema |
| `disable` | Desabilita na inicialização |
| `status` | Mostra o estado atual |
| `is-active` | Verifica se está rodando |
| `is-enabled` | Verifica se está habilitado no boot |
| `list-units` | Lista todos os serviços |
| `daemon-reload` | Recarrega configurações do systemd |

### Exemplos Práticos

```bash
# Ver status do serviço SSH
sudo systemctl status ssh

# Iniciar o serviço de impressão
sudo systemctl start cups

# Parar o nginx
sudo systemctl stop nginx

# Reiniciar o Apache
sudo systemctl restart apache2

# Recarregar configuração do nginx sem downtime
sudo systemctl reload nginx

# Habilitar serviço para iniciar com o sistema
sudo systemctl enable ssh

# Desabilitar serviço no boot
sudo systemctl disable bluetooth

# Habilitar E iniciar ao mesmo tempo
sudo systemctl enable --now nginx

# Ver todos os serviços e seus status
systemctl list-units --type=service

# Ver apenas os que falharam
systemctl list-units --failed
```

### Exemplo de Saída do `status`

```
● nginx.service - A high performance web server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2024-01-15 10:30:00 UTC; 2h ago
       Docs: man:nginx(8)
   Main PID: 1234 (nginx)
      Tasks: 2 (limit: 4915)
     Memory: 5.8M
        CPU: 120ms
     CGroup: /system.slice/nginx.service
             ├─1234 nginx: master process
             └─1235 nginx: worker process
```

### Cenários Reais de Uso

**Cenário 1:** Você modificou o `/etc/nginx/nginx.conf` e precisa aplicar as mudanças:
```bash
sudo nginx -t               # Verificar se a config é válida
sudo systemctl reload nginx # Aplicar sem interromper conexões
```

**Cenário 2:** Investigar por que o serviço falhou na inicialização:
```bash
sudo systemctl status mysql
sudo journalctl -u mysql --no-pager | tail -50
```

### Exercícios Propostos

1. Verifique o status do serviço SSH em sua máquina.
2. Habilite o serviço `cron` para iniciar no boot.
3. Liste todos os serviços que falharam com `systemctl list-units --failed`.

---

## 2.2 `journalctl` — Analisar Logs do Sistema

### O que faz
Acessa e filtra os logs gerados pelo systemd (journald). É a ferramenta central para diagnóstico de problemas.

### Sintaxe
```bash
journalctl [opções]
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-u servico` | Logs de um serviço específico |
| `-f` | Segue os logs em tempo real (como `tail -f`) |
| `-n N` | Mostra as últimas N linhas |
| `-b` | Logs do boot atual |
| `-b -1` | Logs do boot anterior |
| `--since "data"` | Logs a partir de uma data |
| `--until "data"` | Logs até uma data |
| `-p err` | Filtra por prioridade (err, warning, info, debug) |
| `-e` | Vai ao final dos logs |
| `--no-pager` | Imprime direto sem paginar |

### Exemplos Práticos

```bash
# Ver todos os logs do sistema (use q para sair)
sudo journalctl

# Logs do serviço nginx
sudo journalctl -u nginx

# Acompanhar logs do nginx em tempo real
sudo journalctl -u nginx -f

# Últimas 100 linhas do SSH
sudo journalctl -u ssh -n 100

# Logs desde o último boot
sudo journalctl -b

# Logs de erros desde ontem
sudo journalctl --since "yesterday" -p err

# Logs em um intervalo de tempo
sudo journalctl --since "2024-01-15 08:00" --until "2024-01-15 10:00"

# Ver erros do kernel
sudo journalctl -k -p err

# Verificar uso do disco pelo journal
sudo journalctl --disk-usage
```

### Cenários Reais de Uso

**Cenário:** O site caiu às 3h da manhã. Como investigar?
```bash
# Ver logs do nginx nesse período
sudo journalctl -u nginx --since "03:00" --until "04:00"

# Ver erros gerais do sistema nesse período
sudo journalctl --since "03:00" --until "04:00" -p err

# Ver o que aconteceu durante o boot (se houve reinicialização)
sudo journalctl -b -1
```

### Exercícios Propostos

1. Use `journalctl -b` para ver os logs do boot atual.
2. Filtre os logs para mostrar apenas erros com `-p err`.
3. Monitore os logs do serviço SSH em tempo real com `-f` e tente fazer login em outro terminal.

---

## 2.3 `service` — Compatibilidade com init.d

### O que faz
Comando mais antigo para gerenciar serviços, compatível com sistemas que usam SysV init. Em sistemas com systemd, ele redireciona chamadas para o `systemctl`.

### Sintaxe
```bash
sudo service nome_servico {start|stop|restart|status|reload}
```

### Exemplos Práticos

```bash
sudo service nginx start
sudo service nginx stop
sudo service nginx restart
sudo service nginx status
```

> 💡 **Nota:** Em sistemas modernos com systemd, prefira `systemctl`. O `service` existe por compatibilidade.

---

## Tabela: Iniciar vs Habilitar

| Ação | Efeito imediato | Persiste no boot |
|------|-----------------|------------------|
| `systemctl start` | ✅ Sim | ❌ Não |
| `systemctl enable` | ❌ Não | ✅ Sim |
| `systemctl enable --now` | ✅ Sim | ✅ Sim |

---

## Resumo do Capítulo 2

```bash
# Fluxo típico de gerenciamento de serviço
sudo systemctl status nginx       # Verificar estado
sudo systemctl start nginx        # Iniciar
sudo systemctl enable --now nginx # Iniciar e habilitar no boot
sudo systemctl reload nginx       # Recarregar config (sem downtime)
sudo journalctl -u nginx -f       # Acompanhar logs em tempo real
```

---

<a name="cap3"></a>
# Capítulo 3 — Rede e Conectividade

## Introdução

Gerenciar redes pelo terminal é uma habilidade essencial no Linux — seja para configurar conexões, diagnosticar problemas ou monitorar tráfego. Este capítulo cobre as ferramentas mais utilizadas.

---

## 3.1 `nmcli` — Gerenciar Redes com NetworkManager

### O que faz
Interface de linha de comando para o NetworkManager. Permite gerenciar conexões de rede, Wi-Fi, VPN e ethernet sem interface gráfica.

### Sintaxe
```bash
nmcli [opções] {device|connection|networking|radio} [subcomando]
```

### Exemplos Práticos

```bash
# Ver status geral da rede
nmcli general status

# Listar dispositivos de rede
nmcli device status

# Ver redes Wi-Fi disponíveis
nmcli device wifi list

# Conectar ao Wi-Fi
nmcli device wifi connect "Nome_da_Rede" password "sua_senha"

# Ver conexões salvas
nmcli connection show

# Desconectar de uma rede
nmcli device disconnect wlan0

# Reconectar
nmcli device connect wlan0

# Criar conexão ethernet estática
nmcli connection add type ethernet con-name "eth-static" ifname eth0 \
  ipv4.addresses 192.168.1.100/24 \
  ipv4.gateway 192.168.1.1 \
  ipv4.dns "8.8.8.8 8.8.4.4" \
  ipv4.method manual

# Ativar a conexão
nmcli connection up "eth-static"

# Deletar uma conexão salva
nmcli connection delete "nome_conexao"
```

### Cenários Reais de Uso

**Cenário:** Configurar Wi-Fi em um servidor sem interface gráfica:
```bash
nmcli device wifi list                           # Ver redes disponíveis
nmcli device wifi connect "RedeEmpresa" password "senha123"
nmcli general status                             # Confirmar conexão
```

### Exercícios Propostos

1. Liste as redes Wi-Fi disponíveis com `nmcli device wifi list`.
2. Verifique o status dos dispositivos de rede com `nmcli device status`.
3. Veja as conexões salvas com `nmcli connection show`.

---

## 3.2 `ip` — Configurar Interfaces de Rede

### O que faz
Ferramenta moderna para configurar interfaces de rede, rotas e endereços IP. Substitui o antigo `ifconfig`.

### Sintaxe
```bash
ip [opções] {link|addr|route|neigh} [subcomando]
```

### Exemplos Práticos

```bash
# Ver todas as interfaces e seus IPs
ip addr show
# Atalho
ip a

# Ver apenas IPv4
ip -4 addr

# Ver informações de uma interface específica
ip addr show eth0

# Adicionar IP temporário a uma interface
sudo ip addr add 192.168.1.100/24 dev eth0

# Remover IP de uma interface
sudo ip addr del 192.168.1.100/24 dev eth0

# Ativar/desativar interface
sudo ip link set eth0 up
sudo ip link set eth0 down

# Ver tabela de roteamento
ip route show
# Atalho
ip r

# Adicionar rota padrão (gateway)
sudo ip route add default via 192.168.1.1

# Adicionar rota específica
sudo ip route add 10.0.0.0/8 via 192.168.1.254

# Ver cache ARP (tabela de vizinhos)
ip neigh show
```

### Dica: Descobrir seu IP

```bash
# IP local (LAN)
ip addr show | grep "inet " | grep -v "127.0.0.1"

# IP público (Internet)
curl ifconfig.me
# ou
curl ipinfo.io/ip
```

---

## 3.3 `ping` — Testar Conectividade

### O que faz
Envia pacotes ICMP para um host e mede a latência da resposta. Usado para testar se um host está acessível.

### Sintaxe
```bash
ping [opções] destino
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-c N` | Envia apenas N pacotes |
| `-i segundos` | Intervalo entre pacotes |
| `-t TTL` | Define o Time To Live |
| `-s tamanho` | Tamanho do pacote em bytes |
| `-W segundos` | Timeout por pacote |

### Exemplos Práticos

```bash
# Ping básico (Ctrl+C para parar)
ping google.com

# Enviar apenas 4 pacotes
ping -c 4 google.com

# Testar conectividade local
ping -c 2 192.168.1.1

# Testar DNS (se resolver o nome, o DNS funciona)
ping -c 2 www.google.com

# Ping com intervalo de 0.5 segundos
ping -i 0.5 -c 10 8.8.8.8
```

### Diagnóstico com ping

```bash
# 1. Testar interface local
ping -c 2 127.0.0.1        # Se falhar: problema no stack de rede

# 2. Testar gateway
ping -c 2 192.168.1.1      # Se falhar: problema na rede local

# 3. Testar DNS externo por IP
ping -c 2 8.8.8.8          # Se falhar: sem acesso à Internet

# 4. Testar resolução de DNS
ping -c 2 google.com        # Se falhar: problema de DNS
```

---

## 3.4 `ss` — Monitorar Conexões de Rede (Socket Statistics)

### O que faz
Mostra informações sobre sockets de rede. Substitui o antigo `netstat`.

### Sintaxe
```bash
ss [opções]
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-t` | Conexões TCP |
| `-u` | Conexões UDP |
| `-l` | Apenas sockets em escuta (listening) |
| `-n` | Não resolver nomes (mais rápido) |
| `-p` | Mostra o processo que usa o socket |
| `-a` | Todos os sockets |

### Exemplos Práticos

```bash
# Ver todas as conexões TCP
ss -t

# Ver portas em escuta
ss -tlnp

# Ver quem está usando a porta 80
ss -tlnp | grep :80

# Ver todas as conexões estabelecidas
ss -tn state established

# Ver conexões UDP
ss -ulnp

# Ver conexões de um processo específico
ss -tp | grep nginx
```

### Saída típica de `ss -tlnp`
```
State   Recv-Q  Send-Q  Local Address:Port  Peer Address:Port  Process
LISTEN  0       128     0.0.0.0:22          0.0.0.0:*          users:(("sshd",pid=1234))
LISTEN  0       511     0.0.0.0:80          0.0.0.0:*          users:(("nginx",pid=5678))
```

---

## 3.5 `curl` — Transferir Dados pela Web

### O que faz
Faz requisições HTTP, HTTPS, FTP e outros protocolos. Extremamente versátil para APIs, downloads e testes.

### Sintaxe
```bash
curl [opções] URL
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-o arquivo` | Salva a saída em arquivo |
| `-O` | Salva com o nome original do arquivo |
| `-L` | Segue redirecionamentos |
| `-I` | Mostra apenas cabeçalhos HTTP |
| `-X MÉTODO` | Define o método HTTP (GET, POST, etc.) |
| `-H "Header"` | Adiciona um cabeçalho |
| `-d "dados"` | Envia dados (POST) |
| `-u user:pass` | Autenticação básica |
| `-k` | Ignora erros de SSL |
| `-v` | Modo verbose (detalhado) |
| `-s` | Modo silencioso (sem progresso) |

### Exemplos Práticos

```bash
# Fazer uma requisição GET simples
curl https://api.exemplo.com/dados

# Baixar um arquivo
curl -O https://exemplo.com/arquivo.zip

# Salvar com nome específico
curl -o meu_arquivo.html https://exemplo.com

# Ver apenas os headers HTTP
curl -I https://www.google.com

# Fazer POST com JSON
curl -X POST https://api.exemplo.com/usuarios \
  -H "Content-Type: application/json" \
  -d '{"nome": "João", "email": "joao@email.com"}'

# POST com autenticação Bearer token
curl -H "Authorization: Bearer meu_token" \
  https://api.exemplo.com/protegido

# Descobrir seu IP público
curl ifconfig.me

# Testar resposta de uma API REST
curl -s https://api.github.com/users/torvalds | python3 -m json.tool

# Seguir redirecionamentos
curl -L http://bit.ly/algum-link
```

---

## 3.6 `wget` — Baixar Arquivos

### O que faz
Baixa arquivos da web. Mais simples que o `curl` para downloads, com suporte a downloads recursivos.

### Sintaxe
```bash
wget [opções] URL
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-O arquivo` | Salva com nome específico |
| `-c` | Continua download interrompido |
| `-q` | Modo silencioso |
| `-r` | Download recursivo |
| `-np` | Não sobe para o diretório pai (com -r) |
| `--limit-rate=TAXA` | Limita velocidade de download |
| `-P /diretorio` | Define diretório de destino |

### Exemplos Práticos

```bash
# Baixar um arquivo
wget https://exemplo.com/arquivo.zip

# Salvar com nome específico
wget -O ubuntu.iso https://releases.ubuntu.com/22.04/ubuntu-22.04.iso

# Continuar download interrompido
wget -c https://exemplo.com/arquivo-grande.iso

# Baixar para diretório específico
wget -P /tmp https://exemplo.com/script.sh

# Download silencioso (útil em scripts)
wget -q https://exemplo.com/config.txt

# Limitar velocidade (para não sobrecarregar a rede)
wget --limit-rate=500k https://exemplo.com/grande.zip
```

---

## Resumo do Capítulo 3

```bash
# Diagnóstico de rede passo a passo
ip a                              # Ver interfaces e IPs
ping -c 2 192.168.1.1             # Testar gateway
ping -c 2 8.8.8.8                 # Testar Internet (por IP)
ping -c 2 google.com              # Testar DNS
ss -tlnp                          # Ver portas abertas
curl ifconfig.me                  # Ver IP público
```

---

<a name="cap4"></a>
# Capítulo 4 — Gerenciamento de Dispositivos e Hardware

## Introdução

O Linux oferece ferramentas robustas para identificar e gerenciar hardware. Saber montar discos, identificar dispositivos e configurar impressoras pelo terminal é fundamental para administração de sistemas.

---

## 4.1 `lsblk` — Listar Dispositivos de Bloco

### O que faz
Exibe todos os dispositivos de bloco (discos, partições, SSDs, pendrives) em formato de árvore.

### Sintaxe
```bash
lsblk [opções]
```

### Exemplos Práticos

```bash
# Listar todos os discos e partições
lsblk

# Com informações de sistema de arquivos
lsblk -f

# Saída mais detalhada
lsblk -o NAME,SIZE,TYPE,MOUNTPOINT,FSTYPE,UUID

# Ver apenas discos (sem partições)
lsblk -d
```

### Saída típica

```
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0  500G  0 disk
├─sda1   8:1    0  512M  0 part /boot/efi
├─sda2   8:2    0    1G  0 part /boot
└─sda3   8:3    0  498G  0 part /
sdb      8:16   1   16G  0 disk
└─sdb1   8:17   1   16G  0 part /media/usb
```

---

## 4.2 `mount` e `umount` — Montar e Desmontar Dispositivos

### O que fazem
`mount` conecta um sistema de arquivos a um ponto da árvore de diretórios. `umount` desfaz essa conexão.

### Sintaxe
```bash
sudo mount [opções] dispositivo ponto_de_montagem
sudo umount ponto_de_montagem
```

### Exemplos Práticos

```bash
# Criar ponto de montagem
sudo mkdir -p /mnt/pendrive

# Montar pendrive (identificar com lsblk primeiro)
sudo mount /dev/sdb1 /mnt/pendrive

# Montar com sistema de arquivos específico
sudo mount -t ntfs /dev/sdb1 /mnt/pendrive

# Montar ISO
sudo mount -o loop arquivo.iso /mnt/iso

# Montar com opções (somente leitura)
sudo mount -o ro /dev/sdb1 /mnt/pendrive

# Ver o que está montado
mount | grep /mnt
# ou
df -h

# Desmontar
sudo umount /mnt/pendrive

# Se estiver ocupado, forçar (use com cuidado)
sudo umount -f /mnt/pendrive
# ou aguardar processos terminarem
sudo lsof /mnt/pendrive   # Ver quem está usando
```

### Montagem Permanente com `/etc/fstab`

Para montar automaticamente no boot, edite `/etc/fstab`:
```bash
# Formato: dispositivo  ponto  tipo  opções  dump  pass
UUID=abc123...  /mnt/dados  ext4  defaults  0  2
```

Use UUID (não `/dev/sdb`) para evitar problemas quando a ordem dos discos muda:
```bash
# Obter UUID
lsblk -f
# ou
blkid /dev/sdb1
```

---

## 4.3 `fdisk` — Gerenciar Partições

### O que faz
Cria, deleta e modifica partições em discos. **Use com extremo cuidado** — operações erradas podem causar perda de dados.

### Sintaxe
```bash
sudo fdisk [opções] dispositivo
```

### Exemplos Práticos

```bash
# Listar partições de todos os discos
sudo fdisk -l

# Listar partições de um disco específico
sudo fdisk -l /dev/sdb

# Entrar no modo interativo para editar partições
sudo fdisk /dev/sdb
# Comandos internos:
# m → menu de ajuda
# p → listar partições
# n → nova partição
# d → deletar partição
# w → salvar e sair
# q → sair sem salvar
```

> ⚠️ **CUIDADO:** Toda operação em `fdisk` só é salva quando você digita `w`. Digite `q` para sair sem fazer alterações. Faça backup antes de modificar partições!

---

## 4.4 `lspci` e `lsusb` — Listar Hardware

### `lspci` — Dispositivos PCI

```bash
# Listar todos os dispositivos PCI
lspci

# Com detalhes do driver
lspci -k

# Filtrar por tipo (ex: rede)
lspci | grep -i network

# Ver placas de vídeo
lspci | grep -i vga

# Versão detalhada
lspci -v
```

### `lsusb` — Dispositivos USB

```bash
# Listar dispositivos USB
lsusb

# Com árvore
lsusb -t

# Com detalhes
lsusb -v

# Monitorar conexão/desconexão USB em tempo real
watch -n 1 lsusb
```

---

## 4.5 `dmesg` — Mensagens do Kernel

### O que faz
Exibe o buffer de mensagens do kernel. Essencial para diagnosticar problemas de hardware.

### Sintaxe
```bash
dmesg [opções]
```

### Exemplos Práticos

```bash
# Ver todas as mensagens do kernel
dmesg

# Ver com paginação
dmesg | less

# Acompanhar em tempo real
dmesg -w

# Filtrar erros
dmesg -l err

# Ver mensagens sobre USB (quando conecta um pendrive)
dmesg | grep -i usb

# Ver mensagens recentes sobre disco
dmesg | tail -20

# Limpar buffer (como root)
sudo dmesg -C
```

### Cenário: Diagnosticar pendrive não reconhecido

```bash
# Conecte o pendrive e execute:
dmesg | tail -20
# Procure por mensagens como:
# [12345.678] usb 2-1: new high-speed USB device
# [12345.890] sdb: sdb1
```

---

## 4.6 Gerenciar Impressoras com CUPS

O CUPS (Common Unix Printing System) é o sistema de impressão padrão no Linux.

### Instalar CUPS

```bash
# Ubuntu/Debian
sudo apt install cups

# Fedora
sudo dnf install cups

# Iniciar e habilitar
sudo systemctl enable --now cups
```

### Comandos de Impressão

```bash
# Listar impressoras configuradas
lpstat -p

# Ver impressora padrão
lpstat -d

# Imprimir arquivo
lp arquivo.pdf

# Imprimir em impressora específica
lp -d nome_impressora arquivo.pdf

# Imprimir várias cópias
lp -n 3 arquivo.pdf

# Ver fila de impressão
lpq

# Cancelar trabalho de impressão
lprm ID_DO_TRABALHO

# Cancelar todos os trabalhos
lprm -
```

### Adicionar Impressora via Interface Web

```bash
# Habilitar acesso externo ao CUPS
sudo cupsctl --remote-admin
# Acesse: http://localhost:631
```

---

## Resumo do Capítulo 4

```bash
lsblk -f                          # Ver discos e partições
sudo mount /dev/sdb1 /mnt/usb     # Montar pendrive
sudo umount /mnt/usb              # Desmontar pendrive
lspci | grep -i network           # Ver placa de rede
lsusb                             # Ver dispositivos USB
dmesg | tail -20                  # Mensagens recentes do kernel
sudo fdisk -l                     # Listar partições
```

---

<a name="cap5"></a>
# Capítulo 5 — Processos e Monitoramento do Sistema

## Introdução

Entender e gerenciar processos é fundamental para manter o sistema saudável. Neste capítulo você aprenderá a monitorar recursos, identificar gargalos e controlar processos problemáticos.

---

## 5.1 `ps` — Listar Processos

### O que faz
Mostra um snapshot dos processos em execução no momento.

### Sintaxe
```bash
ps [opções]
```

### Exemplos Práticos

```bash
# Processos do usuário atual
ps

# Todos os processos do sistema (formato completo)
ps aux

# Formato hierárquico (árvore de processos)
ps auxf

# Filtrar por nome
ps aux | grep nginx

# Ordenar por uso de CPU
ps aux --sort=-%cpu | head -10

# Ordenar por uso de memória
ps aux --sort=-%mem | head -10

# Ver processos de um usuário específico
ps -u joao

# Formato customizado
ps -eo pid,ppid,user,cmd,%cpu,%mem --sort=-%cpu
```

### Significado das Colunas em `ps aux`

| Coluna | Descrição |
|--------|-----------|
| `USER` | Dono do processo |
| `PID` | ID do processo |
| `%CPU` | Uso de CPU |
| `%MEM` | Uso de memória |
| `VSZ` | Memória virtual (KB) |
| `RSS` | Memória física usada (KB) |
| `STAT` | Estado do processo |
| `COMMAND` | Comando que gerou o processo |

### Estados de Processo (STAT)

| Estado | Significado |
|--------|-------------|
| `R` | Running (executando) |
| `S` | Sleeping (aguardando) |
| `D` | Uninterruptible sleep (aguardando I/O) |
| `Z` | Zombie (processo filho que terminou mas não foi coletado) |
| `T` | Stopped (parado) |

---

## 5.2 `top` — Monitor de Processos em Tempo Real

### O que faz
Exibe os processos em tempo real, ordenados por uso de CPU por padrão. Interativo via teclado.

### Sintaxe
```bash
top [opções]
```

### Atalhos dentro do `top`

| Tecla | Ação |
|-------|------|
| `q` | Sair |
| `k` | Matar processo (pede o PID) |
| `M` | Ordenar por memória |
| `P` | Ordenar por CPU |
| `1` | Ver uso por núcleo de CPU |
| `u` | Filtrar por usuário |
| `h` | Ajuda |
| `Space` | Atualizar agora |

### Exemplos

```bash
# Iniciar o top
top

# Iniciar já ordenado por memória
top -o %MEM

# Ver apenas processos de um usuário
top -u joao

# Atualizar a cada 5 segundos
top -d 5

# Rodar em modo batch (útil para scripts)
top -b -n 1 | head -20
```

---

## 5.3 `htop` — Monitor Avançado e Visual

### O que faz
Versão melhorada do `top`, com interface colorida, suporte a mouse e mais funcionalidades.

### Instalar

```bash
sudo apt install htop        # Debian/Ubuntu
sudo dnf install htop        # Fedora
sudo pacman -S htop          # Arch
```

### Atalhos do `htop`

| Tecla | Ação |
|-------|------|
| `F2` | Configurações |
| `F3` | Buscar processo |
| `F4` | Filtrar processos |
| `F5` | Ver em árvore |
| `F6` | Ordenar por coluna |
| `F9` | Matar processo (menu de sinais) |
| `F10` | Sair |
| `u` | Filtrar por usuário |
| `t` | Alternar visão em árvore |

```bash
# Iniciar htop
htop

# Iniciar com delay personalizado (em décimos de segundo)
htop -d 20   # Atualiza a cada 2 segundos
```

---

## 5.4 `kill` e `killall` — Encerrar Processos

### `kill` — Por PID

```bash
# Sintaxe
kill [sinal] PID

# Encerrar graciosamente (SIGTERM - padrão)
kill 1234

# Forçar encerramento (SIGKILL - sem possibilidade de ignorar)
kill -9 1234

# Pausar processo
kill -STOP 1234

# Retomar processo pausado
kill -CONT 1234

# Listar todos os sinais
kill -l
```

### `killall` — Por Nome

```bash
# Encerrar todos os processos com esse nome
killall firefox

# Forçar
killall -9 nginx

# Encerrar processos de um usuário específico
sudo killall -u joao

# Encerrar apenas se o processo for de um executável específico
killall -e /usr/bin/python3
```

### Sinais Mais Importantes

| Sinal | Número | Descrição |
|-------|--------|-----------|
| `SIGTERM` | 15 | Encerramento educado (padrão) |
| `SIGKILL` | 9 | Encerramento forçado (não pode ser ignorado) |
| `SIGHUP` | 1 | Recarregar configuração |
| `SIGSTOP` | 19 | Pausar processo |
| `SIGCONT` | 18 | Retomar processo |

> 💡 **Boa prática:** Sempre tente `kill PID` (SIGTERM) antes de `kill -9 PID` (SIGKILL). O SIGTERM permite que o processo limpe recursos; o SIGKILL não.

---

## 5.5 `nice` e `renice` — Prioridade de Processos

### O que fazem
Controlam a prioridade de CPU de um processo. Valores de **-20** (mais prioritário) a **+19** (menos prioritário). O padrão é **0**.

### `nice` — Iniciar com prioridade definida

```bash
# Iniciar com baixa prioridade (nice +10)
nice -n 10 make -j4

# Iniciar backup com prioridade mínima
nice -n 19 rsync -av /origem/ /destino/

# Iniciar com alta prioridade (requer root)
sudo nice -n -10 processo_critico
```

### `renice` — Alterar prioridade de processo em execução

```bash
# Diminuir prioridade do processo 1234 (usar mais CPU)
sudo renice -n 5 -p 1234

# Aumentar prioridade (mais CPU - requer root para valores negativos)
sudo renice -n -5 -p 1234

# Mudar prioridade de todos os processos de um usuário
sudo renice -n 10 -u joao
```

### Cenário: Compilação longa sem travar o sistema

```bash
# Compilar com baixíssima prioridade para não afetar outros usuários
nice -n 19 make -j$(nproc)
```

---

## Resumo do Capítulo 5

```bash
# Encontrar processo que consome mais CPU
ps aux --sort=-%cpu | head -5

# Matar processo problemático
kill -9 PID

# Monitorar sistema em tempo real
htop

# Verificar se há processos zombie
ps aux | grep Z

# Reduzir prioridade de backup em execução
sudo renice -n 15 -p $(pgrep rsync)
```

---

<a name="cap6"></a>
# Capítulo 6 — Gerenciamento de Pacotes

## Introdução

Cada família de distribuições Linux tem seu próprio gerenciador de pacotes. Entender o gerenciador da sua distribuição é essencial para instalar, atualizar e manter software no sistema.

---

## 6.1 Debian/Ubuntu — `apt`

O **APT** (Advanced Package Tool) é o gerenciador padrão do Debian e Ubuntu.

### Operações Básicas

```bash
# Atualizar lista de pacotes disponíveis
sudo apt update

# Atualizar pacotes instalados
sudo apt upgrade

# Atualizar E remover pacotes desnecessários
sudo apt full-upgrade

# Instalar pacote
sudo apt install nome_pacote

# Instalar múltiplos pacotes
sudo apt install vim curl htop git

# Remover pacote (mantém configurações)
sudo apt remove nome_pacote

# Remover pacote E configurações
sudo apt purge nome_pacote

# Remover dependências não utilizadas
sudo apt autoremove

# Buscar pacote
apt search "editor de texto"

# Ver informações de um pacote
apt show vim

# Ver arquivos instalados por um pacote
dpkg -L vim

# Ver qual pacote instalou determinado arquivo
dpkg -S /usr/bin/vim

# Listar pacotes instalados
dpkg -l

# Baixar .deb sem instalar
apt download nome_pacote

# Instalar arquivo .deb local
sudo dpkg -i arquivo.deb
sudo apt install -f   # Resolver dependências após dpkg
```

### Fluxo de Atualização Recomendado

```bash
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```

---

## 6.2 Fedora — `dnf`

O **DNF** (Dandified YUM) é o gerenciador padrão do Fedora e RHEL.

```bash
# Atualizar lista de repositórios
sudo dnf check-update

# Atualizar o sistema
sudo dnf update

# Instalar pacote
sudo dnf install nome_pacote

# Remover pacote
sudo dnf remove nome_pacote

# Buscar pacote
dnf search "web server"

# Ver informações de um pacote
dnf info nginx

# Listar pacotes instalados
dnf list installed

# Ver histórico de transações
dnf history

# Desfazer última transação
sudo dnf history undo last

# Limpar cache
sudo dnf clean all

# Ver qual pacote fornece um arquivo
dnf provides /usr/bin/git

# Instalar grupo de pacotes
sudo dnf groupinstall "Development Tools"
```

---

## 6.3 Arch Linux — `pacman` e `yay`

O **pacman** é o gerenciador nativo do Arch Linux. O **yay** é um helper para o AUR (Arch User Repository).

### `pacman`

```bash
# Sincronizar repositórios e atualizar sistema
sudo pacman -Syu

# Instalar pacote
sudo pacman -S nome_pacote

# Instalar sem confirmação
sudo pacman -S --noconfirm nome_pacote

# Remover pacote
sudo pacman -R nome_pacote

# Remover com dependências não utilizadas
sudo pacman -Rs nome_pacote

# Remover com configs e dependências
sudo pacman -Rns nome_pacote

# Buscar pacote nos repositórios
pacman -Ss "editor"

# Ver informações de pacote
pacman -Si vim

# Listar pacotes instalados
pacman -Qs

# Ver arquivos de um pacote instalado
pacman -Ql vim

# Ver qual pacote possui um arquivo
pacman -Qo /usr/bin/vim

# Limpar cache
sudo pacman -Sc

# Remover pacotes órfãos
sudo pacman -Rns $(pacman -Qtdq)
```

### `yay` — AUR Helper

O AUR (Arch User Repository) contém milhares de pacotes mantidos pela comunidade.

```bash
# Instalar yay (primeira vez)
git clone https://aur.archlinux.org/yay.git
cd yay && makepkg -si

# Usar yay (igual ao pacman, mas acessa AUR)
yay -Syu              # Atualizar tudo (repositórios + AUR)
yay -S google-chrome  # Instalar do AUR
yay -Ss spotify       # Buscar no AUR
yay -R nome_pacote    # Remover
```

---

## Tabela Comparativa de Comandos

| Ação | apt (Debian/Ubuntu) | dnf (Fedora) | pacman (Arch) |
|------|---------------------|--------------|---------------|
| Atualizar lista | `apt update` | `dnf check-update` | `pacman -Sy` |
| Atualizar sistema | `apt upgrade` | `dnf update` | `pacman -Su` |
| Instalar | `apt install pkg` | `dnf install pkg` | `pacman -S pkg` |
| Remover | `apt remove pkg` | `dnf remove pkg` | `pacman -R pkg` |
| Buscar | `apt search pkg` | `dnf search pkg` | `pacman -Ss pkg` |
| Informações | `apt show pkg` | `dnf info pkg` | `pacman -Si pkg` |
| Listar instalados | `dpkg -l` | `dnf list installed` | `pacman -Q` |

---

<a name="cap7"></a>
# Capítulo 7 — Sistema de Arquivos e Permissões

## Introdução

O sistema de permissões do Linux é a espinha dorsal da sua segurança. Cada arquivo e diretório tem um dono, um grupo e permissões que controlam quem pode ler, escrever ou executar.

---

## 7.1 Entendendo Permissões

### A Notação de Permissões

Execute `ls -l` e veja:
```
-rwxr-xr--  1  joao  desenvolvedores  4096  Jan 15 10:00  script.sh
```

Decompondo:
```
- rwx r-x r--
│  │   │   └─ Outros (others): leitura
│  │   └───── Grupo: leitura + execução
│  └───────── Dono: leitura + escrita + execução
└──────────── Tipo: - arquivo, d diretório, l link
```

### Permissões Numéricas (Octal)

| Número | Permissão | Significado |
|--------|-----------|-------------|
| 7 | rwx | Leitura + Escrita + Execução |
| 6 | rw- | Leitura + Escrita |
| 5 | r-x | Leitura + Execução |
| 4 | r-- | Apenas Leitura |
| 3 | -wx | Escrita + Execução |
| 2 | -w- | Apenas Escrita |
| 1 | --x | Apenas Execução |
| 0 | --- | Sem permissão |

```
chmod 755 script.sh
      │││
      ││└─ Outros: 5 = r-x
      │└── Grupo:  5 = r-x
      └─── Dono:   7 = rwx
```

---

## 7.2 `chmod` — Alterar Permissões

### Sintaxe

```bash
chmod [opções] modo arquivo
```

### Notação Simbólica

```bash
# Adicionar permissão de execução para o dono
chmod u+x script.sh

# Remover permissão de escrita para grupo e outros
chmod go-w arquivo.txt

# Definir permissões exatas para todos
chmod a=rw arquivo.txt

# Combinações
chmod u+x,go-w script.sh
```

### Notação Numérica

```bash
# Permissões comuns
chmod 644 arquivo.txt       # -rw-r--r-- (arquivo comum)
chmod 755 script.sh         # -rwxr-xr-x (executável)
chmod 700 chave_privada.pem # -rwx------ (privado)
chmod 777 /tmp/compartilhado # ⚠️ Evitar em produção

# Aplicar recursivamente em diretório
chmod -R 755 /var/www/html
```

### Permissões Especiais

```bash
# SUID: executa com permissões do dono
chmod u+s executavel
# ou
chmod 4755 executavel

# SGID: arquivos herdam grupo do diretório
chmod g+s diretorio
chmod 2755 diretorio

# Sticky Bit: em /tmp, só o dono pode deletar o próprio arquivo
chmod +t /pasta/compartilhada
chmod 1777 /pasta/compartilhada
```

---

## 7.3 `chown` — Mudar Proprietário

### Sintaxe

```bash
sudo chown [opções] dono[:grupo] arquivo
```

### Exemplos Práticos

```bash
# Mudar dono
sudo chown joao arquivo.txt

# Mudar dono e grupo
sudo chown joao:desenvolvedores projeto/

# Mudar apenas grupo (equivalente ao chgrp)
sudo chown :desenvolvedores arquivo.txt

# Aplicar recursivamente
sudo chown -R www-data:www-data /var/www/html

# Mudar para o mesmo dono de outro arquivo de referência
sudo chown --reference=arquivo_ref.txt novo_arquivo.txt
```

---

## 7.4 `chgrp` — Mudar Grupo

```bash
# Mudar grupo de um arquivo
sudo chgrp desenvolvedores projeto.tar

# Recursivamente
sudo chgrp -R equipe /compartilhado

# Equivalente a chown :grupo
sudo chown :equipe /compartilhado
```

---

## 7.5 Links Simbólicos com `ln -s`

### O que é um link simbólico?

É como um atalho: aponta para outro arquivo. Se o original for deletado, o link fica "quebrado".

```bash
# Criar link simbólico
ln -s /caminho/original /caminho/link

# Exemplos práticos
ln -s /var/www/html/meu-site /home/joao/site    # Atalho para diretório
ln -s /usr/bin/python3 /usr/local/bin/python    # Alias de comando

# Ver links simbólicos
ls -la | grep "^l"
# ou
find . -type l

# Remover link (não remove o arquivo original)
rm link_simbolico

# Verificar para onde aponta
readlink -f link_simbolico
```

### Links Simbólicos vs. Hard Links

| Característica | Link Simbólico (`ln -s`) | Hard Link (`ln`) |
|----------------|--------------------------|------------------|
| Aponta para | Caminho | Inode |
| Funciona entre sistemas | ✅ Sim | ❌ Não |
| Funciona para diretórios | ✅ Sim | ❌ Não |
| Se original é deletado | Link quebra | Arquivo permanece |

---

## 7.6 Variáveis de Ambiente e Arquivos de Configuração

### Variáveis de Ambiente Importantes

```bash
# Ver todas as variáveis
env
printenv

# Ver variável específica
echo $HOME
echo $PATH
echo $USER
echo $SHELL

# Definir variável temporária (dura apenas a sessão)
export MEU_VAR="valor"
echo $MEU_VAR

# Remover variável
unset MEU_VAR
```

### Arquivos de Configuração do Shell

| Arquivo | Quando é carregado |
|---------|-------------------|
| `~/.bashrc` | Cada nova sessão bash interativa |
| `~/.bash_profile` | Login via terminal (não GUI) |
| `~/.profile` | Login (compatível com sh) |
| `~/.zshrc` | Cada sessão zsh |
| `/etc/environment` | Variáveis globais (todos os usuários) |
| `/etc/profile` | Login de todos os usuários |

### Adicionar ao PATH permanentemente

```bash
# Editar ~/.bashrc
nano ~/.bashrc

# Adicionar ao final:
export PATH="$PATH:/meu/diretorio/scripts"

# Aplicar sem reiniciar
source ~/.bashrc
# ou
. ~/.bashrc
```

---

## Resumo do Capítulo 7

```bash
# Permissões típicas
chmod 644 arquivo.txt        # Arquivo leitura para todos, escrita para dono
chmod 755 script.sh          # Script executável
chmod 700 privado/           # Diretório só para o dono
chmod -R 750 /app/           # Recursivo: dono tudo, grupo lê/executa, outros nada

# Mudar dono
sudo chown -R www-data:www-data /var/www/

# Criar atalho
ln -s /opt/meu-app/bin/meu-app /usr/local/bin/meu-app
```

---

<a name="cap8"></a>
# Capítulo 8 — Automação e Produtividade

## Introdução

O poder real do Linux está na capacidade de combinar ferramentas simples para criar fluxos de trabalho poderosos. Este capítulo cobre as técnicas essenciais de automação que farão você trabalhar muito mais rápido.

---

## 8.1 Redirecionamento de Entrada e Saída

### Operadores de Redirecionamento

| Operador | Descrição |
|----------|-----------|
| `>` | Redireciona saída (sobrescreve) |
| `>>` | Redireciona saída (anexa/append) |
| `<` | Redireciona entrada |
| `2>` | Redireciona erros (stderr) |
| `2>>` | Redireciona erros (anexa) |
| `&>` | Redireciona saída e erros |
| `\|` | Pipe: passa saída para próximo comando |

### Exemplos Práticos

```bash
# Salvar saída em arquivo (sobrescreve)
ls -la > lista.txt

# Adicionar ao final do arquivo
echo "Nova linha" >> log.txt

# Descartar erros
find / -name "*.conf" 2>/dev/null

# Salvar saída E erros no mesmo arquivo
comando &> tudo.log

# Redirecionar erros para saída padrão
comando 2>&1 | less

# Usar arquivo como entrada
sort < lista.txt

# Pipeline: processar saída de um comando com outro
cat /etc/passwd | cut -d: -f1 | sort
```

---

## 8.2 `grep` — Buscar Padrões em Texto

### O que faz
Busca linhas que correspondem a um padrão (texto ou expressão regular).

### Sintaxe
```bash
grep [opções] padrão [arquivo...]
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-i` | Ignora maiúsculas/minúsculas |
| `-r` | Busca recursiva em diretórios |
| `-n` | Mostra número da linha |
| `-v` | Inverte (mostra linhas que NÃO combinam) |
| `-l` | Mostra apenas nomes dos arquivos |
| `-c` | Conta ocorrências |
| `-A N` | Mostra N linhas após o match |
| `-B N` | Mostra N linhas antes do match |
| `-E` | Expressões regulares estendidas |
| `--color` | Destaca o padrão em cor |

### Exemplos Práticos

```bash
# Buscar palavra em arquivo
grep "erro" /var/log/syslog

# Ignorar maiúsculas
grep -i "error" /var/log/nginx/error.log

# Busca recursiva em diretório
grep -r "TODO" /home/joao/projetos/

# Mostrar número da linha
grep -n "def " script.py

# Linhas que NÃO contêm o padrão
grep -v "^#" /etc/ssh/sshd_config   # Remove comentários

# Buscar múltiplos padrões
grep -E "error|warning|critical" app.log

# Contar ocorrências
grep -c "404" /var/log/nginx/access.log

# Ver contexto em torno do match
grep -A 3 -B 1 "Exception" app.log

# Buscar em todos os arquivos .py do diretório atual
grep -rn "import os" *.py

# Combinar com pipe
ps aux | grep nginx | grep -v grep
```

---

## 8.3 `find` — Encontrar Arquivos

### O que faz
Busca arquivos e diretórios com base em critérios como nome, tamanho, data, permissões, etc.

### Sintaxe
```bash
find [onde] [critérios] [ação]
```

### Exemplos Práticos

```bash
# Buscar por nome
find /home -name "*.log"

# Busca case-insensitive
find / -iname "readme.md" 2>/dev/null

# Buscar por tipo
find /var -type f   # Arquivos
find /var -type d   # Diretórios
find /etc -type l   # Links simbólicos

# Buscar por tamanho
find /var/log -size +100M     # Maior que 100MB
find /tmp -size -10k          # Menor que 10KB
find . -size +1M -size -100M  # Entre 1MB e 100MB

# Buscar por data de modificação
find /home -mtime -7     # Modificados nos últimos 7 dias
find /tmp -mtime +30     # Não modificados há mais de 30 dias

# Buscar por permissões
find / -perm 777         # Permissão exata 777
find / -perm -4000       # Com SUID set

# Buscar por dono
find /home -user joao
find /var -group www-data

# Executar ação nos resultados
find . -name "*.tmp" -delete          # Deletar temporários
find . -name "*.sh" -exec chmod +x {} \;  # Tornar scripts executáveis
find /logs -name "*.log" -exec gzip {} \; # Comprimir logs

# Combinações
find /var/log -name "*.log" -size +50M -mtime +30
```

---

## 8.4 `xargs` — Construir e Executar Comandos

### O que faz
Lê entradas da entrada padrão e as passa como argumentos para um comando. Essencial para trabalhar com resultados do `find`.

### Exemplos Práticos

```bash
# Deletar arquivos encontrados pelo find
find . -name "*.tmp" | xargs rm

# Com espaços em nomes de arquivo (use -print0 e -0)
find . -name "*.log" -print0 | xargs -0 rm

# Mover arquivos encontrados
find . -name "*.jpg" | xargs -I{} mv {} /fotos/

# Processar em paralelo (4 processos simultâneos)
find . -name "*.jpg" | xargs -P 4 -I{} convert {} -resize 800x600 {}_small.jpg

# Grep em múltiplos arquivos
find . -name "*.py" | xargs grep "import"

# Limitar número de argumentos por chamada
find . -name "*.txt" | xargs -n 10 ls -la
```

---

## 8.5 `tar` e `zip` — Compactar e Arquivar

### `tar` — Archivar e Comprimir

```bash
# Criar arquivo .tar.gz (comprimido)
tar -czf backup.tar.gz /pasta/

# Criar .tar.bz2 (compressão maior, mais lento)
tar -cjf backup.tar.bz2 /pasta/

# Criar .tar.xz (compressão máxima)
tar -cJf backup.tar.xz /pasta/

# Extrair .tar.gz
tar -xzf backup.tar.gz

# Extrair em diretório específico
tar -xzf backup.tar.gz -C /destino/

# Listar conteúdo sem extrair
tar -tzf backup.tar.gz

# Extrair arquivo específico
tar -xzf backup.tar.gz pasta/arquivo.txt

# Com verbose (ver arquivos sendo processados)
tar -czfv backup.tar.gz /pasta/
```

**Dica para lembrar os parâmetros:**
- `c` = **C**riar
- `x` = e**X**trair
- `z` = g**Z**ip
- `j` = bzip2 (**J**)
- `J` = xz (**J** maiúsculo)
- `f` = arquivo (**F**ile) — sempre por último

### `zip` e `unzip`

```bash
# Criar arquivo zip
zip arquivo.zip arquivo1 arquivo2

# Zipar diretório
zip -r backup.zip /pasta/

# Com senha
zip -e -r seguro.zip /pasta/

# Extrair
unzip arquivo.zip

# Extrair em diretório específico
unzip arquivo.zip -d /destino/

# Listar conteúdo
unzip -l arquivo.zip

# Ver uso do disco antes/depois
du -sh pasta/ && zip -r comprimido.zip pasta/ && du -sh comprimido.zip
```

---

## 8.6 `rsync` — Sincronizar Arquivos

### O que faz
Sincroniza arquivos e diretórios de forma eficiente, transferindo apenas as diferenças. Funciona localmente e via SSH.

### Sintaxe
```bash
rsync [opções] origem destino
```

### Principais Parâmetros

| Parâmetro | Descrição |
|-----------|-----------|
| `-a` | Modo arquivo (preserva permissões, dono, timestamps) |
| `-v` | Verbose (mostra arquivos sendo copiados) |
| `-z` | Comprimir durante transferência |
| `-P` | Mostrar progresso + retomar transferências |
| `--delete` | Remove arquivos no destino que não existem na origem |
| `-n` | Dry run (simula sem executar) |
| `--exclude="padrão"` | Excluir arquivos/pastas |

### Exemplos Práticos

```bash
# Sincronização local básica
rsync -av /origem/ /destino/

# ATENÇÃO: origem/ (com barra) copia CONTEÚDO; origem (sem barra) copia a PASTA
rsync -av /home/joao/docs/ /backup/docs/    # Copia conteúdo de docs/
rsync -av /home/joao/docs /backup/          # Cria /backup/docs/ e copia

# Backup com deleção (espelho exato)
rsync -av --delete /home/joao/ /backup/home-joao/

# Excluir node_modules e .git
rsync -av --exclude=node_modules --exclude=.git /projeto/ /backup/projeto/

# Simular antes de executar
rsync -avn --delete /origem/ /destino/

# Backup via SSH
rsync -avz -e ssh /local/ usuario@servidor:/remoto/

# Backup via SSH com porta customizada
rsync -avz -e "ssh -p 2222" /local/ usuario@servidor:/remoto/

# Baixar do servidor para local
rsync -avz usuario@servidor:/var/www/ /local/www/
```

---

## 8.7 `cron` — Agendar Tarefas

### O que é o cron?

O `cron` é o agendador de tarefas do Linux. Permite executar comandos automaticamente em horários definidos.

### Editar o crontab

```bash
# Editar tarefas do usuário atual
crontab -e

# Ver tarefas agendadas
crontab -l

# Remover todas as tarefas (cuidado!)
crontab -r

# Editar crontab de outro usuário (como root)
sudo crontab -u joao -e
```

### Sintaxe do crontab

```
* * * * * comando
│ │ │ │ │
│ │ │ │ └── Dia da semana (0-7, 0=domingo, 7=domingo também)
│ │ │ └──── Mês (1-12)
│ │ └────── Dia do mês (1-31)
│ └──────── Hora (0-23)
└────────── Minuto (0-59)
```

### Exemplos de Agendamento

```bash
# Executar a cada minuto
* * * * * /script/monitorar.sh

# Às 3h da manhã todos os dias
0 3 * * * /script/backup.sh

# A cada 6 horas
0 */6 * * * /script/verificar.sh

# Toda segunda-feira às 8h30
30 8 * * 1 /script/relatorio.sh

# Primeiro dia do mês à meia-noite
0 0 1 * * /script/fechamento.sh

# De segunda a sexta às 9h
0 9 * * 1-5 /script/diario.sh

# A cada 15 minutos
*/15 * * * * /script/checar.sh

# Atalhos especiais
@reboot    /script/inicializar.sh    # Ao iniciar o sistema
@daily     /script/backup.sh         # Uma vez por dia (00:00)
@weekly    /script/limpeza.sh        # Uma vez por semana
@monthly   /script/relatorio.sh      # Uma vez por mês
```

### Exemplo Real de crontab

```bash
# Abrir para editar
crontab -e

# Adicionar estas linhas:

# Backup diário às 2h
0 2 * * * rsync -a /home/joao/ /backup/joao/ >> /var/log/backup.log 2>&1

# Limpeza de /tmp semanalmente
0 4 * * 0 find /tmp -mtime +7 -delete >> /var/log/limpeza.log 2>&1

# Verificar uso de disco a cada hora e alertar se > 90%
0 * * * * df -h / | awk 'NR==2{if($5+0 > 90) print "ALERTA: disco " $5 " cheio"}' >> /var/log/disco.log
```

> 💡 **Dica:** Sempre redirecione a saída em cron jobs (`>> /log/arquivo.log 2>&1`) para ter registro do que foi executado e eventuais erros.

---

## Resumo do Capítulo 8

```bash
# Encontrar e deletar arquivos temporários
find /tmp -mtime +30 -name "*.tmp" | xargs rm -f

# Comprimir logs antigos
find /var/log -name "*.log" -mtime +7 | xargs -I{} gzip {}

# Backup incremental via rsync
rsync -avz --delete /dados/ /backup/dados/

# Grep em logs para erros
grep -i "error\|critical\|fail" /var/log/syslog | tail -50

# Agendar backup às 3h
crontab -e
# Adicionar: 0 3 * * * rsync -a /home/ /backup/
```

---

<a name="cap9"></a>
# Capítulo 9 — Tópicos Intermediários e Avançados

## 9.1 O Processo de Boot do Linux

### Sequência de Inicialização

```
1. BIOS/UEFI
   └── POST (Power-On Self Test)
   └── Identifica dispositivo de boot

2. Bootloader (GRUB2)
   └── Carregado da partição /boot/efi ou MBR
   └── Apresenta menu de sistemas operacionais
   └── Carrega o kernel Linux

3. Kernel Linux
   └── Descomprime e se carrega na memória
   └── Inicializa drivers de hardware
   └── Monta o filesystem raiz (/) em modo read-only
   └── Inicia o processo PID 1 (systemd)

4. systemd (PID 1)
   └── Lê targets e units
   └── Monta sistemas de arquivos (/etc/fstab)
   └── Inicia serviços em paralelo
   └── Alcança o target final (multi-user ou graphical)

5. Login Manager
   └── getty (terminal) ou GDM/SDDM (gráfico)
```

### Diagnóstico de Boot

```bash
# Ver tempo de boot de cada serviço
systemd-analyze blame

# Análise gráfica do boot
systemd-analyze plot > boot.svg

# Ver o tempo total de boot
systemd-analyze

# Ver logs do boot atual
journalctl -b

# Ver logs do boot anterior (útil se travou)
journalctl -b -1
```

---

## 9.2 Como Funciona o systemd

### Conceitos Fundamentais

**Unit:** Qualquer recurso gerenciado pelo systemd (serviços, mounts, timers, etc.)

**Target:** Grupos de units (equivalente ao antigo runlevel)

| Target | Descrição |
|--------|-----------|
| `poweroff.target` | Sistema desligado |
| `rescue.target` | Modo de recuperação (single user) |
| `multi-user.target` | Multi-usuário sem gráficos |
| `graphical.target` | Multi-usuário com interface gráfica |

```bash
# Ver o target atual
systemctl get-default

# Mudar o target padrão
sudo systemctl set-default multi-user.target

# Ir para modo de recuperação agora
sudo systemctl isolate rescue.target

# Ver dependências de um serviço
systemctl list-dependencies nginx

# Ver unit file de um serviço
systemctl cat nginx

# Editar unit file (sem modificar o original)
sudo systemctl edit nginx
```

### Estrutura de um Unit File

```ini
# /etc/systemd/system/meu-app.service
[Unit]
Description=Minha Aplicação
After=network.target

[Service]
Type=simple
User=www-data
WorkingDirectory=/opt/meu-app
ExecStart=/opt/meu-app/bin/start.sh
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

```bash
# Após criar um novo unit file
sudo systemctl daemon-reload
sudo systemctl enable --now meu-app
```

---

## 9.3 Variáveis de Ambiente

### PATH — O Caminho de Busca de Comandos

O `PATH` define onde o sistema busca executáveis quando você digita um comando.

```bash
# Ver o PATH atual
echo $PATH
# Exemplo: /usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin

# Adicionar diretório ao PATH temporariamente
export PATH="$PATH:/meu/diretorio"

# Adicionar permanentemente (para o usuário)
echo 'export PATH="$PATH:/meu/diretorio"' >> ~/.bashrc
source ~/.bashrc

# Adicionar para todos os usuários
echo 'export PATH="$PATH:/usr/local/meu-app/bin"' | sudo tee /etc/profile.d/meu-app.sh
```

### `.bashrc` vs `.bash_profile`

```bash
# .bashrc — executado em shells interativos não-login
# .bash_profile — executado em shells de login

# Prática recomendada: colocar tudo em .bashrc e no .bash_profile apenas:
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
```

### Personalizando o Shell

```bash
# Exemplos de customizações no ~/.bashrc

# Aliases úteis
alias ll='ls -lah'
alias grep='grep --color=auto'
alias update='sudo apt update && sudo apt upgrade'
alias ..='cd ..'
alias ...='cd ../..'

# Funções
mkcd() {
    mkdir -p "$1" && cd "$1"
}

# Prompt customizado (PS1)
export PS1='\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '

# Histórico maior
export HISTSIZE=10000
export HISTFILESIZE=20000
```

---

## 9.4 Gerenciamento de Logs

### Estrutura de Logs no Linux

```
/var/log/
├── syslog          # Log geral do sistema (Debian/Ubuntu)
├── messages        # Log geral (Fedora/RHEL)
├── auth.log        # Autenticações e sudo
├── kern.log        # Mensagens do kernel
├── dpkg.log        # Instalações de pacotes (Debian)
├── nginx/
│   ├── access.log  # Acessos ao nginx
│   └── error.log   # Erros do nginx
└── journal/        # Logs binários do systemd
```

### Rotação de Logs com `logrotate`

```bash
# Ver configuração
cat /etc/logrotate.conf

# Ver configurações por serviço
ls /etc/logrotate.d/

# Exemplo de configuração custom
cat > /etc/logrotate.d/meu-app << 'EOF'
/var/log/meu-app/*.log {
    daily
    missingok
    rotate 30
    compress
    delaycompress
    notifempty
    create 640 www-data adm
    sharedscripts
    postrotate
        systemctl reload meu-app
    endscript
}
EOF

# Testar configuração
sudo logrotate -d /etc/logrotate.d/meu-app

# Forçar rotação
sudo logrotate -f /etc/logrotate.conf
```

---

## 9.5 Introdução a Containers e Virtualização

### Docker

O Docker permite empacotar aplicações em containers — ambientes isolados e portáteis.

```bash
# Instalar Docker (Ubuntu)
curl -fsSL https://get.docker.com | sudo sh
sudo usermod -aG docker $USER

# Verificar instalação
docker --version
docker run hello-world

# Conceitos básicos
docker pull nginx               # Baixar imagem
docker run nginx                # Criar e iniciar container
docker run -d nginx             # Em background (detached)
docker run -d -p 80:80 nginx    # Com port mapping
docker run -d --name meu-nginx nginx   # Com nome

# Gerenciar containers
docker ps                       # Containers rodando
docker ps -a                    # Todos (incluindo parados)
docker stop meu-nginx           # Parar
docker start meu-nginx          # Iniciar
docker restart meu-nginx        # Reiniciar
docker rm meu-nginx             # Remover container

# Imagens
docker images                   # Listar imagens
docker rmi nginx                # Remover imagem

# Logs
docker logs meu-nginx
docker logs -f meu-nginx        # Em tempo real

# Entrar no container
docker exec -it meu-nginx bash

# Criar imagem com Dockerfile
cat > Dockerfile << 'EOF'
FROM ubuntu:22.04
RUN apt-get update && apt-get install -y nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
EOF

docker build -t minha-imagem .
docker run -d -p 80:80 minha-imagem
```

### Docker Compose

```yaml
# docker-compose.yml
version: '3.8'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
  
  db:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: senha123
    volumes:
      - dados_db:/var/lib/postgresql/data

volumes:
  dados_db:
```

```bash
docker compose up -d         # Iniciar
docker compose down          # Parar e remover
docker compose logs -f       # Ver logs
docker compose ps            # Status
```

### Podman — Alternativa ao Docker (sem daemon)

```bash
# Instalar (Fedora/RHEL - já vem pré-instalado)
sudo dnf install podman

# Ubuntu
sudo apt install podman

# Uso (quase idêntico ao Docker)
podman pull nginx
podman run -d -p 80:80 nginx
podman ps
podman stop ID

# Podman não requer root (rootless)
podman run nginx   # Sem sudo!
```

### KVM — Virtualização Completa

```bash
# Verificar suporte à virtualização
egrep -c '(vmx|svm)' /proc/cpuinfo   # > 0 = suportado

# Instalar KVM e ferramentas
sudo apt install qemu-kvm libvirt-daemon-system virt-manager

# Adicionar usuário ao grupo
sudo usermod -aG libvirt,kvm $USER

# Interface gráfica
virt-manager

# CLI com virsh
virsh list --all          # Listar VMs
virsh start minha-vm      # Iniciar VM
virsh shutdown minha-vm   # Desligar
virsh snapshot-create-as minha-vm snap1   # Criar snapshot
```

---

## 9.6 Conceitos de Segurança — Revisão

### Resumo: Usuários, Grupos e Processos

```
┌─────────────────────────────────────────────┐
│                  USUÁRIO ROOT                │
│           UID=0 - Acesso Total              │
└─────────────────────────────────────────────┘
                       │
              ┌────────┴────────┐
              │                 │
        ┌─────▼─────┐    ┌─────▼─────┐
        │  Usuário  │    │  Usuário  │
        │   joao    │    │  maria    │
        │  UID=1000 │    │  UID=1001 │
        └─────┬─────┘    └─────┬─────┘
              │                 │
       Grupos: joao,sudo  Grupos: maria,docker
```

### Princípio do Menor Privilégio

- Cada processo deve ter apenas as permissões mínimas necessárias.
- Use `sudo` ao invés de trabalhar como root.
- Configure serviços para rodar como usuários dedicados (ex: `www-data`, `nginx`, `postgres`).

```bash
# Ver com qual usuário um serviço roda
ps aux | grep nginx
# www-data  1234  0.0  0.1  nginx: worker process

# Ver arquivos SUID (potencial risco de segurança)
sudo find / -perm -4000 -type f 2>/dev/null

# Ver arquivos sem dono (arquivos órfãos)
sudo find / -nouser -o -nogroup 2>/dev/null
```

---

## Apêndice — Referência Rápida

### Atalhos Essenciais do Terminal

| Atalho | Ação |
|--------|------|
| `Ctrl+C` | Interromper processo |
| `Ctrl+Z` | Suspender processo |
| `Ctrl+D` | Sair/EOF |
| `Ctrl+L` | Limpar tela |
| `Ctrl+A` | Início da linha |
| `Ctrl+E` | Fim da linha |
| `Ctrl+R` | Buscar no histórico |
| `Tab` | Autocompletar |
| `!!` | Repetir último comando |
| `!$` | Último argumento do comando anterior |
| `sudo !!` | Repetir último comando com sudo |

### Comandos de Emergência

```bash
# Sistema travado - matar processo pelo nome
sudo killall -9 nome_processo

# Desmontar dispositivo ocupado
sudo fuser -km /mnt/pendrive && sudo umount /mnt/pendrive

# Recuperar arquivos deletados com rm (se não sobreescrito)
sudo debugfs /dev/sda1  # Ferramenta avançada

# Resetar permissões de /home
sudo chmod 755 /home
sudo chown -R joao:joao /home/joao

# Ver o que está usando a porta 80
sudo ss -tlnp | grep :80
sudo fuser 80/tcp

# Listar arquivos abertos por um processo
sudo lsof -p PID

# Ver chamadas de sistema de um processo (debug avançado)
sudo strace -p PID
```

### Estrutura de Diretórios do Linux (FHS)

```
/               # Raiz do sistema
├── bin/        # Binários essenciais (ls, cp, mv...)
├── boot/       # Arquivos de boot (kernel, grub)
├── dev/        # Dispositivos (discos, terminais)
├── etc/        # Configurações do sistema
├── home/       # Diretórios dos usuários
├── lib/        # Bibliotecas do sistema
├── media/      # Mídias removíveis (automount)
├── mnt/        # Montagens manuais
├── opt/        # Software de terceiros
├── proc/       # Sistema de arquivos virtual (processos)
├── root/       # Home do root
├── run/        # Dados de runtime
├── sbin/       # Binários de administração
├── srv/        # Dados de serviços
├── sys/        # Sistema de arquivos virtual (hardware)
├── tmp/        # Temporários (limpos no boot)
├── usr/        # Programas e dados de usuário
│   ├── bin/   # Binários de usuário
│   ├── lib/   # Bibliotecas
│   └── local/ # Software local/customizado
└── var/        # Dados variáveis (logs, spool, cache)
    ├── log/   # Logs do sistema
    └── www/   # Dados de servidores web
```

---

## Considerações Finais

Parabéns por chegar até aqui! Você agora tem uma base sólida para administrar sistemas Linux. Os próximos passos recomendados são:

### Para continuar aprendendo

1. **Praticar em ambiente seguro:** Use VMs com VirtualBox ou KVM para experimentar sem medo de quebrar o sistema principal.

2. **Shell Scripting:** Combine tudo que aprendeu em scripts bash para automatizar tarefas repetitivas.

3. **Segurança:** Estude `iptables`/`nftables`, `fail2ban`, `SELinux`/`AppArmor`.

4. **Redes avançadas:** Aprofunde em `iptables`, roteamento, VPN com WireGuard.

5. **Certificações:** Considere Linux Foundation (LFCS, LFCE) ou Red Hat (RHCSA, RHCE).

### Recursos Recomendados

- **man** — O manual embutido: `man nome_do_comando`
- **tldr** — Resumos práticos: `tldr nome_do_comando`
- **LinuxCommand.org** — Aprendizado progressivo
- **ArchWiki** — Wiki mais completa sobre Linux (funciona para qualquer distro!)
- **Linux Journey** — linuxjourney.com

```bash
# Sempre que tiver dúvida sobre um comando:
man comando           # Manual completo
comando --help        # Ajuda rápida
tldr comando          # Exemplos práticos (instalar: apt install tldr)
info comando          # Documentação GNU
```

---

*Apostila desenvolvida para administradores e usuários Linux — do básico ao intermediário.*  
*Versão 1.0 — 2024*
