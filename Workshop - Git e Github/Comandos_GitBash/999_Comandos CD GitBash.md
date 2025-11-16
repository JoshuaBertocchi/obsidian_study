# Comandos de Terminal, usando o Git Bash
## 🔹 Entrar em pastas
```bash
cd "Nome_da_pasta"      # Entrar na pasta
cd pasta1/pasta2        # Entrar em subpastas direto
cd "Minha Pasta"        # Entrar em pasta com espaço

```
## 🔹 Volta as pastas
```bash
cd ..                   # Volta 1 pasta
cd ../..                # Volta 2 pastas
cd ../../..             # Volta 3 pastas
cd ../../../../         # Volta 4 pastas```
```
## 🔹 Ir para locais importantes
```bash
cd ~                    # Ir para HOME do usuário
cd $HOME                # Mesma coisa que ~
cd /                    # Ir para a raiz do sistema
cd -                    # Voltar para a pasta anterior
```
## 🔹 Acessar unidades no Git Bash

```bash
cd /c                   # Acessa o disco C:
cd /d                   # Acessa o disco D:
cd /e                   # Acessa o disco E:
```

## 🔹 Caminhos completos

```bash
cd /c/Users/Joshua/Documents   # Caminho absoluto
cd "/c/Users/Joshua/Minha Pasta" 
```

## 🔹 Comandos úteis com TAB

```bash
cd Doc<TAB>            # Autocomplete para 'Documents'
cd Meu<TAB>            # Autocomplete para 'Meu Projeto'
```

## 🔹 Returnar para diretórios anteriores

```bash
cd -                   # Alterna entre duas pastas
cd ~/Downloads         # Volta à pasta Downloads
cd ~/Desktop           # Volta à área de trabalho
```

## 🔹 Expansões avançadas (opcional)

```bash
cd $(printf '../%.0s' {1..3})   # Voltar 3 pastas dinamicamente
cd $(printf '../%.0s' {1..5})   # Voltar 5 pastas
```

## 🔹 Casos especiais

```bash
cd .                   # Fica na mesma pasta
cd ""                  # Nada acontece, permanece no local
cd ~usuario            # Acessa a home de outro usuário (Linux/Mac)
```

---
#gitbash 
#git 
#jornada_dos_dados