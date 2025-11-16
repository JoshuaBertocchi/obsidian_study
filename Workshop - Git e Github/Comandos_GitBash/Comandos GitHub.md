# 🐙 Guia Completo de Git & GitHub

## 📌 1. Configuração inicial (uma vez por máquina)
```bash
git config --global user.name "Seu Nome"
git config --global user.email "seuemail@exemplo.com"
git config --global init.defaultBranch main
````

---

## 📌 2. Criar um repositório

### Criar um repositório novo

```bash
git init
```

### Criar um repositório já com README no GitHub

Depois:

```bash
git clone https://github.com/usuario/repositorio.git
```

---

## 📌 3. Status e controle

```bash
git status       # Ver estado atual
git log          # Histório de commits
git log --oneline
```

---

## 📌 4. Adicionar arquivos para commit

```bash
git add arquivo.txt     # Adiciona apenas 1 arquivo
git add pasta/          # Adiciona uma pasta
git add .               # Adiciona tudo
```

---

## 📌 5. Fazer commit

```bash
git commit -m "Mensagem"
git commit -am "Add + commit de arquivos rastreados"
```

---

## 📌 6. Conectar ao GitHub (primeira conexão)

No GitHub → Criar repositório vazio → copiar o link

### HTTPS

```bash
git remote add origin https://github.com/usuario/repositorio.git
```

### SSH

```bash
git remote add origin git@github.com:usuario/repositorio.git
```

Verificar se conectou:

```bash
git remote -v
```

---

## 📌 7. Enviar para o GitHub

```bash
git push -u origin main   # Primeira vez
git push                  # Próximas vezes
```

---

## 📌 8. Baixar atualizações do GitHub

```bash
git pull                  # Atualiza o repositório local
git pull origin main
```

---

## 📌 9. Clonar repositórios

```bash
git clone https://github.com/usuario/repositorio.git
```

---

## 📌 10. Criar e trocar de branches

```bash
git branch                # Lista branches
git branch nova-feature  # Cria branch
git checkout nova-feature # Troca para ela
git checkout -b teste     # Cria + troca
```

---

## 📌 11. Mesclar branches

Estando na **main**:

```bash
git merge nova-feature
```

---

## 📌 12. Resolver conflitos

Durante conflito:

```bash
<<<<<<< HEAD
Código atual
=======
Código vindo do outro branch
>>>>>>> nova-feature
```

Depois de resolver:

```bash
git add .
git commit -m "Conflitos resolvidos"
```

---

## 📌 13. Deletar branch

```bash
git branch -d nome-branch
git branch -D nome-branch   # Forçar
```

---

## 📌 14. Remover arquivo do Git mas não da máquina

```bash
git rm --cached arquivo.txt
```

---

## 📌 15. Resetar alterações

### Desfazer mudanças do arquivo sem commit

```bash
git checkout -- arquivo.txt
```

### Limpar tudo localmente

```bash
git reset --hard
```

---

## 📌 16. Ignorar arquivos com `.gitignore`

Criar arquivo:

```
node_modules/
*.log
.env
```

Adicionar:

```bash
git add .gitignore
git commit -m "Add gitignore"
```

---

## 📌 17. Reposicionar commits (rebase)

```bash
git rebase main
```

---

## 📌 18. Atualizar branch local para última versão remota

```bash
git fetch
git pull
```

---

## 📌 19. Renomear branch

```bash
git branch -m novo-nome
```

---

## 📌 20. Ver diferenças

```bash
git diff               # Ver alterações não commitadas
git diff --staged      # Ver alterações já adicionadas
```

---

## 📌 21. Remover repositório remoto e adicionar outro

```bash
git remote remove origin
git remote add origin novo_link
```

---
#github 