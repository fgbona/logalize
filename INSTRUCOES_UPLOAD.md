# 📤 Como Fazer Upload para o GitHub

Este guia mostra como criar o repositório "logalize" no seu GitHub e fazer upload dos arquivos.

## Opção 1: Via Interface Web do GitHub (Mais Fácil) 🌐

### Passo 1: Criar o Repositório

1. Acesse https://github.com/new
2. Configure o repositório:
   - **Repository name**: `logalize`
   - **Description**: `Configuração completa para Logalize - colorador de logs`
   - **Public** ou **Private**: escolha conforme preferir
   - ⚠️ **NÃO** marque "Add a README file" (já temos um)
   - ⚠️ **NÃO** adicione .gitignore (já temos um)
   - ⚠️ **NÃO** adicione license (já temos uma)
3. Clique em **"Create repository"**

### Passo 2: Fazer Upload dos Arquivos

1. Na página do repositório recém-criado, clique em **"uploading an existing file"**
2. Arraste os seguintes arquivos para a área de upload:
   - `logalize.yaml`
   - `README.md`
   - `LICENSE`
   - `.gitignore`
3. Na caixa "Commit changes":
   - Digite: `Initial commit - configuração completa do Logalize`
4. Clique em **"Commit changes"**

✅ **Pronto!** Seu repositório está no ar!

---

## Opção 2: Via Linha de Comando Git 💻

### Pré-requisitos

```bash
# Verificar se git está instalado
git --version

# Se não estiver, instale:
# Ubuntu/Debian: sudo apt install git
# Fedora/RHEL: sudo dnf install git
# macOS: brew install git
```

### Passo 1: Criar o Repositório no GitHub

1. Acesse https://github.com/new
2. **Repository name**: `logalize`
3. **NÃO** adicione README, .gitignore ou license
4. Clique em **"Create repository"**

### Passo 2: Fazer Upload via Git

```bash
# 1. Entre no diretório do repositório
cd /caminho/para/logalize-repo

# 2. Inicialize o git
git init

# 3. Adicione todos os arquivos
git add .

# 4. Faça o primeiro commit
git commit -m "Initial commit - configuração completa do Logalize"

# 5. Adicione o repositório remoto (SUBSTITUA SEU_USUARIO pelo seu username)
git remote add origin https://github.com/SEU_USUARIO/logalize.git

# 6. Configure a branch principal
git branch -M main

# 7. Faça o push
git push -u origin main
```

**Nota**: Você precisará fazer login no GitHub. Use:
- **Username**: seu username do GitHub
- **Password**: seu Personal Access Token (não use a senha da conta)

#### Como criar Personal Access Token:

1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token (classic)
3. Marque: `repo` (Full control of private repositories)
4. Generate token
5. **Copie o token** (você não verá novamente!)

---

## Opção 3: Via GitHub CLI (gh) 🚀

### Instalar GitHub CLI

```bash
# Ubuntu/Debian
sudo apt install gh

# Fedora/RHEL
sudo dnf install gh

# macOS
brew install gh

# Arch Linux
sudo pacman -S github-cli
```

### Fazer Upload

```bash
# 1. Autenticar (só precisa fazer uma vez)
gh auth login

# 2. Entre no diretório
cd /caminho/para/logalize-repo

# 3. Criar repositório e fazer upload (tudo de uma vez!)
gh repo create logalize --public --source=. --push

# Ou se preferir privado:
gh repo create logalize --private --source=. --push
```

---

## 🎉 Após o Upload

Seu repositório estará disponível em:
```
https://github.com/SEU_USUARIO/logalize
```

### Compartilhe com o mundo! 🌍

```bash
# Copie o link do repositório para compartilhar
echo "https://github.com/SEU_USUARIO/logalize"
```

### Atualizações Futuras

Se você fizer alterações nos arquivos:

```bash
cd /caminho/para/logalize-repo

# Adicionar alterações
git add .

# Fazer commit
git commit -m "Descrição das alterações"

# Enviar para o GitHub
git push
```

---

## 📋 Checklist Final

Após fazer upload, verifique se tudo está correto:

- [ ] README.md está aparecendo como página inicial
- [ ] logalize.yaml está presente e visível
- [ ] LICENSE está presente
- [ ] .gitignore está presente
- [ ] A descrição do repositório está correta
- [ ] Os tópicos/tags estão configurados (opcional):
  - `logalize`
  - `logs`
  - `colorizer`
  - `yaml`
  - `configuration`

---

## 🏷️ Adicionar Tópicos/Tags (Opcional)

1. Vá para a página do repositório
2. Clique em ⚙️ (engrenagem) ao lado de "About"
3. Em "Topics", adicione:
   - `logalize`
   - `logs`
   - `log-colorizer`
   - `yaml`
   - `configuration`
   - `syslog`
   - `docker`
   - `kubernetes`

---

## 🎨 Personalizar README

Se quiser adicionar mais informações:

1. Clique no arquivo `README.md` no GitHub
2. Clique no ícone de lápis (✏️) para editar
3. Faça suas alterações
4. Role até o final e clique em "Commit changes"

---

## ❓ Problemas Comuns

### "Permission denied (publickey)"

Configure SSH ou use HTTPS:
```bash
git remote set-url origin https://github.com/SEU_USUARIO/logalize.git
```

### "Authentication failed"

Use Personal Access Token ao invés da senha da conta.

### "Repository not found"

Verifique se o nome do usuário e do repositório estão corretos:
```bash
git remote -v
```

---

## 📞 Precisa de Ajuda?

- [Documentação Git](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [GitHub CLI Docs](https://cli.github.com/manual/)

---

✨ **Boa sorte com seu repositório!**
