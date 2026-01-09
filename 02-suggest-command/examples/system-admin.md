# System Administration Examples

Practical system administration tasks using `gh copilot suggest`.

## Process Management

### View Processes

```bash
# All processes
gh copilot suggest "show all running processes"
# → ps aux

# Processes by user
gh copilot suggest "show processes owned by current user"
# → ps -u $USER

# Process tree
gh copilot suggest "show process tree"
# → ps auxf
# or → pstree
```

### Find Processes

```bash
# By name
gh copilot suggest "find all node processes"
# → ps aux | grep node

# By port
gh copilot suggest "find process using port 3000"
# → lsof -i :3000
# or → netstat -tlnp | grep 3000

# By resource usage
gh copilot suggest "show top 10 processes by CPU usage"
# → ps aux --sort=-%cpu | head -11

# By memory
gh copilot suggest "show processes using more than 500MB memory"
# → ps aux | awk '$6 > 500000'
```

### Kill Processes

```bash
# By PID
gh copilot suggest "kill process with PID 1234"
# → kill 1234

# Force kill
gh copilot suggest "force kill process 1234"
# → kill -9 1234

# By name
gh copilot suggest "kill all node processes"
# → pkill node

# By port (find then kill)
gh copilot suggest "kill process using port 8080"
# → kill $(lsof -t -i:8080)
```

## System Resources

### CPU Information

```bash
# CPU details
gh copilot suggest "show CPU information"
# → lscpu

# CPU usage
gh copilot suggest "show current CPU usage"
# → top -bn1 | grep "Cpu(s)"

# Per-core usage
gh copilot suggest "show CPU usage per core"
# → mpstat -P ALL
```

### Memory Usage

```bash
# Memory overview
gh copilot suggest "show memory usage in human readable format"
# → free -h

# Detailed memory
gh copilot suggest "show detailed memory information"
# → cat /proc/meminfo

# Memory by process
gh copilot suggest "show memory usage by process sorted"
# → ps aux --sort=-%mem | head -20

# Available memory
gh copilot suggest "show available memory"
# → free -h | awk '/Mem:/ {print $7}'
```

### Disk Usage

```bash
# Disk space overview
gh copilot suggest "show disk space for all mounted filesystems"
# → df -h

# Directory sizes
gh copilot suggest "show size of each subdirectory sorted by size"
# → du -h --max-depth=1 | sort -hr

# Largest directories
gh copilot suggest "find 10 largest directories"
# → du -h / | sort -hr | head -10

# Disk I/O stats
gh copilot suggest "show disk I/O statistics"
# → iostat -x 1
```

## Network Operations

### Network Information

```bash
# IP address
gh copilot suggest "show my IP address"
# → ip addr show
# or → ifconfig

# Listening ports
gh copilot suggest "show all listening ports"
# → netstat -tuln | grep LISTEN
# or → ss -tuln

# Network connections
gh copilot suggest "show active network connections"
# → netstat -an

# Route table
gh copilot suggest "show routing table"
# → route -n
# or → ip route
```

### Network Testing

```bash
# Ping
gh copilot suggest "ping google with 5 packets"
# → ping -c 5 google.com

# Check port
gh copilot suggest "test if port 443 is open on example.com"
# → nc -zv example.com 443

# DNS lookup
gh copilot suggest "lookup DNS records for domain"
# → nslookup example.com

# Trace route
gh copilot suggest "trace route to google.com"
# → traceroute google.com
```

### Download Operations

```bash
# Download file
gh copilot suggest "download file from URL"
# → wget https://example.com/file.zip
# or → curl -O https://example.com/file.zip

# Download with progress
gh copilot suggest "download with progress bar"
# → wget --progress=bar https://example.com/file.zip

# Resume download
gh copilot suggest "resume interrupted download"
# → wget -c https://example.com/file.zip
```

## Service Management

### Systemd Services

```bash
# List services
gh copilot suggest "list all systemd services"
# → systemctl list-units --type=service

# Service status
gh copilot suggest "check status of nginx service"
# → systemctl status nginx

# Start/stop service
gh copilot suggest "restart apache service"
# → sudo systemctl restart apache2

# Enable on boot
gh copilot suggest "enable service to start on boot"
# → sudo systemctl enable service-name

# View logs
gh copilot suggest "show logs for failed services"
# → journalctl -u service-name -p err
```

## User Management

### View Users

```bash
# Current user
gh copilot suggest "show current user information"
# → whoami
# → id

# Logged in users
gh copilot suggest "show all logged in users"
# → who

# User details
gh copilot suggest "show details for user john"
# → finger john
# or → id john
```

### User Operations

```bash
# Add user
gh copilot suggest "create new user with home directory"
# → sudo useradd -m username

# Change password
gh copilot suggest "change password for user"
# → sudo passwd username

# Add to group
gh copilot suggest "add user to sudo group"
# → sudo usermod -aG sudo username

# Lock user account
gh copilot suggest "lock user account"
# → sudo passwd -l username
```

