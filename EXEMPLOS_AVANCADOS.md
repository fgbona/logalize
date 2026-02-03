# 🚀 Exemplos Avançados de Uso

Exemplos práticos e avançados de como usar o Logalize em diferentes cenários.

## 📊 Monitoramento de Múltiplos Serviços

### Sistema Completo

```bash
# Monitorar todos os logs do sistema em tempo real
sudo tail -f /var/log/syslog \
  /var/log/auth.log \
  /var/log/kern.log | logalize -t tokyonight-dark
```

### Web Stack Completo

```bash
# Nginx + PHP-FPM + MySQL
tail -f /var/log/nginx/access.log \
  /var/log/nginx/error.log \
  /var/log/php-fpm/error.log \
  /var/log/mysql/error.log | logalize
```

## 🐳 Docker e Containers

### Docker Compose Multi-Container

```bash
# Todos os containers com cores
docker-compose logs -f --tail=100 | logalize -t dracula
```

### Docker Swarm

```bash
# Logs de um serviço no Swarm
docker service logs -f service-name 2>&1 | logalize
```

### Filtrar e Colorir

```bash
# Apenas erros de containers
docker-compose logs -f | grep -i error | logalize
```

## ☸️ Kubernetes Avançado

### Múltiplos Pods

```bash
# Todos os pods de um deployment
kubectl logs -f deployment/myapp --all-containers=true | logalize

# Pods com selector de label
kubectl logs -f -l app=backend,env=production | logalize
```

### Namespace Específico

```bash
# Todos os pods em um namespace
kubectl logs -f --all-containers=true -n production | logalize -t nord
```

### Logs Anteriores (Crashed Pods)

```bash
# Ver logs de pod que crashou
kubectl logs pod-name --previous | logalize
```

### Stern + Logalize

```bash
# Instalar stern: https://github.com/stern/stern
stern myapp --color=never | logalize
```

## 🔍 Busca e Filtros Avançados

### Combinando grep, awk e logalize

```bash
# Apenas erros 5xx do Nginx
grep "\" 5[0-9][0-9] " /var/log/nginx/access.log | logalize

# Erros de autenticação SSH
grep "Failed password" /var/log/auth.log | logalize -t gruvbox-dark

# IPs específicos
awk '/192\.168\.1\./' /var/log/nginx/access.log | logalize
```

### Filtros por Tempo

```bash
# Logs das últimas 24 horas (com journalctl)
journalctl --since "24 hours ago" | logalize

# Logs entre datas específicas
journalctl --since "2024-01-01" --until "2024-01-31" | logalize
```

### Regex Complexos

```bash
# Apenas requisições POST e PUT
grep -E "\"(POST|PUT)" /var/log/nginx/access.log | logalize

# Erros específicos de Python
grep -E "(Exception|Error|Traceback)" /var/log/myapp/app.log | logalize
```

## 📈 Análise de Performance

### Tempos de Resposta Lentos

```bash
# Nginx - requisições que levaram mais de 1 segundo
awk '$NF > 1.0' /var/log/nginx/access.log | logalize
```

### Top IPs

```bash
# 10 IPs que mais acessaram (colorido)
awk '{print $1}' /var/log/nginx/access.log | \
  sort | uniq -c | sort -rn | head -10 | logalize
```

### Status Codes

```bash
# Contar status codes e colorir
awk '{print $9}' /var/log/nginx/access.log | \
  sort | uniq -c | sort -rn | logalize
```

## 🔐 Análise de Segurança

### Tentativas de Login Falhadas

```bash
# SSH failed attempts
grep "Failed password" /var/log/auth.log | logalize -t dracula

# Com contagem por IP
grep "Failed password" /var/log/auth.log | \
  awk '{print $(NF-3)}' | sort | uniq -c | sort -rn | logalize
```

### Logs de Firewall

```bash
# UFW blocks
grep -i "UFW BLOCK" /var/log/kern.log | logalize

# iptables drops
journalctl -k | grep -i "drop" | logalize
```

