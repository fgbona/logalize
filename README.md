# Logalize - Configuração Completa 🎨

> Arquivo de configuração completo e otimizado para o [Logalize](https://github.com/deponian/logalize) - colorador de logs rápido e extensível

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![YAML](https://img.shields.io/badge/YAML-Valid-brightgreen.svg)]()

## 📋 Sobre

Este repositório contém um arquivo de configuração **completo, testado e funcional** para o Logalize, incluindo:

- ✅ **15+ formatos de logs** predefinidos
- ✅ **40+ padrões** de detecção (IPs, URLs, timestamps, etc)
- ✅ **100+ palavras** categorizadas (success, error, warning, etc)
- ✅ **6 temas** de cores prontos para uso
- ✅ **Totalmente documentado** com comentários em português

## 🚀 Instalação Rápida

### 1. Instale o Logalize

#### Ubuntu/Debian
```bash
sudo dpkg -i logalize_X.X.X_linux_amd64.deb
```

#### Fedora/RHEL/CentOS
```bash
sudo rpm -i logalize_X.X.X_linux_amd64.rpm
```

#### Arch Linux
```bash
sudo pacman -U logalize_X.X.X_linux_amd64.pkg.tar.zst
# ou via AUR
yay -S logalize-bin
```

#### macOS
```bash
brew install deponian/tap/logalize
```

#### Go
```bash
go install github.com/deponian/logalize@latest
```

### 2. Configure o Logalize

```bash
# Clone este repositório
git clone https://github.com/SEU_USUARIO/logalize.git
cd logalize

# Copie a configuração para o local correto
mkdir -p ~/.config/logalize
cp logalize.yaml ~/.config/logalize/

# Ou use configuração global
sudo mkdir -p /etc/logalize
sudo cp logalize.yaml /etc/logalize/
```

### 3. Teste!

```bash
# Teste com seus logs
tail -f /var/log/syslog | logalize
cat /var/log/nginx/access.log | logalize
journalctl -f | logalize
```

## 📦 O que está incluído

### 🎯 **Formatos Completos (15)**

Formatos predefinidos para logs estruturados:

- **Apache/Nginx** - Access logs em formato combinado
- **Syslog** - Formato padrão do sistema
- **Systemd Journal** - Logs do systemd
- **Docker Compose** - Logs de containers
- **Kubernetes** - Logs de pods e containers
- **Spring Boot** - Logs de aplicações Java
- **Python/Django** - Logs de aplicações Python
- **PostgreSQL** - Logs do banco de dados
- **MySQL/MariaDB** - Logs do banco de dados
- **Nginx Error** - Logs de erro do Nginx
- **Redis** - Logs do Redis
- **Logfmt** - Formato usado por Prometheus/Grafana

### 🔍 **Padrões de Detecção (40+)**

Padrões que são detectados em qualquer parte da linha:

#### Endereços e URLs
- ✅ IPv4 (com e sem porta)
- ✅ IPv6
- ✅ URLs (http/https)
- ✅ Domínios
- ✅ E-mails

#### Timestamps e Datas
- ✅ ISO8601 (2024-01-10T14:23:45.123Z)
- ✅ Data com barra (2024/01/10)
- ✅ Data com hífen (2024-01-10)
- ✅ Hora 24h (14:23:45.123)
- ✅ Unix timestamp

#### Identificadores
- ✅ UUID (8-4-4-4-12)
- ✅ GUID ({8-4-4-4-12})
- ✅ Hash MD5 (32 caracteres hex)
- ✅ Hash SHA1 (40 caracteres hex)
- ✅ Hash SHA256 (64 caracteres hex)

#### HTTP
- ✅ Métodos HTTP (GET, POST, PUT, etc)
- ✅ Status codes (200, 404, 500, etc)

#### Filesystem
- ✅ Caminhos Unix (/var/log/syslog)
- ✅ Caminhos Windows (C:\Windows\System32)
- ✅ Extensões de arquivo (.log, .txt)

#### Números
- ✅ Inteiros
- ✅ Decimais
- ✅ Hexadecimais (0xFF)
- ✅ Percentagens (85%)
- ✅ Tamanhos de memória (1.5GB, 256MB)

#### Código e Tech
- ✅ Strings ("texto" ou 'texto')
- ✅ Log levels (DEBUG, INFO, WARN, ERROR)
- ✅ Chaves JSON ("key":)
- ✅ Atribuições de variáveis (var=)
- ✅ Chamadas de função (func())
- ✅ Palavras-chave SQL
- ✅ IDs de containers
- ✅ Namespaces do Kubernetes

#### Segurança
- ✅ JWT tokens
- ✅ API keys

### 📝 **Palavras Categorizadas (100+)**

O Logalize detecta automaticamente palavras e suas formas flexionadas:

#### ✅ Boas (Verde/Positivo)
- accept, active, allow, authenticate, authorized
- complete, connect, enabled, established, granted
- healthy, initialize, listening, loaded, mounted
- online, ready, running, success, valid, verified
- E mais 30+ palavras...

#### ❌ Ruins (Vermelho/Negativo)
- abort, block, broken, cancel, crash, critical
- dead, denied, disconnect, error, fail, fatal
- forbidden, invalid, kill, panic, refuse, reject
- stop, terminate, timeout, unauthorized, unstable
- E mais 40+ palavras...

#### 🔄 Ações (Azul/Neutro)
- create, delete, deploy, execute, install
- load, migrate, process, restart, update, upgrade

#### 💻 Tecnologias (Roxo)
- docker, kubernetes, k8s, redis, postgres
- nginx, apache, elasticsearch, kafka, mongodb
- aws, azure, gcp, github, gitlab

#### 🎨 Customizadas
- Adicione suas próprias palavras aqui!

### 🎨 **Temas de Cores (6)**

Temas profissionais prontos para uso:

1. **TokyoNight Dark** ⭐ (Padrão)
   - Moderno e elegante
   - Ótimo contraste
   - Suave para os olhos

2. **Catppuccin Mocha** ☕
   - Paleta suave e confortável
   - Cores pastéis
   - Muito popular

3. **Nord** ❄️
   - Tema polar minimalista
   - Cores frias
   - Design escandinavo

4. **Dracula** 🧛
   - Tema escuro popular
   - Alto contraste
   - Cores vibrantes

5. **Gruvbox Dark** 🎨
   - Tema retrô
   - Cores quentes
   - Confortável para longas sessões

6. **Solarized Dark** 🌅
   - Clássico design solarized
   - Cientificamente balanceado
   - Cores harmoniosas

## 🎯 Exemplos de Uso

### Logs do Sistema

```bash
# Syslog em tempo real
tail -f /var/log/syslog | logalize

# Journalctl
journalctl -f | logalize
journalctl -u nginx.service -f | logalize
journalctl -xe | logalize
```

### Servidores Web

```bash
# Apache
tail -f /var/log/apache2/access.log | logalize
tail -f /var/log/apache2/error.log | logalize

# Nginx
tail -f /var/log/nginx/access.log | logalize
tail -f /var/log/nginx/error.log | logalize
```

### Bancos de Dados

```bash
# PostgreSQL
tail -f /var/log/postgresql/postgresql-14-main.log | logalize

# MySQL
tail -f /var/log/mysql/error.log | logalize

# Redis
tail -f /var/log/redis/redis-server.log | logalize
```

### Containers e Kubernetes

```bash
# Docker
docker logs -f container-name 2>&1 | logalize
docker-compose logs -f | logalize

# Kubernetes
kubectl logs -f deployment/myapp | logalize
kubectl logs -f -l app=myapp --all-containers=true | logalize
kubectl logs -f pod/myapp-pod -c container-name | logalize
```

### Aplicações

```bash
# Spring Boot / Java
tail -f application.log | logalize
java -jar app.jar | logalize

# Python / Django
tail -f django.log | logalize
python manage.py runserver 2>&1 | logalize

# Logs gerais de aplicação
tail -f /var/log/myapp/app.log | logalize
```

### Com Temas Específicos

```bash
# Usar tema Dracula
cat logs.txt | logalize -t dracula

# Usar tema Nord
tail -f /var/log/syslog | logalize -t nord

# Usar tema Gruvbox
journalctl -f | logalize -t gruvbox-dark
```

### Arquivos de Log

```bash
# Ler arquivo completo
cat /var/log/syslog | logalize

# Últimas 100 linhas
tail -n 100 /var/log/nginx/access.log | logalize

# Procurar e colorir
grep "error" /var/log/syslog | logalize
```

## ⚙️ Comandos Úteis

### Listar Temas

```bash
# Ver todos os temas disponíveis
logalize -T
logalize --list-themes
```

### Usar Configuração Customizada

```bash
# Especificar arquivo de configuração
cat logs.txt | logalize -c /caminho/para/logalize.yaml
cat logs.txt | logalize --config custom-config.yaml
```

### Modos de Operação

```bash
# Usar apenas formatos (ignorar padrões e palavras)
cat logs.txt | logalize --only-formats

# Usar apenas padrões
cat logs.txt | logalize --only-patterns

# Usar apenas palavras
cat logs.txt | logalize --only-words

# Desabilitar todos os builtins
cat logs.txt | logalize -N
cat logs.txt | logalize --no-builtins
```

### Debug e Testes

```bash
# Modo debug (ver o que está sendo aplicado)
cat logs.txt | logalize --debug

# Dry-run (processar sem colorir)
cat logs.txt | logalize --dry-run
```

## 🛠️ Customização

### Adicionar Palavras Customizadas

Edite o arquivo `logalize.yaml` e adicione suas palavras na seção `words.custom`:

```yaml
words:
  custom:
    - "minha-aplicacao"
    - "meu-servico"
    - "palavra-especial"
    - "empresa-xyz"
```

### Criar Formato Personalizado

Adicione um novo formato na seção `formats`:

```yaml
formats:
  meu-formato:
    - regexp: "(\\d{4}-\\d{2}-\\d{2} )"
      name: data
    - regexp: "([A-Z]+) "
      name: nivel
    - regexp: "\\[([^\\]]+)\\] "
      name: modulo
    - regexp: "(.*)"
      name: mensagem
```

### Customizar Cores de um Tema

Modifique as cores em hexadecimal (#RRGGBB) ou ANSI (0-255):

```yaml
themes:
  tokyonight-dark:
    patterns:
      ipv4-address:
        fg: "#ff0000"  # vermelho
        bg: "#000000"  # fundo preto
        style: bold    # negrito
```

### Estilos Disponíveis

- `bold` - negrito
- `faint` - esmaecido
- `italic` - itálico
- `underline` - sublinhado
- `overline` - linha superior
- `crossout` - riscado
- `reverse` - inverter cores foreground/background
- `patterns` - aplicar padrões de cores
- `words` - aplicar coloração de palavras
- `patterns-and-words` - aplicar ambos

## 📚 Estrutura do Arquivo

```yaml
settings:           # Configurações gerais
  theme: "..."      # Tema padrão
  debug: false      # Modo debug
  # ... outras opções

formats:            # Formatos completos de log
  apache-access-log:
    - regexp: "..."
      name: "..."
  # ... mais formatos

patterns:           # Padrões de detecção
  ipv4-address:
    priority: 100
    regexp: "..."
  # ... mais padrões

words:              # Palavras categorizadas
  good:
    - "success"
    - "complete"
  bad:
    - "error"
    - "fail"
  # ... mais categorias

themes:             # Temas de cores
  tokyonight-dark:
    default:
      fg: "..."
    patterns:
      # ... cores dos padrões
    words:
      # ... cores das palavras
  # ... mais temas
```

## 🔧 Solução de Problemas

### Validar Arquivo YAML

```bash
# Verificar se o YAML está válido
python3 -c "import yaml; yaml.safe_load(open('logalize.yaml'))"
```

### Nenhuma Colorização Aparece

```bash
# Verifique se o arquivo está sendo encontrado
logalize --debug < arquivo.log

# Teste com formatos apenas
logalize --only-formats < arquivo.log

# Teste com padrões apenas
logalize --only-patterns < arquivo.log
```

### Cores Não Aparecem no Terminal

```bash
# Verifique o suporte a cores
echo $TERM

# Force saída colorida
export FORCE_COLOR=1
cat logs.txt | logalize
```

### Arquivo de Configuração Não Encontrado

O Logalize procura configurações nesta ordem:
1. `/etc/logalize/logalize.yaml`
2. `~/.config/logalize/logalize.yaml`
3. `.logalize.yaml` (no diretório atual)
4. Caminho especificado com `-c/--config`

```bash
# Use caminho específico
logalize -c /caminho/completo/para/logalize.yaml < logs.txt
```

## 💡 Dicas e Truques

### 1. Performance

Para logs muito grandes, use `--only-formats` para melhor performance:

```bash
tail -f huge.log | logalize --only-formats
```

### 2. Integração com Pipelines

```bash
# Combinar com grep
grep "error" /var/log/syslog | logalize

# Combinar com awk
awk '/failed/' /var/log/auth.log | logalize

# Combinar com sed
sed -n '100,200p' app.log | logalize
```

### 3. Salvar Output Colorido

```bash
# Salvar com cores ANSI
tail -f /var/log/syslog | logalize > colorido.log

# Ver depois com less (preserva cores)
less -R colorido.log
```

### 4. Múltiplos Arquivos

```bash
# Colorir múltiplos arquivos
cat /var/log/syslog /var/log/auth.log | logalize

# Todos os logs de um diretório
cat /var/log/*.log | logalize
```

### 5. Monitoramento em Tempo Real

```bash
# Com atualização de título do terminal
watch -c "tail -n 50 /var/log/syslog | logalize"

# Múltiplos terminais com tmux/screen
tmux split-window "tail -f /var/log/nginx/access.log | logalize"
```

## 📖 Documentação Oficial

- **Projeto Original**: [deponian/logalize](https://github.com/deponian/logalize)
- **Documentação**: [README oficial](https://github.com/deponian/logalize/blob/main/readme.md)
- **Issues**: [Reportar problemas](https://github.com/deponian/logalize/issues)

## 🤝 Contribuindo

Encontrou um bug ou tem uma sugestão? Sinta-se à vontade para:

1. Abrir uma [Issue](https://github.com/SEU_USUARIO/logalize/issues)
2. Enviar um Pull Request
3. Compartilhar suas configurações customizadas

## 📄 Licença

Este arquivo de configuração está sob a licença MIT. O Logalize original também usa a licença MIT.

## ⭐ Agradecimentos

- **[@deponian](https://github.com/deponian)** - Criador do Logalize
- **[@emptysad](https://github.com/emptysad)** - Nome e ideia do logo
- **[@ekivoka](https://github.com/ekivoka)** - Design e testes

## 📞 Suporte

Precisa de ajuda? 

- 📖 Leia a [documentação oficial](https://github.com/deponian/logalize)
- 🐛 Reporte bugs nas [Issues](https://github.com/deponian/logalize/issues)
- 💬 Discussões na [comunidade](https://github.com/deponian/logalize/discussions)

---

**Feito com ❤️ para a comunidade Logalize**

⭐ Se este repositório foi útil, deixe uma estrela!
