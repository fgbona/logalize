# Logalize - Complete Configuration 🎨

> Complete and optimized configuration file for [Logalize](https://github.com/deponian/logalize) - fast and extensible log colorizer

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![YAML](https://img.shields.io/badge/YAML-Valid-brightgreen.svg)]()

## 📋 About

This repository contains a **complete, tested, and functional** configuration file for Logalize, including:

- ✅ **15+ predefined log formats**
- ✅ **40+ detection patterns** (IPs, URLs, timestamps, etc)
- ✅ **100+ categorized words** (success, error, warning, etc)
- ✅ **6 ready-to-use color themes**
- ✅ **Fully documented** with comments in Portuguese

## 🚀 Quick Installation

### 1. Install Logalize

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
# or via AUR
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

### 2. Configure Logalize

```bash
# Clone this repository
git clone https://github.com/fgbona/logalize.git
cd logalize

# Copy configuration to the correct location
mkdir -p ~/.config/logalize
cp logalize.yaml ~/.config/logalize/

# Or use global configuration
sudo mkdir -p /etc/logalize
sudo cp logalize.yaml /etc/logalize/
```

### 3. Test!

```bash
# Test with your logs
tail -f /var/log/syslog | logalize
cat /var/log/nginx/access.log | logalize
journalctl -f | logalize
```

## 📦 What's Included

### 🎯 **Complete Formats (15)**

Predefined formats for structured logs:

- **Apache/Nginx** - Access logs in combined format
- **Syslog** - Standard system format
- **Systemd Journal** - Systemd logs
- **Docker Compose** - Container logs
- **Kubernetes** - Pod and container logs
- **Spring Boot** - Java application logs
- **Python/Django** - Python application logs
- **PostgreSQL** - Database logs
- **MySQL/MariaDB** - Database logs
- **Nginx Error** - Nginx error logs
- **Redis** - Redis logs
- **Logfmt** - Format used by Prometheus/Grafana

### 🔍 **Detection Patterns (40+)**

Patterns detected anywhere in the line:

#### Addresses and URLs
- ✅ IPv4 (with and without port)
- ✅ IPv6
- ✅ URLs (http/https)
- ✅ Domains
- ✅ Emails

#### Timestamps and Dates
- ✅ ISO8601 (2024-01-10T14:23:45.123Z)
- ✅ Slash date format (2024/01/10)
- ✅ Dash date format (2024-01-10)
- ✅ 24h time (14:23:45.123)
- ✅ Unix timestamp

#### Identifiers
- ✅ UUID (8-4-4-4-12)
- ✅ GUID ({8-4-4-4-12})
- ✅ MD5 hash (32 hex characters)
- ✅ SHA1 hash (40 hex characters)
- ✅ SHA256 hash (64 hex characters)

#### HTTP
- ✅ HTTP methods (GET, POST, PUT, etc)
- ✅ Status codes (200, 404, 500, etc)

#### Filesystem
- ✅ Unix paths (/var/log/syslog)
- ✅ Windows paths (C:\Windows\System32)
- ✅ File extensions (.log, .txt)

#### Numbers
- ✅ Integers
- ✅ Decimals
- ✅ Hexadecimals (0xFF)
- ✅ Percentages (85%)
- ✅ Memory sizes (1.5GB, 256MB)

#### Code and Tech
- ✅ Strings ("text" or 'text')
- ✅ Log levels (DEBUG, INFO, WARN, ERROR)
- ✅ JSON keys ("key":)
- ✅ Variable assignments (var=)
- ✅ Function calls (func())
- ✅ SQL keywords
- ✅ Container IDs
- ✅ Kubernetes namespaces

#### Security
- ✅ JWT tokens
- ✅ API keys

### 📝 **Categorized Words (100+)**

Logalize automatically detects words and their inflected forms:

#### ✅ Good (Green/Positive)
- accept, active, allow, authenticate, authorized
- complete, connect, enabled, established, granted
- healthy, initialize, listening, loaded, mounted
- online, ready, running, success, valid, verified
- And 30+ more words...

#### ❌ Bad (Red/Negative)
- abort, block, broken, cancel, crash, critical
- dead, denied, disconnect, error, fail, fatal
- forbidden, invalid, kill, panic, refuse, reject
- stop, terminate, timeout, unauthorized, unstable
- And 40+ more words...

#### 🔄 Actions (Blue/Neutral)
- create, delete, deploy, execute, install
- load, migrate, process, restart, update, upgrade

#### 💻 Technologies (Purple)
- docker, kubernetes, k8s, redis, postgres
- nginx, apache, elasticsearch, kafka, mongodb
- aws, azure, gcp, github, gitlab

#### 🎨 Custom
- Add your own words here!

### 🎨 **Color Themes (6)**

Professional themes ready to use:

1. **TokyoNight Dark** ⭐ (Default)
   - Modern and elegant
   - Great contrast
   - Easy on the eyes

2. **Catppuccin Mocha** ☕
   - Soft and comfortable palette
   - Pastel colors
   - Very popular

3. **Nord** ❄️
   - Minimalist polar theme
   - Cool colors
   - Scandinavian design

4. **Dracula** 🧛
   - Popular dark theme
   - High contrast
   - Vibrant colors

5. **Gruvbox Dark** 🎨
   - Retro theme
   - Warm colors
   - Comfortable for long sessions

6. **Solarized Dark** 🌅
   - Classic solarized design
   - Scientifically balanced
   - Harmonious colors

## 🎯 Usage Examples

### System Logs

```bash
# Real-time syslog
tail -f /var/log/syslog | logalize

# Journalctl
journalctl -f | logalize
journalctl -u nginx.service -f | logalize
journalctl -xe | logalize
```

### Web Servers

```bash
# Apache
tail -f /var/log/apache2/access.log | logalize
tail -f /var/log/apache2/error.log | logalize

# Nginx
tail -f /var/log/nginx/access.log | logalize
tail -f /var/log/nginx/error.log | logalize
```

### Databases

```bash
# PostgreSQL
tail -f /var/log/postgresql/postgresql-14-main.log | logalize

# MySQL
tail -f /var/log/mysql/error.log | logalize

# Redis
tail -f /var/log/redis/redis-server.log | logalize
```

### Containers and Kubernetes

```bash
# Docker
docker logs -f container-name 2>&1 | logalize
docker-compose logs -f | logalize

# Kubernetes
kubectl logs -f deployment/myapp | logalize
kubectl logs -f -l app=myapp --all-containers=true | logalize
kubectl logs -f pod/myapp-pod -c container-name | logalize
```

### Applications

```bash
# Spring Boot / Java
tail -f application.log | logalize
java -jar app.jar | logalize

# Python / Django
tail -f django.log | logalize
python manage.py runserver 2>&1 | logalize

# General application logs
tail -f /var/log/myapp/app.log | logalize
```

### With Specific Themes

```bash
# Use Dracula theme
cat logs.txt | logalize -t dracula

# Use Nord theme
tail -f /var/log/syslog | logalize -t nord

# Use Gruvbox theme
journalctl -f | logalize -t gruvbox-dark
```

### Log Files

```bash
# Read complete file
cat /var/log/syslog | logalize

# Last 100 lines
tail -n 100 /var/log/nginx/access.log | logalize

# Search and colorize
grep "error" /var/log/syslog | logalize
```

## ⚙️ Useful Commands

### List Themes

```bash
# View all available themes
logalize -T
logalize --list-themes
```

### Use Custom Configuration

```bash
# Specify configuration file
cat logs.txt | logalize -c /path/to/logalize.yaml
cat logs.txt | logalize --config custom-config.yaml
```

### Operation Modes

```bash
# Use only formats (ignore patterns and words)
cat logs.txt | logalize --only-formats

# Use only patterns
cat logs.txt | logalize --only-patterns

# Use only words
cat logs.txt | logalize --only-words

# Disable all builtins
cat logs.txt | logalize -N
cat logs.txt | logalize --no-builtins
```

### Debug and Testing

```bash
# Debug mode (see what's being applied)
cat logs.txt | logalize --debug

# Dry-run (process without coloring)
cat logs.txt | logalize --dry-run
```

## 🛠️ Customization

### Add Custom Words

Edit the `logalize.yaml` file and add your words in the `words.custom` section:

```yaml
words:
  custom:
    - "my-application"
    - "my-service"
    - "special-word"
    - "company-xyz"
```

### Create Custom Format

Add a new format in the `formats` section:

```yaml
formats:
  my-format:
    - regexp: "(\\d{4}-\\d{2}-\\d{2} )"
      name: date
    - regexp: "([A-Z]+) "
      name: level
    - regexp: "\\[([^\\]]+)\\] "
      name: module
    - regexp: "(.*)"
      name: message
```

### Customize Theme Colors

Modify colors in hexadecimal (#RRGGBB) or ANSI (0-255):

```yaml
themes:
  tokyonight-dark:
    patterns:
      ipv4-address:
        fg: "#ff0000"  # red
        bg: "#000000"  # black background
        style: bold    # bold
```

### Available Styles

- `bold` - bold
- `faint` - faint
- `italic` - italic
- `underline` - underline
- `overline` - overline
- `crossout` - strikethrough
- `reverse` - reverse foreground/background colors
- `patterns` - apply color patterns
- `words` - apply word coloring
- `patterns-and-words` - apply both

## 📚 File Structure

```yaml
settings:           # General settings
  theme: "..."      # Default theme
  debug: false      # Debug mode
  # ... other options

formats:            # Complete log formats
  apache-access-log:
    - regexp: "..."
      name: "..."
  # ... more formats

patterns:           # Detection patterns
  ipv4-address:
    priority: 100
    regexp: "..."
  # ... more patterns

words:              # Categorized words
  good:
    - "success"
    - "complete"
  bad:
    - "error"
    - "fail"
  # ... more categories

themes:             # Color themes
  tokyonight-dark:
    default:
      fg: "..."
    patterns:
      # ... pattern colors
    words:
      # ... word colors
  # ... more themes
```

## 🔧 Troubleshooting

### Validate YAML File

```bash
# Check if YAML is valid
python3 -c "import yaml; yaml.safe_load(open('logalize.yaml'))"
```

### No Colorization Appears

```bash
# Check if file is being found
logalize --debug < file.log

# Test with formats only
logalize --only-formats < file.log

# Test with patterns only
logalize --only-patterns < file.log
```

### Colors Don't Appear in Terminal

```bash
# Check color support
echo $TERM

# Force colored output
export FORCE_COLOR=1
cat logs.txt | logalize
```

### Configuration File Not Found

Logalize searches for configurations in this order:

1. `/etc/logalize/logalize.yaml`
2. `~/.config/logalize/logalize.yaml`
3. `.logalize.yaml` (in current directory)
4. Path specified with `-c/--config`

```bash
# Use specific path
logalize -c /full/path/to/logalize.yaml < logs.txt
```

## 💡 Tips and Tricks

### 1. Performance

For very large logs, use `--only-formats` for better performance:

```bash
tail -f huge.log | logalize --only-formats
```

### 2. Pipeline Integration

```bash
# Combine with grep
grep "error" /var/log/syslog | logalize

# Combine with awk
awk '/failed/' /var/log/auth.log | logalize

# Combine with sed
sed -n '100,200p' app.log | logalize
```

### 3. Save Colored Output

```bash
# Save with ANSI colors
tail -f /var/log/syslog | logalize > colored.log

# View later with less (preserves colors)
less -R colored.log
```

### 4. Multiple Files

```bash
# Colorize multiple files
cat /var/log/syslog /var/log/auth.log | logalize

# All logs in a directory
cat /var/log/*.log | logalize
```

### 5. Real-time Monitoring

```bash
# With terminal title update
watch -c "tail -n 50 /var/log/syslog | logalize"

# Multiple terminals with tmux/screen
tmux split-window "tail -f /var/log/nginx/access.log | logalize"
```

## 📖 Official Documentation

- **Original Project**: [deponian/logalize](https://github.com/deponian/logalize)
- **Documentation**: [Official README](https://github.com/deponian/logalize/blob/main/readme.md)
- **Issues**: [Report problems](https://github.com/deponian/logalize/issues)

## 🤝 Contributing

Found a bug or have a suggestion? Feel free to:

1. Open an [Issue](https://github.com/fgbona/logalize/issues)
2. Submit a Pull Request
3. Share your custom configurations

## 📄 License

This configuration file is under the MIT license. The original Logalize also uses the MIT license.

## ⭐ Acknowledgments

- **[@deponian](https://github.com/deponian)** - Creator of Logalize
- **[@emptysad](https://github.com/emptysad)** - Name and logo idea
- **[@ekivoka](https://github.com/ekivoka)** - Design and testing

## 📞 Support

Need help?

- 📖 Read the [official documentation](https://github.com/deponian/logalize)
- 🐛 Report bugs in [Issues](https://github.com/deponian/logalize/issues)
- 💬 Discussions in the [community](https://github.com/deponian/logalize/discussions)

---

**Made with ❤️ for the Logalize community**

⭐ If this repository was useful, leave a star!
