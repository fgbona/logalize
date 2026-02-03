# 🚀 Advanced Usage Examples

Practical and advanced examples of how to use Logalize in different scenarios.

## 📊 Multi-Service Monitoring

### Complete System

```bash
# Monitor all system logs in real-time
sudo tail -f /var/log/syslog \
  /var/log/auth.log \
  /var/log/kern.log | logalize -t tokyonight-dark
```

### Complete Web Stack

```bash
# Nginx + PHP-FPM + MySQL
tail -f /var/log/nginx/access.log \
  /var/log/nginx/error.log \
  /var/log/php-fpm/error.log \
  /var/log/mysql/error.log | logalize
```

## 🐳 Docker and Containers

### Docker Compose Multi-Container

```bash
# All containers with colors
docker-compose logs -f --tail=100 | logalize -t dracula
```

### Docker Swarm

```bash
# Service logs in Swarm
docker service logs -f service-name 2>&1 | logalize
```

### Filter and Colorize

```bash
# Only container errors
docker-compose logs -f | grep -i error | logalize
```

## ☸️ Advanced Kubernetes

### Multiple Pods

```bash
# All pods from a deployment
kubectl logs -f deployment/myapp --all-containers=true | logalize

# Pods with label selector
kubectl logs -f -l app=backend,env=production | logalize
```

### Specific Namespace

```bash
# All pods in a namespace
kubectl logs -f --all-containers=true -n production | logalize -t nord
```

### Previous Logs (Crashed Pods)

```bash
# View logs from crashed pod
kubectl logs pod-name --previous | logalize
```

### Stern + Logalize

```bash
# Install stern: https://github.com/stern/stern
stern myapp --color=never | logalize
```

## 🔍 Advanced Search and Filters

### Combining grep, awk and logalize

```bash
# Only 5xx errors from Nginx
grep "\" 5[0-9][0-9] " /var/log/nginx/access.log | logalize

# SSH authentication errors
grep "Failed password" /var/log/auth.log | logalize -t gruvbox-dark

# Specific IPs
awk '/192\.168\.1\./' /var/log/nginx/access.log | logalize
```

### Time-based Filters

```bash
# Logs from last 24 hours (with journalctl)
journalctl --since "24 hours ago" | logalize

# Logs between specific dates
journalctl --since "2024-01-01" --until "2024-01-31" | logalize
```

### Complex Regex

```bash
# Only POST and PUT requests
grep -E "\"(POST|PUT)" /var/log/nginx/access.log | logalize

# Specific Python errors
grep -E "(Exception|Error|Traceback)" /var/log/myapp/app.log | logalize
```

## 📈 Performance Analysis

### Slow Response Times

```bash
# Nginx - requests that took more than 1 second
awk '$NF > 1.0' /var/log/nginx/access.log | logalize
```

### Top IPs

```bash
# 10 most accessed IPs (colorized)
awk '{print $1}' /var/log/nginx/access.log | \
  sort | uniq -c | sort -rn | head -10 | logalize
```

### Status Codes

```bash
# Count status codes and colorize
awk '{print $9}' /var/log/nginx/access.log | \
  sort | uniq -c | sort -rn | logalize
```

## 🔐 Security Analysis

### Failed Login Attempts

```bash
# SSH failed attempts
grep "Failed password" /var/log/auth.log | logalize -t dracula

# With count by IP
grep "Failed password" /var/log/auth.log | \
  awk '{print $(NF-3)}' | sort | uniq -c | sort -rn | logalize
```

### Firewall Logs

```bash
# UFW blocks
grep -i "UFW BLOCK" /var/log/kern.log | logalize

# iptables drops
journalctl -k | grep -i "drop" | logalize
```

## 💾 Saving Colored Logs

### For Later Viewing

```bash
# Save with ANSI colors
tail -1000 /var/log/syslog | logalize > /tmp/syslog-colored.log

# View with less preserving colors
less -R /tmp/syslog-colored.log

# View with cat
cat /tmp/syslog-colored.log
```

### Convert to HTML

```bash
# Using aha (ANSI HTML Adapter)
sudo apt install aha  # or dnf/brew

tail -1000 /var/log/syslog | logalize | aha > logs.html
```

## 🔄 Log Rotation

### Watch + Logalize

```bash
# Update every 2 seconds
watch -c -n 2 "tail -50 /var/log/syslog | logalize"
```

### Monitor Rotating File

```bash
# tail -F (uppercase) follows rotation
tail -F /var/log/syslog | logalize
```

## 📱 Integration with Tmux/Screen

### Tmux Layout

```bash
# Vertical split with different logs
tmux split-window -h
tmux send-keys "tail -f /var/log/nginx/access.log | logalize" Enter
tmux select-pane -L
tail -f /var/log/nginx/error.log | logalize
```

### Monitoring Script

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

## 🎯 Specific Use Cases

### Spring Boot Application

```bash
# Only stacktraces
grep -A 20 "Exception" application.log | logalize

# By log level
grep "WARN\|ERROR" application.log | logalize
```

### PostgreSQL Database