## Log Management

### View Logs

```bash
# System log
gh copilot suggest "show last 50 lines of system log"
# → tail -50 /var/log/syslog

# Follow log in real-time
gh copilot suggest "watch auth log in real-time"
# → tail -f /var/log/auth.log

# Journalctl
gh copilot suggest "show logs from last hour"
# → journalctl --since "1 hour ago"

# Errors only
gh copilot suggest "show only error logs from today"
# → journalctl -p err --since today
```

### Search Logs

```bash
# Search for pattern
gh copilot suggest "search for failed login attempts"
# → grep "Failed password" /var/log/auth.log

# Count occurrences
gh copilot suggest "count errors in log file"
# → grep -c "ERROR" /var/log/app.log

# Multiple logs
gh copilot suggest "search all logs for out of memory errors"
# → grep -r "out of memory" /var/log/
```

## Scheduled Tasks

### Cron Jobs

```bash
# List cron jobs
gh copilot suggest "show cron jobs for current user"
# → crontab -l

# Edit cron jobs
gh copilot suggest "edit cron jobs"
# → crontab -e

# System-wide cron
gh copilot suggest "list all system cron jobs"
# → ls -la /etc/cron.*
```

## System Information

### General Info

```bash
# OS version
gh copilot suggest "show operating system version"
# → cat /etc/os-release

# Kernel version
gh copilot suggest "show kernel version"
# → uname -r

# Uptime
gh copilot suggest "show system uptime"
# → uptime

# Hardware info
gh copilot suggest "show hardware information"
# → lshw
```

### Boot Information

```bash
# Boot time
gh copilot suggest "show last boot time"
# → who -b

# Boot log
gh copilot suggest "show boot messages"
# → dmesg

# Boot performance
gh copilot suggest "analyze boot time"
# → systemd-analyze blame
```

## Backup and Restore

### Backup Operations

```bash
# Backup directory
gh copilot suggest "backup home directory to external drive"
# → rsync -avz --progress /home/user/ /mnt/backup/

# Incremental backup
gh copilot suggest "create incremental backup"
# → rsync -avz --delete --link-dest=/backup/previous /source/ /backup/current/

# Database backup
gh copilot suggest "backup mysql database"
# → mysqldump -u root -p database_name > backup.sql
```

## Performance Monitoring

### Real-time Monitoring

```bash
# System overview
gh copilot suggest "show real-time system resource usage"
# → htop
# or → top

# Disk activity
gh copilot suggest "monitor disk activity in real-time"
# → iotop

# Network traffic
gh copilot suggest "monitor network bandwidth usage"
# → iftop
```

### Performance Analysis

```bash
# Load average
gh copilot suggest "check system load average"
# → uptime
# → cat /proc/loadavg

# I/O wait
gh copilot suggest "show I/O wait time"
# → iostat

# Open files
gh copilot suggest "show number of open files"
# → lsof | wc -l
```

## Security

### Firewall

```bash
# Firewall status
gh copilot suggest "check firewall status"
# → sudo ufw status

# Open port
gh copilot suggest "allow port 80 through firewall"
# → sudo ufw allow 80

# Block IP
gh copilot suggest "block IP address"
# → sudo ufw deny from 192.168.1.100
```

### Security Auditing

```bash
# Failed login attempts
gh copilot suggest "show failed ssh login attempts"
# → grep "Failed password" /var/log/auth.log

# Open ports
gh copilot suggest "show all open ports and listening services"
# → sudo netstat -tlnp

# Last logins
gh copilot suggest "show last login history"
# → last

# Sudo usage
gh copilot suggest "show recent sudo commands"
# → grep sudo /var/log/auth.log
```

## Practical Scenarios

### High CPU Usage Investigation

```bash
# 1. Identify high CPU processes
gh copilot suggest "show top 5 CPU consuming processes"

# 2. Get details
gh copilot suggest "show threads for process 1234"

# 3. Check history
gh copilot suggest "analyze CPU usage over time"
```

### Disk Space Crisis

```bash
# 1. Check space
gh copilot suggest "show disk usage summary"

# 2. Find large directories
gh copilot suggest "find largest directories in root"

# 3. Find large files
gh copilot suggest "find files larger than 1GB"

# 4. Clean up
gh copilot suggest "remove old log files"
```

### Memory Leak Detection

```bash
# 1. Check memory usage
gh copilot suggest "show memory usage by process"

# 2. Monitor over time
gh copilot suggest "log memory usage every 5 seconds"

# 3. Identify culprit
gh copilot suggest "show process with highest memory growth"
```

## Tips

1. **Use sudo carefully**: Review commands before running with sudo
2. **Test in safe environment**: Try destructive commands in test environment first
3. **Backup before changes**: Always backup configuration files before modifying
4. **Monitor after changes**: Watch logs after making system changes
5. **Document changes**: Keep notes of system modifications

---

**Related**: [file-operations.md](./file-operations.md) | [docker-k8s.md](./docker-k8s.md)
