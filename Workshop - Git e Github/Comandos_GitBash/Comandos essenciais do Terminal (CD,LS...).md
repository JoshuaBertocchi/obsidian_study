Anotações[[Gerenciamento de Ambiente|.]] #terminal 
 
# 🟦 CD — Navegar entre pastas
```bash
cd "pasta"            # Entra na pasta
cd pasta1/pasta2      # Entra em subpastas
cd ..                 # Volta 1 pasta
cd ../..              # Volta 2 pastas
cd ../../..           # Volta 3 pastas
cd ~                  # Vai para a pasta HOME
cd /                  # Vai para a raiz do sistema
cd -                  # Volta para o diretório anterior
cd /c                 # Acessa o disco C: (Git Bash)
cd /d                 # Acessa o disco D:
cd "/c/Meu Arquivo"   # Caminho com espaços
cd .                  # Fica no mesmo lugar
## 🔹 Casos especiais

```bash
cd .                   # Fica na mesma pasta
cd ""                  # Nada acontece, permanece no local
cd ~usuario            # Acessa a home de outro usuário (Linux/Mac)
```

# 🟦 LS — Listar arquivos
```bash

ls              # Mostra os arquivos da pasta
ls -a           # Mostra arquivos ocultos
ls -l           # Lista detalhada (tamanho, permissões)
ls -al          # Lista detalhada incluindo arquivos ocultos
ls -h           # Mostra tamanhos em formato legível
ls -R           # Lista pastas e subpastas (recursivo)
ls *.txt        # Lista todos os arquivos .txt
ls -t           # Ordena por data (mais recente primeiro)
```

---

# 🟥 RM — Remover arquivos/pastas

⚠️ Cuidado! `rm` não envia para lixeira.

```bash
rm arquivo.txt          # Remove arquivo
rm -f arquivo.txt       # Remove sem pedir confirmação
rm *.txt                # Remove todos .txt da pasta
rm -r pasta             # Remove pasta e conteúdo
rm -rf pasta            # Remove pasta e ignora erros (perigoso)
```

---

# 🟨 MV — Mover ou renomear

```bash
mv arquivo.txt pasta/       # Move arquivo para pasta
mv arquivo.txt novo_nome.txt   # Renomeia arquivo
mv *.txt pasta/             # Move todos arquivos .txt
mv pasta1/ pasta2/backup/   # Move pasta para dentro de outra
```

---

# 🟩 CP — Copiar arquivos

```bash
cp arquivo.txt backup/          # Copia arquivo
cp -r pasta/ backup/            # Copia pasta recursivamente
cp *.txt pasta/                 # Copia todos .txt
cp arquivo.txt novo_arquivo.txt # Duplica arquivo
```

---

# 🟧 MKDIR — Criar pastas

```bash
mkdir nova_pasta          # Cria pasta
mkdir -p caminho/pasta    # Cria várias pastas ao mesmo tempo
```

---

# 🟪 TOUCH — Criar arquivos

```bash
touch arquivo.txt         # Cria arquivo vazio
touch a.txt b.txt c.txt   # Cria vários arquivos
```

---

# 🟫 CAT — Ler arquivos

```bash
cat arquivo.txt       # Mostra conteúdo
cat a.txt b.txt       # Mostra arquivos em sequência
cat arquivo.txt | less  # Mostra com rolagem
```

---

# 🟧 GREP — Buscar texto

```bash
grep "palavra" arquivo.txt        # Busca texto no arquivo
grep -i "palavra" arquivo.txt     # Busca ignorando maiúsc/minúsc
grep -r "palavra" pasta/          # Busca dentro de pastas
grep -n "palavra" arquivo.txt     # Mostra número da linha
```

---

# 🟦 PWD — Mostrar diretório atual

```bash
pwd             # Exibe o caminho completo da pasta atual
```

---

# 🟩 CLEAR — Limpar tela

```bash
clear           # Limpa o terminal
Ctrl + L        # Atalho que faz o mesmo
```

---

# 🔵 OUTROS COMANDOS ÚTEIS

## **WHOAMI — Quem é o usuário**

```bash
whoami
```

## **DATE — Mostrar data**

```bash
date
```

## **HISTORY — Histórico de comandos**

```bash
history
```

## **HEAD / TAIL — Ler parte do arquivo**

```bash
head arquivo.txt      # Primeiras linhas
tail arquivo.txt      # Últimas linhas
tail -f log.txt       # Acompanha arquivo em tempo real
```

---
#gitbash 
#git 
#jornada_dos_dados