## 💾 Salvando Logs Coloridos

### Para Visualização Posterior

```bash
# Salvar com cores ANSI
tail -1000 /var/log/syslog | logalize > /tmp/syslog-colorido.log

# Ver com less preservando cores
less -R /tmp/syslog-colorido.log

# Ver com cat
cat /tmp/syslog-colorido.log
```

### Converter para HTML

```bash
# Usando aha (ANSI HTML Adapter)
sudo apt install aha  # ou dnf/brew

tail -1000 /var/log/syslog | logalize | aha > logs.html
```

## 🔄 Rotação de Logs

### Watch + Logalize

```bash
# Atualizar a cada 2 segundos
watch -c -n 2 "tail -50 /var/log/syslog | logalize"
```

### Monitorar Arquivo que Rotaciona

```bash
# tail -F (maiúsculo) acompanha rotação
tail -F /var/log/syslog | logalize
```

## 📱 Integração com Tmux/Screen

### Tmux Layout

```bash
# Split vertical com diferentes logs
tmux split-window -h
tmux send-keys "tail -f /var/log/nginx/access.log | logalize" Enter
tmux select-pane -L
tail -f /var/log/nginx/error.log | logalize
```

### Script de Monitoramento

```bash
#!/bin/bash
# monitor-logs.sh

tmux new-session -d -s logs

# Pane 1: Nginx Access
tmux send-keys "tail -f /var/log/nginx/access.log | logalize -t tokyonight-dark" Enter

# Pane 2: Nginx Error
tmux split-window -v
tmux send-keys "tail -f /var/log/nginx/error.log | logalize -t tokyonight-dark" Enter

# Pane 3: Syslog
tmux split-window -h
tmux send-keys "tail -f /var/log/syslog | logalize -t tokyonight-dark" Enter

# Pane 4: Docker
tmux select-pane -t 0
tmux split-window -h
tmux send-keys "docker-compose logs -f | logalize -t tokyonight-dark" Enter

# Attach
tmux attach-session -t logs
```

## 🎯 Casos de Uso Específicos

### Aplicação Spring Boot

```bash
# Apenas stacktraces
grep -A 20 "Exception" application.log | logalize

# Por nível de log
grep "WARN\|ERROR" application.log | logalize
```

### Banco de Dados PostgreSQL

```bash
# Apenas queries lentas
grep "duration:" /var/log/postgresql/postgresql.log | \
  awk '$6 > 1000' | logalize

# Deadlocks
grep -i "deadlock" /var/log/postgresql/postgresql.log | logalize
```

### Redis

```bash
# Monitorar comandos executados
redis-cli MONITOR | logalize -t catppuccin-mocha
```

### Elasticsearch

```bash
# Logs do ES
tail -f /var/log/elasticsearch/elasticsearch.log | logalize
```

## 🧪 Desenvolvimento e Debug

### Logs de Build

```bash
# Maven
mvn clean install 2>&1 | logalize

# Gradle
./gradlew build 2>&1 | logalize

# npm
npm run build 2>&1 | logalize
```

### Testes

```bash
# pytest com output colorido
pytest -v 2>&1 | logalize

# Jest
npm test 2>&1 | logalize
```

### CI/CD Logs

```bash
# Jenkins
curl -u user:token https://jenkins.example.com/job/myjob/lastBuild/consoleText | logalize

# GitHub Actions (local com act)
act -j build 2>&1 | logalize
```

## 🌐 Logs Remotos

### SSH + Logalize

```bash
# Logs de servidor remoto
ssh user@server "tail -f /var/log/syslog" | logalize

# Múltiplos servidores
for server in server1 server2 server3; do
  ssh $server "tail -f /var/log/nginx/access.log" | \
    sed "s/^/[$server] /" | logalize &
done
```

### rsyslog Centralizado

```bash
# Monitorar logs centralizados
tail -f /var/log/rsyslog/*.log | logalize
```

## 📊 Métricas e Estatísticas

### Requests por Minuto