```bash
# Only slow queries
grep "duration:" /var/log/postgresql/postgresql.log | \
  awk '$6 > 1000' | logalize

# Deadlocks
grep -i "deadlock" /var/log/postgresql/postgresql.log | logalize
```

### Redis

```bash
# Monitor executed commands
redis-cli MONITOR | logalize -t catppuccin-mocha
```

### Elasticsearch

```bash
# ES logs
tail -f /var/log/elasticsearch/elasticsearch.log | logalize
```

## 🧪 Development and Debug

### Build Logs

```bash
# Maven
mvn clean install 2>&1 | logalize

# Gradle
./gradlew build 2>&1 | logalize

# npm
npm run build 2>&1 | logalize
```

### Tests

```bash
# pytest with colored output
pytest -v 2>&1 | logalize

# Jest
npm test 2>&1 | logalize
```

### CI/CD Logs

```bash
# Jenkins
curl -u user:token https://jenkins.example.com/job/myjob/lastBuild/consoleText | logalize

# GitHub Actions (local with act)
act -j build 2>&1 | logalize
```

## 🌐 Remote Logs

### SSH + Logalize

```bash
# Remote server logs
ssh user@server "tail -f /var/log/syslog" | logalize

# Multiple servers
for server in server1 server2 server3; do
  ssh $server "tail -f /var/log/nginx/access.log" | \
    sed "s/^/[$server] /" | logalize &
done
```

### Centralized rsyslog

```bash
# Monitor centralized logs
tail -f /var/log/rsyslog/*.log | logalize
```

## 📊 Metrics and Statistics

### Requests per Minute

```bash
# Last 1000 lines from Nginx
tail -1000 /var/log/nginx/access.log | \
  awk '{print $4}' | cut -d: -f1-3 | \
  sort | uniq -c | logalize
```

### Errors per Hour

```bash
# Group errors by hour
grep ERROR application.log | \
  awk '{print $1, $2}' | cut -d: -f1 | \
  sort | uniq -c | logalize
```

## 🔧 Configuration Debugging

### Test Configuration

```bash
# Debug mode to see what's being applied
cat test.log | logalize --debug

# Only formats
cat test.log | logalize --only-formats --debug

# Check if a specific pattern is working
echo "192.168.1.1 example.com" | logalize --only-patterns
```

### Validate YAML

```bash
# Validate file syntax
python3 -c "import yaml; yaml.safe_load(open('logalize.yaml'))"

# Check if file is being loaded
strace logalize < test.log 2>&1 | grep logalize.yaml
```

## 🎨 Advanced Customizations

### Create Custom Theme

```yaml
# In your logalize.yaml
themes:
  my-company-theme:
    default:
      fg: "#FFFFFF"
    
    patterns:
      ipv4-address:
        fg: "#00FF00"  # Corporate green
      
      http-status-code:
        status-2xx:
          fg: "#00AA00"  # Success green
        status-5xx:
          fg: "#FF0000"  # Error red
    
    words:
      good:
        fg: "#00FF00"
        style: bold
      bad:
        fg: "#FF0000"
        style: bold
      
      # Company-specific words
      custom:
        fg: "#FFA500"  # Highlight orange
        style: bold
```

### Custom Format for Specific App

```yaml
formats:
  my-application:
    - regexp: "(\\[\\d{4}-\\d{2}-\\d{2}\\] )"
      name: date
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
      name: module
    - regexp: "(.*)"
      name: message
```

## 💡 Professional Tips

### Useful Aliases

Add to your `.bashrc` or `.zshrc`:

```bash
# Basic aliases
alias lz='logalize'
alias lzd='logalize -t dracula'
alias lzn='logalize -t nord'

# Common logs
alias syslog='tail -f /var/log/syslog | logalize'
alias nginxlog='tail -f /var/log/nginx/access.log | logalize'
alias nginxerr='tail -f /var/log/nginx/error.log | logalize'
alias dockerlog='docker-compose logs -f | logalize'
alias k8slog='kubectl logs -f'

# Function for specific container logs
dlogs() {
  docker logs -f "$1" 2>&1 | logalize
}

# Function for specific pod logs
klogs() {
  kubectl logs -f "$1" | logalize
}
```

### Useful Scripts

```bash
#!/bin/bash
# log-summary.sh - Daily log summary

echo "=== Log Summary ==="
echo

echo "Top 10 IPs:"
awk '{print $1}' /var/log/nginx/access.log | \
  sort | uniq -c | sort -rn | head -10 | logalize
echo

echo "Status Codes:"
awk '{print $9}' /var/log/nginx/access.log | \
  sort | uniq -c | sort -rn | logalize
echo

echo "System Errors:"
grep -i "error\|fail\|critical" /var/log/syslog | tail -20 | logalize
```

---

## 📚 More Resources

- [Official Logalize Documentation](https://github.com/deponian/logalize)
- [Regex for Logs](https://regex101.com/)
- [YAML Validator](https://www.yamllint.com/)

---

✨ **Contribute with your examples!** Open a PR with your favorite use cases.
