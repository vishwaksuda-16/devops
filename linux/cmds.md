# 🐧 Linux Basics Complete Guide

A comprehensive guide covering Linux fundamentals, networking, SSH, services, and system administration.

---

## Table of Contents

1. [Filesystem & Paths](#-filesystem--paths)
2. [Navigation & Directories](#-navigation--directories)
3. [File Operations](#-file-operations)
4. [Search & Compare](#-search--compare)
5. [Links](#-links)
6. [Help & Documentation](#-help--documentation)
7. [Globbing (Wildcards)](#-globbing-wildcards)
8. [Tab Completion](#️-tab-completion)
9. [Standard Streams & Redirection](#-standard-streams--redirection)
10. [Variables & Scope](#-variables--scope)
11. [Text Processing](#-text-processing)
12. [Process Management](#-process-management)
13. [Root & Privileges](#-root--privileges)
14. [File Permissions](#-file-permissions)
15. [Scripts & Operators](#-scripts--operators)
16. [Terminal Multiplexers](#️-terminal-multiplexers)
17. [PATH & Executables](#-path--executables)
18. [Security & Shenanigans](#️-security--shenanigans)
19. [System Breaking (Caution)](#-system-breaking-caution)
20. [Networking Commands](#-networking-commands)
21. [SSH & Remote Access](#-ssh--remote-access)
22. [File Transfer](#-file-transfer)
23. [Services Management](#-services-management)
24. [Web Servers](#-web-servers)
25. [Firewall Management](#-firewall-management)
26. [System Logs](#-system-logs)
27. [System Monitoring](#-system-monitoring)
28. [Practical Use Cases](#-practical-use-cases)

---

## 📂 Filesystem & Paths

- `/` = root directory
- **Absolute path**: starts with `/` (e.g., `/challenge/run`)
- **Relative path**: depends on current working directory (e.g., `challenge/run`)
- `.` = current directory
- `..` = parent directory
- `~` = home directory (`/home/username`)

### Running Programs

```bash
/challenge/run     # absolute path
./run              # relative path from current directory
```

---

## 📁 Navigation & Directories

```bash
pwd               # show current directory
cd /path          # go to specified path
cd                # go to home directory (~)
cd -              # go to previous directory
ls                # list files
ls -a             # include hidden files
ls -l             # detailed listing
ls -la            # detailed listing with hidden files
ls -ld dir        # show directory permissions
mkdir dir         # create directory
mkdir -p a/b/c    # create nested directories
```

---

## 📄 File Operations

```bash
cat file1 file2   # print/concatenate files
touch file        # create empty file or update timestamp
rm file           # remove file
rm -rf dir        # remove directory recursively (dangerous!)
mv old new        # move/rename file
cp file1 file2    # copy file
cp -r dir1 dir2   # copy directory recursively
```

---

## 🔍 Search & Compare

```bash
grep "text" file          # find lines containing "text"
grep -r "text" dir        # recursive search in directory
grep -i "text" file       # case-insensitive search
diff file1 file2          # show differences between files
find . -name "pattern"    # search for files by name
find . -type f -name "*.txt"  # find all .txt files
locate filename           # find file using database
which command             # find location of command
```

---

## 🔗 Links

```bash
ln -s /path/to/file link_name   # create symbolic link
ln /path/to/file hard_link      # create hard link
file link_name                  # check file type (shows if symlink)
readlink link_name              # show target of symlink
```

---

## 📖 Help & Documentation

```bash
man command       # manual page for command
command --help    # quick help for command
help              # list shell builtins
help cd           # help on specific builtin
info command      # info documentation
whatis command    # brief description
apropos keyword   # search man pages by keyword
```

---

## ✨ Globbing (Wildcards)

- `*` = matches any string (except `/`)
- `?` = matches any single character
- `[abc]` = matches one of a, b, or c
- `[!abc]` = matches anything except a, b, or c
- `[a-z]` = matches any lowercase letter
- `{a,b,c}` = matches a or b or c

### Examples

```bash
ls file_*         # match file_a, file_b, etc.
ls file_??        # match file_ab, not file_a
ls file_[!a]      # exclude file_a
ls *.{txt,log}    # match .txt and .log files
```

---

## ⌨️ Tab Completion

- `TAB` = auto-complete filenames/commands
- `TAB TAB` = show all available options
- Works with commands, filenames, and paths

---

## 🔹 Standard Streams & Redirection

- **stdin (0)** → input stream
- **stdout (1)** → normal output
- **stderr (2)** → error messages

### Redirection Operators

```bash
command > file.txt           # redirect stdout to file (overwrite)
command >> file.txt          # redirect stdout to file (append)
command 2> error.log         # redirect stderr to file
command 2>&1                 # redirect stderr to stdout
command > out.log 2> err.log # separate stdout and stderr
command &> all.log           # redirect both stdout and stderr
```

### Pipes

```bash
command1 | command2          # stdout of cmd1 → stdin of cmd2
command | tee file.txt       # save output to file and display
command | grep "pattern"     # filter output
```

### Process Substitution

```bash
diff <(command1) <(command2)     # compare outputs of two commands
```

### FIFOs (Named Pipes)

```bash
mkfifo myfifo               # create named pipe
echo "hello" > myfifo &     # write to pipe (background)
cat myfifo                  # read from pipe
```

---

## 🔹 Variables & Scope

### Variable Operations

```bash
VAR=value                   # assign variable (no spaces!)
VAR="value with spaces"     # assign with spaces
echo $VAR                   # print variable
echo ${VAR}                 # print variable (preferred)
unset VAR                   # remove variable
```

### Environment Variables

```bash
export VAR=value            # export variable to child processes
env                         # show all environment variables
printenv                    # show all environment variables
echo $PATH                  # show PATH variable
```

### Command Substitution

```bash
OUTPUT=$(command)           # capture command output
OUTPUT=`command`            # older syntax (backticks)
FLAG=$(cat /flag)           # example usage
```

### Reading Input

```bash
read VAR                    # read from stdin
read VAR < file             # read from file
read -p "Enter name: " NAME # read with prompt
```

---

## 📌 Text Processing

```bash
head -n 10 file             # show first 10 lines
tail -n 10 file             # show last 10 lines
tail -f file                # follow file changes
cut -d',' -f1,3 file.csv    # extract columns 1 and 3
sort file                   # sort lines
sort -n file                # numerical sort
sort -r file                # reverse sort
uniq file                   # remove duplicate lines
wc file                     # count lines, words, characters
wc -l file                  # count lines only
tr 'a-z' 'A-Z' < file       # translate lowercase to uppercase
sed 's/old/new/g' file      # replace text
awk '{print $1}' file       # print first column
```

---

## 📌 Process Management

### Viewing Processes

```bash
ps                          # show current user's processes
ps aux                      # show all processes
ps -ef                      # alternative format
top                         # dynamic process viewer
htop                        # enhanced process viewer
pgrep process_name          # find process ID by name
```

### Process Control

```bash
kill PID                    # terminate process by ID
kill -9 PID                 # force kill process
killall process_name        # kill all processes by name
pkill process_name          # kill processes by name pattern
```

### Job Control

```bash
command &                   # run in background
jobs                        # list active jobs
fg %1                       # bring job 1 to foreground
bg %1                       # send job 1 to background
Ctrl+C                      # interrupt (SIGINT)
Ctrl+Z                      # suspend (SIGTSTP)
nohup command &             # run immune to hangups
```

### Exit Status

```bash
echo $?                     # show exit status of last command
command && echo "success"   # run if previous succeeded
command || echo "failed"    # run if previous failed
```

---

## 📌 Root & Privileges

### User Switching

```bash
su                          # switch to root
su username                 # switch to specific user
su -                        # switch to root with environment
su - username               # switch user with environment
```

### Sudo

```bash
sudo command                # run command as root
sudo -u username command    # run command as specific user
sudo -i                     # interactive root shell
sudo -s                     # non-login root shell
visudo                      # edit sudoers file safely
```

### Password Files

```bash
/etc/passwd                 # user account information
/etc/shadow                 # password hashes (root only)
/etc/group                  # group information
```

### Password Cracking

```bash
john /etc/shadow            # crack password hashes
john --show /etc/shadow     # show cracked passwords
```

---

## 📌 File Permissions

### Permission Structure

```
rwx rwx rwx
│   │   └── other permissions
│   └────── group permissions
└────────── owner permissions
```

- `r` = read (4)
- `w` = write (2)
- `x` = execute (1)

### Changing Permissions

```bash
chmod 755 file              # rwxr-xr-x
chmod u+x file              # add execute for owner
chmod g-w file              # remove write for group
chmod o=r file              # set other to read-only
chmod +x file               # add execute for all
```

### Changing Ownership

```bash
chown user file             # change owner
chown user:group file       # change owner and group
chgrp group file            # change group only
chown -R user:group dir     # recursive change
```

### Special Permissions

```bash
chmod u+s file              # set SUID bit
chmod g+s file              # set SGID bit
chmod +t dir                # set sticky bit
ls -l                       # view permissions
```

---

## 📌 Scripts & Operators

### Command Chaining

```bash
command1; command2          # run sequentially
command1 && command2        # run cmd2 if cmd1 succeeds
command1 || command2        # run cmd2 if cmd1 fails
(command1; command2)        # run in subshell
```

### Script Basics

```bash
#!/bin/bash                 # shebang line
chmod +x script.sh          # make executable
./script.sh                 # run script
bash script.sh              # run with bash
```

### Script Variables

```bash
$0                          # script name
$1, $2, ...                 # script arguments
$#                          # number of arguments
$@                          # all arguments
$*                          # all arguments as single string
$$                          # process ID
$?                          # exit status of last command
```

### Conditional Statements

```bash
if [ condition ]; then
    commands
elif [ condition ]; then
    commands
else
    commands
fi
```

### Loops

```bash
for item in list; do
    echo $item
done

while [ condition ]; do
    commands
done
```

---

## 🖥️ Terminal Multiplexers

### Screen

```bash
screen                      # start new session
screen -S name              # start named session
screen -ls                  # list sessions
screen -r                   # reattach to session
screen -r name              # reattach to named session
```

**Screen Key Bindings:**
- `Ctrl+A d` → detach session
- `Ctrl+A c` → create new window
- `Ctrl+A n` → next window
- `Ctrl+A p` → previous window
- `Ctrl+A "` → list windows

### tmux

```bash
tmux                        # start new session
tmux new -s name            # start named session
tmux ls                     # list sessions
tmux attach                 # attach to session
tmux attach -t name         # attach to named session
tmux kill-session -t name   # kill session
```

**tmux Key Bindings:**
- `Ctrl+B d` → detach session
- `Ctrl+B c` → create new window
- `Ctrl+B n` → next window
- `Ctrl+B p` → previous window
- `Ctrl+B w` → list windows

---

## 📂 PATH & Executables

```bash
echo $PATH                  # show current PATH
which command               # find command location
whereis command             # find command and manual
type command                # show command type
PATH=$PATH:/new/dir         # add directory to PATH
export PATH                 # make PATH available to subprocesses
```

### Making Scripts Executable

```bash
chmod +x script.sh          # add execute permission
./script.sh                 # run from current directory
cp script.sh /usr/local/bin # install globally
```

---

## 🕵️ Security & Shenanigans

### Backdoor Techniques

```bash
echo "malicious_command" >> ~/.bashrc     # modify user's bashrc
echo "malicious_command" >> ~/.profile    # modify user's profile
```

### PATH Manipulation

```bash
mkdir ~/fake_bin
echo '#!/bin/bash' > ~/fake_bin/ls
echo 'echo "Hacked!"' >> ~/fake_bin/ls
chmod +x ~/fake_bin/ls
export PATH=~/fake_bin:$PATH
```

### Symlink Tricks

```bash
ln -sf /path/to/malicious ~/.bashrc       # replace bashrc with symlink
```

### Process Snooping

```bash
ps aux | grep -i password                  # look for passwords in processes
ps -eo pid,ppid,cmd,comm                   # detailed process info
```

### Configuration File Secrets

```bash
grep -r "password" /etc/                   # search for passwords in configs
find /home -name "*.conf" -exec grep -l "pass" {} \;
```

---

## 💣 System Breaking (Caution)

⚠️ **WARNING: These commands can destroy systems. Use only in test environments!**

### Fork Bomb

```bash
:(){ :|:& };:              # bash fork bomb
.(){.|.&};.                # alternative syntax
```

### Disk DoS

```bash
dd if=/dev/zero of=largefile bs=1M count=1000    # create large file
yes | head -c 1GB > bigfile                      # alternative method
```

### System Wipe

```bash
rm -rf /                   # delete everything (dangerous!)
dd if=/dev/zero of=/dev/sda # overwrite hard drive
```

---

## 🌐 Networking Commands

### Linux Networking

```bash
ip addr show               # show IP addresses
ip route show              # show routing table
ip link show               # show network interfaces
ping hostname              # test connectivity
traceroute hostname        # trace route to destination
mtr hostname               # continuous traceroute
netstat -tulnp             # show listening ports
ss -tulnp                  # modern alternative to netstat
tcpdump -i eth0            # capture packets
wget URL                   # download file
curl URL                   # transfer data from server
nmap target                # network scanning
dig hostname               # DNS lookup
host hostname              # DNS lookup
nmcli                      # network manager CLI
```

### Windows Networking

```cmd
ipconfig /all              # IP configuration details
nslookup hostname          # DNS records lookup
ping hostname              # test connectivity
tracert hostname           # trace route to destination
pathping hostname          # ping + route statistics
netstat -an                # view network connections
hostname                   # show system name
arp -a                     # show ARP table
nbtstat -a hostname        # NetBIOS information
route print                # show routing table
```

---

## 🔐 SSH & Remote Access

### SSH Service Setup (Ubuntu)

```bash
sudo apt update
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh
```

### SSH Client Usage

```bash
ssh username@hostname              # basic SSH connection
ssh -p 2222 username@hostname      # custom port
ssh -i ~/.ssh/key username@host    # use specific key
ssh -L 8080:localhost:80 user@host # local port forwarding
ssh -R 8080:localhost:80 user@host # remote port forwarding
ssh -D 1080 user@host              # SOCKS proxy
```

### SSH Key Management

```bash
ssh-keygen                         # generate SSH key pair
ssh-keygen -t rsa -b 4096          # generate RSA 4096-bit key
ssh-copy-id user@hostname          # copy public key to remote host
ssh-add ~/.ssh/private_key         # add key to SSH agent
ssh-agent bash                     # start SSH agent
```

### SSH Configuration

```bash
# Edit SSH client config
nano ~/.ssh/config

# Edit SSH server config
sudo nano /etc/ssh/sshd_config
sudo systemctl restart ssh
```

### Changing SSH Port

```bash
sudo nano /etc/ssh/sshd_config
# Change: Port 22 to Port 220
# Ensure line is uncommented (no #)
sudo systemctl restart ssh
sudo ufw allow 220/tcp
ssh -p 220 username@hostname
```

---

## 📤 File Transfer

### SCP (Secure Copy)

```bash
scp file.txt user@host:~/Desktop/         # copy file to remote
scp user@host:~/file.txt ./                # copy file from remote
scp -r directory/ user@host:~/             # copy directory recursively
scp -P 2222 file.txt user@host:~/          # use custom port
```

### RSYNC

```bash
rsync -avz file.txt user@host:~/Desktop/   # sync file to remote
rsync -avz user@host:~/file.txt ./         # sync file from remote
rsync -avz --delete src/ dest/             # sync with deletion
rsync -avz -e "ssh -p 2222" src/ user@host:dest/  # custom SSH port
```

**RSYNC Options:**
- `-a` = archive mode (preserves permissions, timestamps)
- `-v` = verbose
- `-z` = compress during transfer
- `--delete` = delete files in destination not in source

---

## ⚙️ Services Management

### Systemd Service Management

```bash
systemctl status service_name              # check service status
sudo systemctl start service_name          # start service
sudo systemctl stop service_name           # stop service
sudo systemctl restart service_name        # restart service
sudo systemctl reload service_name         # reload configuration
sudo systemctl enable service_name         # enable at boot
sudo systemctl disable service_name        # disable at boot
```

### Listing Services

```bash
systemctl list-units --type=service        # list all services
systemctl list-units --type=service --state=running  # running services
systemctl list-unit-files --type=service   # all service files
```

### Service Logs

```bash
journalctl -u service_name                 # view service logs
journalctl -u service_name -f              # follow service logs
journalctl -u service_name --since today   # logs since today
```

---

## 🌐 Web Servers

### Nginx

```bash
# Installation
sudo apt install nginx -y

# Service Management
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
sudo systemctl reload nginx

# Configuration
sudo nano /etc/nginx/sites-available/default
sudo nginx -t                              # test configuration
sudo systemctl reload nginx

# Logs
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

### Apache

```bash
# Installation
sudo apt install apache2 -y

# Service Management
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl status apache2

# Configuration
sudo nano /etc/apache2/sites-available/000-default.conf
sudo a2ensite sitename                     # enable site
sudo a2dissite sitename                    # disable site
sudo systemctl reload apache2
```

---

## 🔥 Firewall Management

### UFW (Uncomplicated Firewall)

```bash
sudo ufw status                            # check firewall status
sudo ufw enable                            # enable firewall
sudo ufw disable                           # disable firewall
sudo ufw reload                            # reload rules

# Allow/Deny Rules
sudo ufw allow ssh                         # allow SSH service
sudo ufw allow 22                          # allow port 22
sudo ufw allow 80/tcp                      # allow HTTP
sudo ufw allow from 192.168.1.0/24        # allow from subnet
sudo ufw deny 23                           # deny port 23

# Application Profiles
sudo ufw app list                          # list application profiles
sudo ufw allow 'Nginx Full'               # allow nginx
sudo ufw deny 'Nginx Full'                # deny nginx

# Delete Rules
sudo ufw delete allow 80                   # delete rule
sudo ufw --numbered status                 # show numbered rules
sudo ufw delete 1                          # delete rule by number
```

### iptables

```bash
sudo iptables -L                           # list rules
sudo iptables -F                           # flush all rules
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT  # allow SSH
sudo iptables -A INPUT -j DROP             # drop all other input
sudo iptables-save > /etc/iptables/rules.v4         # save rules
```

---

## 📋 System Logs

### Log Locations

```bash
/var/log/syslog                           # general system log
/var/log/auth.log                         # authentication log
/var/log/kern.log                         # kernel log
/var/log/apache2/                         # Apache logs
/var/log/nginx/                           # Nginx logs
/var/log/mysql/                           # MySQL logs
```

### Log Viewing Commands

```bash
tail -f /var/log/syslog                   # follow system log
tail -n 100 /var/log/auth.log             # last 100 lines of auth log
grep "ssh" /var/log/auth.log              # search for SSH in auth log
journalctl -xe                            # view recent journal entries
journalctl -f                             # follow journal
journalctl --since "2024-01-01"          # logs since date
journalctl -p err                         # error priority logs only
```

### Log Rotation

```bash
sudo logrotate -f /etc/logrotate.conf     # force log rotation
sudo nano /etc/logrotate.d/custom         # custom rotation config
```

---

## 📊 System Monitoring

### Resource Monitoring

```bash
top                                       # dynamic process viewer
htop                                      # enhanced process viewer
free -h                                   # memory usage (human readable)
df -h                                     # disk usage (human readable)
du -sh *                                  # directory sizes
du -h --max-depth=1                       # directory sizes with depth limit
iostat                                    # I/O statistics
vmstat                                    # virtual memory statistics
```

### Network Monitoring

```bash
nethogs                                   # network usage by process
iftop                                     # network usage by connection
vnstat                                    # network statistics
ss -tulnp                                 # socket statistics
netstat -i                               # interface statistics
```

### System Information

```bash
uname -a                                  # system information
lscpu                                     # CPU information
lsblk                                     # block devices
lsusb                                     # USB devices
lspci                                     # PCI devices
dmidecode                                 # hardware information
uptime                                    # system uptime and load
who                                       # logged in users
w                                         # detailed user activity
last                                      # login history
```

### Performance Testing

```bash
# CPU stress test
yes > /dev/null &                         # simple CPU load
stress --cpu 4 --timeout 60s             # stress test with stress tool

# Memory test
stress --vm 2 --vm-bytes 1G --timeout 60s

# I/O test
dd if=/dev/zero of=testfile bs=1M count=1000 oflag=direct
```

---

## 🧪 Practical Use Cases

### Day 1: Network Connectivity Test

**Scenario:** Testing ICMP connectivity between Kali Linux and Ubuntu VMs.

**Ubuntu (receiving end):**
```bash
sudo tcpdump -i enp0s3 icmp
# Observed: 14 ICMP packets (7 requests + 7 replies)
```

**Kali (sending end):**
```bash
ping 192.168.1.2
# Result: 14 packets sent, 0% packet loss, 0.42-0.73ms latency
```

**Outcome:** ✅ Confirmed two-way connectivity and proper ICMP functionality.

### Day 2: SSH Setup and File Transfer

**SSH Service Setup:**
```bash
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
```

**Passwordless Authentication:**
```bash
ssh-keygen                                # on Kali
ssh-copy-id username@192.168.1.20        # copy key to Ubuntu
ssh username@192.168.1.20                # passwordless login
```

**File Transfer Testing:**
```bash
# SCP
scp file1.txt username@192.168.1.20:~/Desktop
scp -r testdir/ username@192.168.1.20:~/Desktop

# RSYNC
rsync -avz file1.txt username@192.168.1.20:~/Desktop
rsync -avz testdir/ username@192.168.1.20:~/Desktop
```

**Issues Resolved:**
- Permission denied → fixed with correct user permissions
- Connection refused → fixed by starting SSH service

### Day 3: Firewall and Monitoring

**UFW Configuration:**
```bash
sudo ufw enable
sudo ufw allow ssh
sudo ufw deny 'Nginx Full'                # blocked web access
sudo ufw allow 'Nginx Full'               # re-enabled web access
```

**Log Monitoring:**
```bash
sudo tail -f /var/log/auth.log            # SSH login attempts
cat /var/log/nginx/access.log             # web server access
```

**Performance Testing:**
```bash
yes > /dev/null &                         # CPU stress test
kill [PID]                                # stop stress test
```

### Day 4: Custom SSH Port

**Port Configuration:**
```bash
sudo nano /etc/ssh/sshd_config
# Changed: Port 22 → Port 220
# Removed # comment
sudo systemctl restart ssh
```

**Firewall Update:**
```bash
sudo ufw allow 220/tcp
sudo ufw reload
```

**Verification:**
```bash
ss -tulnp | grep sshd                     # confirm port binding
ssh -p 220 username@ubuntu-ip             # connect with custom port
```

**Common Issues:**
- Multiple Port lines in config → used default port 22
- Firewall blocking → connection refused
- Service not restarted → changes not applied

---

## ✅ Key Takeaways

### Linux Fundamentals
- Mastered file system navigation, permissions, and basic operations
- Learned process management, job control, and service administration
- Understood shell scripting, variables, and command chaining
- Explored text processing tools and advanced file operations

### Security & System Administration
- Configured SSH with custom ports and key-based authentication
- Implemented firewall rules with UFW
- Monitored system logs and performance metrics
- Practiced secure file transfer methods

### Networking & Services
- Set up and managed web servers (nginx)
- Configured network services and troubleshot connectivity
- Used packet capture tools for network analysis
- Implemented proper service management with systemd

### Troubleshooting Skills
- Diagnosed permission issues and service failures
- Resolved network connectivity problems
- Fixed configuration errors and syntax mistakes
- Applied systematic debugging approaches

This guide serves as a comprehensive reference for Linux system administration, security practices, and troubleshooting techniques.