```bash
# Últimas 1000 linhas do Nginx
tail -1000 /var/log/nginx/access.log | \
  awk '{print $4}' | cut -d: -f1-3 | \
  sort | uniq -c | logalize
```

### Erros por Hora

```bash
# Agrupar erros por hora
grep ERROR application.log | \
  awk '{print $1, $2}' | cut -d: -f1 | \
  sort | uniq -c | logalize
```

## 🔧 Debugging de Configuração

### Testar Configuração

```bash
# Modo debug para ver o que está sendo aplicado
cat test.log | logalize --debug

# Apenas formatos
cat test.log | logalize --only-formats --debug

# Ver se um padrão específico está funcionando
echo "192.168.1.1 example.com" | logalize --only-patterns
```

### Validar YAML

```bash
# Validar sintaxe do arquivo
python3 -c "import yaml; yaml.safe_load(open('logalize.yaml'))"

# Verificar se arquivo está sendo carregado
strace logalize < test.log 2>&1 | grep logalize.yaml
```

## 🎨 Customizações Avançadas

### Criar Tema Personalizado

```yaml
# No seu logalize.yaml
themes:
  meu-tema-empresa:
    default:
      fg: "#FFFFFF"
    
    patterns:
      ipv4-address:
        fg: "#00FF00"  # Verde corporativo
      
      http-status-code:
        status-2xx:
          fg: "#00AA00"  # Verde sucesso
        status-5xx:
          fg: "#FF0000"  # Vermelho erro
    
    words:
      good:
        fg: "#00FF00"
        style: bold
      bad:
        fg: "#FF0000"
        style: bold
      
      # Palavras específicas da empresa
      custom:
        fg: "#FFA500"  # Laranja destaque
        style: bold
```

### Formato Customizado para App Específico

```yaml
formats:
  minha-aplicacao:
    - regexp: "(\\[\\d{4}-\\d{2}-\\d{2}\\] )"
      name: data
    - regexp: "(\\[APP\\] )"
      name: prefix
    - regexp: "([A-Z]+) "
      name: level
      alternatives:
        - regexp: "(INFO) "
          name: info
        - regexp: "(ERROR) "
          name: error
    - regexp: "\\[([^\\]]+)\\] "
      name: modulo
    - regexp: "(.*)"
      name: mensagem
```

## 💡 Dicas Profissionais

### Alias Úteis

Adicione ao seu `.bashrc` ou `.zshrc`:

```bash
# Alias básicos
alias lz='logalize'
alias lzd='logalize -t dracula'
alias lzn='logalize -t nord'

# Logs comuns
alias syslog='tail -f /var/log/syslog | logalize'
alias nginxlog='tail -f /var/log/nginx/access.log | logalize'
alias nginxerr='tail -f /var/log/nginx/error.log | logalize'
alias dockerlog='docker-compose logs -f | logalize'
alias k8slog='kubectl logs -f'

# Função para logs de um container específico
dlogs() {
  docker logs -f "$1" 2>&1 | logalize
}

# Função para logs de um pod específico
klogs() {
  kubectl logs -f "$1" | logalize
}
```

### Scripts Úteis

```bash
#!/bin/bash
# log-summary.sh - Resumo diário de logs

echo "=== Resumo de Logs ==="
echo

echo "Top 10 IPs:"
awk '{print $1}' /var/log/nginx/access.log | \
  sort | uniq -c | sort -rn | head -10 | logalize
echo

echo "Status Codes:"
awk '{print $9}' /var/log/nginx/access.log | \
  sort | uniq -c | sort -rn | logalize
echo

echo "Erros do Sistema:"
grep -i "error\|fail\|critical" /var/log/syslog | tail -20 | logalize
```

---

## 📚 Mais Recursos

- [Documentação Oficial do Logalize](https://github.com/deponian/logalize)
- [Regex para Logs](https://regex101.com/)
- [YAML Validator](https://www.yamllint.com/)

---

✨ **Contribua com seus exemplos!** Abra um PR com seus casos de uso favoritos.
