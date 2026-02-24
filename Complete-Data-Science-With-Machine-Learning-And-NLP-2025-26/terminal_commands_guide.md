# Complete Terminal Commands Guide: macOS & Linux
## From Scratch to Advanced

---

## Table of Contents
1. [Basics & Navigation](#basics--navigation)
2. [File & Directory Operations](#file--directory-operations)
3. [File Viewing & Editing](#file-viewing--editing)
4. [Permissions & Ownership](#permissions--ownership)
5. [Process Management](#process-management)
6. [System Information](#system-information)
7. [Network Commands](#network-commands)
8. [Text Processing](#text-processing)
9. [Searching & Finding](#searching--finding)
10. [Compression & Archives](#compression--archives)
11. [Package Management](#package-management)
12. [Advanced Shell Features](#advanced-shell-features)
13. [Scripting Basics](#scripting-basics)
14. [Advanced Commands](#advanced-commands)

---

## Basics & Navigation

### Essential Navigation
```bash
# Print working directory (where am I?)
pwd

# List files and directories
ls                    # Basic listing
ls -l                 # Long format with details
ls -a                 # Show hidden files (starting with .)
ls -lh                # Human-readable file sizes
ls -ltr               # Sort by time, reversed (newest last)
ls -R                 # Recursive listing

# Change directory
cd /path/to/directory # Absolute path
cd relative/path      # Relative path
cd ..                 # Go up one directory
cd ~                  # Go to home directory
cd -                  # Go to previous directory
cd                    # Go to home directory (shortcut)

# Print to terminal
echo "Hello World"
echo $HOME            # Print environment variable
```

### Getting Help
```bash
# Manual pages
man ls                # Show manual for 'ls' command
man -k search_term    # Search manual pages

# Command help
ls --help             # Most Linux commands
ls -h                 # Some macOS commands

# Which command/where is it
which python          # Show path to executable
whereis python        # Show path, man pages (Linux)
type python           # Show command type
```

---

## File & Directory Operations

### Creating Files & Directories
```bash
# Create empty file
touch file.txt
touch file1.txt file2.txt file3.txt  # Multiple files

# Create directory
mkdir mydir
mkdir -p path/to/nested/directory    # Create parent directories
mkdir dir1 dir2 dir3                 # Multiple directories

# Create file with content
cat > file.txt                        # Type content, Ctrl+D to save
echo "content" > file.txt             # Overwrite file
echo "more content" >> file.txt       # Append to file
```

### Copying, Moving, Renaming
```bash
# Copy files
cp source.txt destination.txt
cp file.txt /path/to/directory/
cp -r directory/ new_directory/       # Copy directory recursively
cp -i file.txt dest.txt               # Interactive (prompt before overwrite)
cp -u source.txt dest.txt             # Copy only if newer

# Move/Rename files
mv oldname.txt newname.txt            # Rename
mv file.txt /path/to/directory/       # Move
mv -i file.txt dest.txt               # Interactive
mv *.txt /destination/                # Move all .txt files

# Remove files/directories
rm file.txt
rm -i file.txt                        # Interactive
rm -f file.txt                        # Force removal
rm -r directory/                      # Remove directory recursively
rm -rf directory/                     # Force recursive removal (DANGEROUS!)
rmdir empty_directory/                # Remove empty directory only
```

### Links
```bash
# Hard link (same inode)
ln source.txt hardlink.txt

# Symbolic link (shortcut)
ln -s /path/to/file symlink.txt
ln -s /path/to/directory/ symlink_dir

# Read symbolic link
readlink symlink.txt
readlink -f symlink.txt               # Follow to absolute path
```

---

## File Viewing & Editing

### Viewing File Contents
```bash
# Display entire file
cat file.txt
cat file1.txt file2.txt               # Concatenate multiple files

# Display with line numbers
cat -n file.txt
nl file.txt

# View file page by page
less file.txt                         # Navigate with arrows, q to quit
more file.txt                         # Older pager

# View beginning/end of file
head file.txt                         # First 10 lines
head -n 20 file.txt                   # First 20 lines
tail file.txt                         # Last 10 lines
tail -n 20 file.txt                   # Last 20 lines
tail -f logfile.txt                   # Follow file (live updates)
tail -F logfile.txt                   # Follow with retry
```

### Text Editors
```bash
# Nano (beginner-friendly)
nano file.txt                         # Ctrl+X to exit

# Vim (powerful, steep learning curve)
vim file.txt
vi file.txt
# In vim: i (insert), Esc (normal mode), :w (save), :q (quit), :wq (save & quit)

# Emacs
emacs file.txt

# macOS specific
open file.txt                         # Open with default app
open -e file.txt                      # Open with TextEdit
```

---

## Permissions & Ownership

### Understanding Permissions
```
-rwxr-xr-x  1 user group size date filename
 |||||||||||
 ||||||||||└─ Other execute
 |||||||||└── Other write
 ||||||||└─── Other read
 |||||||└──── Group execute
 ||||||└───── Group write
 |||||└────── Group read
 ||||└─────── Owner execute
 |||└──────── Owner write
 ||└───────── Owner read
 |└────────── Special permissions
 └─────────── File type (- file, d directory, l link)
```

### Changing Permissions
```bash
# Symbolic method
chmod u+x file.txt                    # Add execute for user
chmod g-w file.txt                    # Remove write for group
chmod o+r file.txt                    # Add read for others
chmod a+x file.txt                    # Add execute for all
chmod u=rw,g=r,o=r file.txt          # Set exact permissions

# Numeric method (octal)
chmod 755 file.txt                    # rwxr-xr-x
chmod 644 file.txt                    # rw-r--r--
chmod 600 file.txt                    # rw-------
chmod 777 file.txt                    # rwxrwxrwx (usually bad practice)

# Recursive
chmod -R 755 directory/
```

### Changing Ownership
```bash
# Change owner
sudo chown newowner file.txt
sudo chown newowner:newgroup file.txt
sudo chown -R newowner directory/     # Recursive

# Change group only
sudo chgrp newgroup file.txt
```

### Special Permissions
```bash
# Setuid (4) - run as file owner
chmod u+s executable
chmod 4755 executable

# Setgid (2) - run as group owner / inherit group
chmod g+s directory/
chmod 2755 directory/

# Sticky bit (1) - only owner can delete
chmod +t directory/
chmod 1755 directory/

# View special permissions
ls -l file
```

---

## Process Management

### Viewing Processes
```bash
# List processes
ps                                    # Current shell processes
ps aux                                # All processes (BSD style)
ps -ef                                # All processes (POSIX style)
ps -u username                        # User's processes
ps -C processname                     # By process name

# Process tree
pstree
pstree -p                             # With PIDs

# Top/interactive monitoring
top                                   # Real-time process viewer
htop                                  # Enhanced top (may need install)
```

### Managing Processes
```bash
# Background & foreground
command &                             # Run in background
jobs                                  # List background jobs
fg %1                                 # Bring job 1 to foreground
bg %1                                 # Resume job 1 in background
Ctrl+Z                                # Suspend current process
Ctrl+C                                # Kill current process

# Killing processes
kill PID                              # Graceful termination (SIGTERM)
kill -9 PID                           # Force kill (SIGKILL)
kill -15 PID                          # Same as kill PID
killall processname                   # Kill by name
pkill pattern                         # Kill by pattern

# Process nice values (priority)
nice -n 10 command                    # Start with lower priority
renice -n 5 -p PID                    # Change priority of running process
```

### Advanced Process Control
```bash
# No hang-up (continue after logout)
nohup command &
nohup command > output.log 2>&1 &

# Disown process
command &
disown

# Process substitution
diff <(ls dir1) <(ls dir2)

# Watch command output
watch -n 2 'ps aux | grep myprocess'  # Update every 2 seconds
```

---

## System Information

### System Details
```bash
# System information
uname -a                              # All system info
uname -s                              # Kernel name
uname -r                              # Kernel release
uname -m                              # Machine hardware

# Hostname
hostname
hostname -I                           # All IP addresses (Linux)

# Uptime
uptime
uptime -p                             # Pretty format

# Who is logged in
who
w
whoami                                # Current user
id                                    # User and group IDs
```

### Hardware & Resources
```bash
# CPU information
lscpu                                 # Linux
sysctl -n machdep.cpu.brand_string    # macOS

# Memory usage
free -h                               # Linux (human readable)
vm_stat                               # macOS

# Disk usage
df -h                                 # Filesystem usage
df -i                                 # Inode usage
du -h directory/                      # Directory size
du -sh directory/                     # Summary only
du -sh *                              # Size of each item

# Disk partitions
lsblk                                 # Linux
diskutil list                         # macOS

# USB devices
lsusb                                 # Linux

# PCI devices
lspci                                 # Linux

# Battery status (macOS)
pmset -g batt
```

### Date & Time
```bash
# Current date/time
date
date "+%Y-%m-%d %H:%M:%S"             # Custom format

# Calendar
cal                                   # Current month
cal 2024                              # Whole year
cal 12 2024                           # Specific month

# Time zone
timedatectl                           # Linux
```

---

## Network Commands

### Network Configuration
```bash
# IP address
ip addr show                          # Linux
ifconfig                              # macOS/older Linux
ipconfig getifaddr en0                # macOS specific interface

# Network interfaces
ip link show                          # Linux
networksetup -listallhardwareports    # macOS

# Routing table
ip route                              # Linux
route -n                              # Linux (older)
netstat -r                            # macOS/Linux
```

### Network Connectivity
```bash
# Ping
ping google.com
ping -c 4 google.com                  # 4 packets only

# Traceroute
traceroute google.com
tracepath google.com                  # Linux alternative

# DNS lookup
nslookup google.com
dig google.com
host google.com
```

### Network Tools
```bash
# Port scanning
nc -zv hostname 80                    # Check if port 80 is open
nmap hostname                         # Port scanner (may need install)

# Active connections
netstat -tuln                         # Listening ports (Linux)
lsof -i                               # Open network connections
lsof -i :8080                         # Specific port

# Download files
wget https://example.com/file.zip
curl -O https://example.com/file.zip
curl -L -o output.zip https://url     # Follow redirects, name output

# Transfer files
scp file.txt user@host:/path/         # Secure copy to remote
scp user@host:/path/file.txt .        # Copy from remote
rsync -avz source/ dest/              # Sync directories
```

### SSH
```bash
# Connect to remote
ssh user@hostname
ssh -p 2222 user@hostname             # Custom port
ssh -i keyfile user@hostname          # Use specific key

# SSH keys
ssh-keygen                            # Generate key pair
ssh-keygen -t rsa -b 4096            # RSA 4096-bit
ssh-copy-id user@hostname             # Copy public key to remote

# SSH tunneling
ssh -L 8080:localhost:80 user@host    # Local port forwarding
ssh -R 8080:localhost:80 user@host    # Remote port forwarding
ssh -D 8080 user@host                 # SOCKS proxy
```

---

## Text Processing

### grep (Search Text)
```bash
# Basic search
grep "pattern" file.txt
grep "pattern" file1.txt file2.txt    # Multiple files
grep -r "pattern" directory/          # Recursive search

# Options
grep -i "pattern" file.txt            # Case insensitive
grep -v "pattern" file.txt            # Invert match (exclude)
grep -n "pattern" file.txt            # Show line numbers
grep -c "pattern" file.txt            # Count matches
grep -l "pattern" *.txt               # Files with matches
grep -w "word" file.txt               # Match whole word
grep -A 3 "pattern" file.txt          # 3 lines after match
grep -B 3 "pattern" file.txt          # 3 lines before match
grep -C 3 "pattern" file.txt          # 3 lines context

# Regular expressions
grep -E "pattern1|pattern2" file.txt  # Extended regex (OR)
grep -P "regex" file.txt              # Perl regex (Linux)
```

### sed (Stream Editor)
```bash
# Substitute text
sed 's/old/new/' file.txt             # First occurrence per line
sed 's/old/new/g' file.txt            # All occurrences
sed 's/old/new/gi' file.txt           # Case insensitive
sed -i 's/old/new/g' file.txt         # Edit file in-place (Linux)
sed -i '' 's/old/new/g' file.txt      # Edit file in-place (macOS)

# Delete lines
sed '5d' file.txt                     # Delete line 5
sed '5,10d' file.txt                  # Delete lines 5-10
sed '/pattern/d' file.txt             # Delete lines matching pattern

# Print specific lines
sed -n '5p' file.txt                  # Print only line 5
sed -n '5,10p' file.txt               # Print lines 5-10
sed -n '/pattern/p' file.txt          # Print matching lines
```

### awk (Text Processing)
```bash
# Print columns
awk '{print $1}' file.txt             # First column
awk '{print $1, $3}' file.txt         # First and third columns
awk -F: '{print $1}' /etc/passwd      # Custom delimiter

# Conditional processing
awk '$3 > 100' file.txt               # Lines where column 3 > 100
awk '$1 == "ERROR"' log.txt           # Lines where column 1 is ERROR
awk 'NR > 1' file.txt                 # Skip first line

# Built-in variables
awk '{print NR, $0}' file.txt         # Line number and line
awk '{print NF}' file.txt             # Number of fields
awk 'END {print NR}' file.txt         # Total lines

# Calculations
awk '{sum += $1} END {print sum}' file.txt        # Sum first column
awk '{sum += $1} END {print sum/NR}' file.txt     # Average
```

### cut (Extract Columns)
```bash
# By character position
cut -c 1-10 file.txt                  # Characters 1-10
cut -c 1,5,10 file.txt                # Characters 1, 5, 10

# By delimiter
cut -d: -f1 /etc/passwd               # First field, : delimiter
cut -d: -f1,3 /etc/passwd             # Fields 1 and 3
cut -d, -f2- file.csv                 # From field 2 to end
```

### sort & uniq
```bash
# Sort
sort file.txt                         # Alphabetically
sort -n file.txt                      # Numerically
sort -r file.txt                      # Reverse
sort -k2 file.txt                     # By second column
sort -t: -k3 -n /etc/passwd          # Custom delimiter, numeric

# Unique lines
uniq file.txt                         # Remove consecutive duplicates
uniq -c file.txt                      # Count occurrences
uniq -d file.txt                      # Only duplicates
sort file.txt | uniq                  # Remove all duplicates
```

### tr (Translate/Delete)
```bash
# Translate characters
tr 'a-z' 'A-Z' < file.txt            # Lowercase to uppercase
tr -d '0-9' < file.txt               # Delete all digits
tr -s ' ' < file.txt                 # Squeeze spaces
echo "text" | tr ' ' '\n'            # Replace space with newline
```

---

## Searching & Finding

### find (Find Files)
```bash
# By name
find /path -name "filename"
find /path -iname "filename"          # Case insensitive
find /path -name "*.txt"              # Wildcard
find /path -not -name "*.txt"         # Exclude pattern

# By type
find /path -type f                    # Files only
find /path -type d                    # Directories only
find /path -type l                    # Symbolic links

# By size
find /path -size +100M                # Larger than 100MB
find /path -size -1k                  # Smaller than 1KB
find /path -empty                     # Empty files/directories

# By time
find /path -mtime -7                  # Modified in last 7 days
find /path -mtime +30                 # Modified more than 30 days ago
find /path -mmin -60                  # Modified in last 60 minutes
find /path -newer file.txt            # Newer than file.txt

# By permissions
find /path -perm 644                  # Exact permissions
find /path -perm -644                 # At least these permissions

# Execute command on results
find /path -name "*.txt" -exec cat {} \;
find /path -name "*.log" -delete
find /path -type f -exec chmod 644 {} \;

# Advanced
find /path -name "*.txt" -o -name "*.pdf"     # OR condition
find /path -name "*.txt" -and -size +1M       # AND condition
find /path -maxdepth 2 -name "*.txt"          # Limit depth
```

### locate (Fast File Search)
```bash
# Search database
locate filename
locate -i filename                    # Case insensitive
locate -c filename                    # Count results
locate -r 'pattern'                   # Regex

# Update database
sudo updatedb                         # Linux
sudo /usr/libexec/locate.updatedb     # macOS
```

### which & whereis
```bash
# Find executable location
which python
which -a python                       # All matches

# Find binary, source, manual
whereis python                        # Linux only
```

---

## Compression & Archives

### tar (Tape Archive)
```bash
# Create archive
tar -cvf archive.tar directory/       # Create
tar -czvf archive.tar.gz directory/   # Create + gzip
tar -cjvf archive.tar.bz2 directory/  # Create + bzip2
tar -cJvf archive.tar.xz directory/   # Create + xz

# Extract archive
tar -xvf archive.tar                  # Extract
tar -xzvf archive.tar.gz              # Extract gzip
tar -xjvf archive.tar.bz2             # Extract bzip2

# List contents
tar -tvf archive.tar                  # List files
tar -tzvf archive.tar.gz              # List gzip archive

# Extract specific file
tar -xvf archive.tar file.txt
tar -xzvf archive.tar.gz path/to/file

# Append to archive
tar -rvf archive.tar newfile.txt

# Options explained:
# -c: create, -x: extract, -t: list
# -v: verbose, -f: file
# -z: gzip, -j: bzip2, -J: xz
```

### gzip & bzip2
```bash
# Compress
gzip file.txt                         # Creates file.txt.gz
gzip -k file.txt                      # Keep original
bzip2 file.txt                        # Creates file.txt.bz2

# Decompress
gunzip file.txt.gz
bunzip2 file.txt.bz2
gzip -d file.txt.gz

# View compressed file
zcat file.txt.gz
zless file.txt.gz
zgrep "pattern" file.txt.gz
```

### zip & unzip
```bash
# Create zip
zip archive.zip file1.txt file2.txt
zip -r archive.zip directory/         # Recursive

# Extract zip
unzip archive.zip
unzip archive.zip -d /destination/    # To specific directory
unzip -l archive.zip                  # List contents

# Password protected
zip -e secure.zip file.txt            # Encrypt
unzip secure.zip                      # Will prompt for password
```

---

## Package Management

### macOS (Homebrew)
```bash
# Install Homebrew (if not installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Package management
brew install package_name
brew uninstall package_name
brew update                           # Update Homebrew
brew upgrade                          # Upgrade all packages
brew upgrade package_name             # Upgrade specific package

# Search and info
brew search keyword
brew info package_name
brew list                             # Installed packages

# Services
brew services list
brew services start service_name
brew services stop service_name

# Cask (GUI apps)
brew install --cask app_name
brew uninstall --cask app_name
```

### Ubuntu/Debian (apt)
```bash
# Update package list
sudo apt update

# Upgrade packages
sudo apt upgrade                      # Upgrade all
sudo apt full-upgrade                 # Smart upgrade

# Install/remove
sudo apt install package_name
sudo apt remove package_name
sudo apt purge package_name           # Remove with config
sudo apt autoremove                   # Remove unused dependencies

# Search
apt search keyword
apt show package_name

# List packages
apt list --installed
apt list --upgradable
```

### RedHat/Fedora/CentOS (dnf/yum)
```bash
# Install/remove
sudo dnf install package_name         # Fedora/newer
sudo yum install package_name         # CentOS/older
sudo dnf remove package_name

# Update
sudo dnf update
sudo dnf upgrade

# Search
dnf search keyword
dnf info package_name

# List
dnf list installed
dnf list available
```

### Arch Linux (pacman)
```bash
# Install/remove
sudo pacman -S package_name           # Install
sudo pacman -R package_name           # Remove
sudo pacman -Rs package_name          # Remove with dependencies

# Update system
sudo pacman -Syu                      # Sync and update

# Search
pacman -Ss keyword                    # Search repository
pacman -Qs keyword                    # Search installed

# Info
pacman -Si package_name               # Repository info
pacman -Qi package_name               # Installed info
```

---

## Advanced Shell Features

### Redirection & Pipes
```bash
# Output redirection
command > file.txt                    # Overwrite file
command >> file.txt                   # Append to file
command 2> error.log                  # Redirect stderr
command 2>&1                          # Redirect stderr to stdout
command > output.txt 2>&1             # Both to file
command &> output.txt                 # Both to file (shorthand)

# Input redirection
command < input.txt
command << EOF                        # Here document
line 1
line 2
EOF

# Pipes
command1 | command2                   # Output of 1 to input of 2
command1 | tee file.txt | command2    # Save to file and pipe
```

### Command Substitution
```bash
# Backticks (old style)
result=`command`

# $() (preferred)
result=$(command)
echo "Today is $(date)"

# Examples
files=$(ls *.txt)
count=$(ls | wc -l)
```

### Variables
```bash
# Define variables
name="value"
count=42
path="/home/user"

# Use variables
echo $name
echo ${name}                          # Preferred
echo "Hello $name"

# Read input
read variable
read -p "Enter name: " name
read -s password                      # Silent (for passwords)

# Special variables
$?      # Exit status of last command
$0      # Script name
$1-$9   # Arguments
$#      # Number of arguments
$@      # All arguments
$$      # Process ID
$!      # Last background process PID
```

### Environment Variables
```bash
# View environment
env                                   # All environment variables
printenv                              # Same as env
echo $PATH                            # Specific variable

# Set environment variables
export VAR="value"                    # For current session
export PATH="$PATH:/new/path"         # Add to PATH

# Permanent (in ~/.bashrc or ~/.zshrc)
echo 'export VAR="value"' >> ~/.bashrc
source ~/.bashrc                      # Reload

# Common variables
$HOME       # Home directory
$USER       # Current username
$PWD        # Current directory
$OLDPWD     # Previous directory
$PATH       # Executable search path
$SHELL      # Current shell
```

### Aliases
```bash
# Create alias
alias ll='ls -lah'
alias ..='cd ..'
alias gs='git status'
alias update='sudo apt update && sudo apt upgrade'

# List aliases
alias

# Remove alias
unalias ll

# Permanent aliases (in ~/.bashrc or ~/.zshrc)
echo "alias ll='ls -lah'" >> ~/.bashrc
source ~/.bashrc
```

### Functions
```bash
# Define function
myfunction() {
    echo "Hello from function"
    echo "Argument 1: $1"
}

# Call function
myfunction arg1 arg2

# Function with return
add() {
    return $(($1 + $2))
}
add 5 3
echo $?                               # Get return value

# More complex function
backup() {
    local source=$1
    local dest=$2
    tar -czf "$dest/backup-$(date +%Y%m%d).tar.gz" "$source"
}
```

### Loops & Conditionals
```bash
# If statement
if [ condition ]; then
    commands
elif [ condition2 ]; then
    commands
else
    commands
fi

# Test conditions
[ -f file.txt ]          # File exists
[ -d directory ]         # Directory exists
[ -r file.txt ]          # Readable
[ -w file.txt ]          # Writable
[ -x file.txt ]          # Executable
[ "$a" = "$b" ]          # String equal
[ "$a" != "$b" ]         # String not equal
[ $a -eq $b ]            # Numeric equal
[ $a -lt $b ]            # Less than
[ $a -gt $b ]            # Greater than

# For loop
for i in 1 2 3 4 5; do
    echo $i
done

for file in *.txt; do
    echo "Processing $file"
done

for i in {1..10}; do
    echo $i
done

# While loop
counter=0
while [ $counter -lt 10 ]; do
    echo $counter
    counter=$((counter + 1))
done

# Until loop
until [ condition ]; do
    commands
done
```

### Command Chaining
```bash
# Sequential execution
command1; command2; command3

# AND (execute if previous succeeds)
command1 && command2

# OR (execute if previous fails)
command1 || command2

# Combine
command1 && command2 || command3
```

---

## Scripting Basics

### Shell Script Structure
```bash
#!/bin/bash
# This is a comment

# Script description
# Author: Your Name
# Date: 2024-01-01

# Variables
NAME="World"

# Main logic
echo "Hello, $NAME!"

# Functions
greet() {
    echo "Hello, $1!"
}

# Call function
greet "User"

# Exit
exit 0
```

### Script Execution
```bash
# Make executable
chmod +x script.sh

# Run script
./script.sh                           # Current directory
bash script.sh                        # With bash interpreter
sh script.sh                          # With sh interpreter
source script.sh                      # In current shell
. script.sh                           # Same as source
```

### Debugging Scripts
```bash
# Debug mode
bash -x script.sh                     # Print each command

# In script
set -x                                # Enable debugging
set +x                                # Disable debugging

# Strict mode (recommended)
set -euo pipefail
# -e: exit on error
# -u: error on undefined variable
# -o pipefail: pipe fails if any command fails
```

### Reading Files
```bash
# Line by line
while IFS= read -r line; do
    echo "Line: $line"
done < file.txt

# With for loop
for line in $(cat file.txt); do
    echo $line
done

# Using command substitution
lines=$(cat file.txt)
```

### User Input Validation
```bash
#!/bin/bash

read -p "Enter your name: " name

if [ -z "$name" ]; then
    echo "Error: Name cannot be empty"
    exit 1
fi

echo "Hello, $name!"
```

---

## Advanced Commands

### xargs (Build Commands)
```bash
# Basic usage
echo "file1 file2 file3" | xargs rm

# From file
cat files.txt | xargs rm

# Find and execute
find . -name "*.tmp" | xargs rm
find . -name "*.txt" -print0 | xargs -0 grep "pattern"

# Parallel execution
cat urls.txt | xargs -P 4 -n 1 curl    # 4 parallel downloads

# Interactive
find . -name "*.log" | xargs -p rm     # Prompt before each

# Replace string
ls *.txt | xargs -I {} mv {} {}.bak
```

### Screen & tmux (Terminal Multiplexers)
```bash
# Screen
screen                                # Start new session
screen -S name                        # Named session
screen -ls                            # List sessions
screen -r                             # Reattach
screen -r name                        # Reattach to named
# Ctrl+A, D                           # Detach
# Ctrl+A, C                           # New window
# Ctrl+A, N                           # Next window

# tmux (more modern)
tmux                                  # New session
tmux new -s name                      # Named session
tmux ls                               # List sessions
tmux attach -t name                   # Attach to session
tmux kill-session -t name             # Kill session
# Ctrl+B, D                           # Detach
# Ctrl+B, C                           # New window
# Ctrl+B, %                           # Split vertical
# Ctrl+B, "                           # Split horizontal
```

### cron (Scheduled Tasks)
```bash
# Edit crontab
crontab -e                            # Edit user's crontab
sudo crontab -e                       # Edit root's crontab

# List crontab
crontab -l

# Remove crontab
crontab -r

# Crontab format
# * * * * * command
# │ │ │ │ │
# │ │ │ │ └─── Day of week (0-7, Sunday=0 or 7)
# │ │ │ └───── Month (1-12)
# │ │ └─────── Day of month (1-31)
# │ └───────── Hour (0-23)
# └─────────── Minute (0-59)

# Examples
0 2 * * * /backup.sh                  # Daily at 2 AM
*/15 * * * * /check.sh                # Every 15 minutes
0 9-17 * * 1-5 /work.sh              # 9 AM-5 PM, weekdays
@reboot /startup.sh                   # At startup
```

### System Logs
```bash
# View logs
tail -f /var/log/syslog               # Follow system log (Linux)
tail -f /var/log/system.log           # macOS
journalctl -f                         # systemd journal (Linux)
journalctl -u service_name            # Specific service

# Search logs
grep "error" /var/log/syslog
journalctl --since "1 hour ago"
journalctl --since "2024-01-01"
```

### System Services (systemd - Linux)
```bash
# Service management
sudo systemctl start service_name
sudo systemctl stop service_name
sudo systemctl restart service_name
sudo systemctl reload service_name
sudo systemctl status service_name

# Enable/disable on boot
sudo systemctl enable service_name
sudo systemctl disable service_name

# List services
systemctl list-units --type=service
systemctl list-unit-files
```

### File Descriptors & Advanced I/O
```bash
# Open file descriptor
exec 3< input.txt                     # Open for reading
exec 4> output.txt                    # Open for writing
exec 5<> file.txt                     # Open for read/write

# Use file descriptor
cat <&3                               # Read from FD 3
echo "data" >&4                       # Write to FD 4

# Close file descriptor
exec 3<&-                             # Close FD 3

# Named pipes (FIFO)
mkfifo mypipe
command1 > mypipe &
command2 < mypipe
```

### Job Control Advanced
```bash
# Run with specific priority
nice -n 19 cpu_intensive_task         # Lowest priority
nice -n -20 important_task            # Highest (requires sudo)

# Change running process priority
renice -n 10 -p PID

# CPU affinity (Linux)
taskset -c 0,1 command                # Run on CPUs 0 and 1
taskset -p -c 0,1 PID                 # Set for running process

# Limit resources
ulimit -a                             # Show all limits
ulimit -n 1024                        # Max open files
ulimit -u 100                         # Max user processes
```

### Performance Monitoring
```bash
# I/O statistics
iostat                                # Disk I/O stats
iostat -x 2                           # Extended, refresh every 2s
iotop                                 # Top for I/O (requires sudo)

# Virtual memory statistics
vmstat 2                              # Every 2 seconds

# Network statistics
iftop                                 # Network bandwidth (may need install)
nethogs                               # Per-process bandwidth

# Disk activity
sar                                   # System activity reporter

# Trace system calls
strace command                        # Trace program execution
strace -p PID                         # Attach to running process
```

### Disk Management Advanced
```bash
# Check filesystem
sudo fsck /dev/sda1                   # Check and repair
sudo e2fsck -f /dev/sda1             # Force check (ext filesystems)

# Mount/Unmount
sudo mount /dev/sdb1 /mnt/usb
sudo umount /mnt/usb
mount                                 # List mounted filesystems

# Create filesystem
sudo mkfs.ext4 /dev/sdb1              # ext4
sudo mkfs.vfat /dev/sdb1              # FAT32

# Disk image
dd if=/dev/sda of=backup.img          # Create disk image
dd if=backup.img of=/dev/sdb          # Restore disk image
dd if=/dev/zero of=file.img bs=1M count=100  # Create 100MB file
```

### Text Processing Advanced
```bash
# Column formatting
column -t file.txt                    # Auto-format columns
column -t -s: file.txt                # Custom separator

# Join files
join file1.txt file2.txt              # Join on common field
paste file1.txt file2.txt             # Merge line by line

# Compare files
diff file1.txt file2.txt
diff -u file1.txt file2.txt           # Unified format
diff -y file1.txt file2.txt           # Side by side
comm file1.txt file2.txt              # Compare sorted files

# Binary file operations
hexdump -C file.bin                   # Hex dump
xxd file.bin                          # Another hex dump
strings file.bin                      # Extract readable strings
```

### Regular Expressions
```bash
# Basic regex metacharacters
.       # Any single character
*       # Zero or more
+       # One or more (extended)
?       # Zero or one (extended)
^       # Start of line
$       # End of line
[]      # Character class
[^]     # Negated character class
\       # Escape special character

# Examples
grep '^[A-Z]' file.txt               # Lines starting with capital
grep '[0-9]\{3\}-[0-9]\{4\}' file.txt # Phone pattern
grep -E '^(https?|ftp)://' file.txt  # URLs
```

### Process Substitution
```bash
# Compare output of two commands
diff <(ls dir1) <(ls dir2)

# Use command output as file
wc -l <(ps aux)

# Multiple process substitution
paste <(cut -f1 file1) <(cut -f2 file2)
```

---

## Security & Encryption

### SSH Advanced
```bash
# SSH config (~/.ssh/config)
Host myserver
    HostName example.com
    User myuser
    Port 2222
    IdentityFile ~/.ssh/mykey

# Then connect with: ssh myserver

# SSH agent
eval $(ssh-agent)
ssh-add ~/.ssh/id_rsa

# SSH tunneling examples
ssh -L 8080:localhost:80 user@remote  # Access remote port 80 via local 8080
ssh -R 8080:localhost:80 user@remote  # Remote can access local port 80 via 8080
ssh -D 8080 user@remote               # SOCKS proxy on port 8080
```

### File Encryption
```bash
# GPG encryption
gpg -c file.txt                       # Encrypt with password
gpg file.txt.gpg                      # Decrypt

# OpenSSL
openssl enc -aes-256-cbc -in file.txt -out file.enc
openssl enc -d -aes-256-cbc -in file.enc -out file.txt

# Generate checksums
md5sum file.txt                       # MD5 (Linux)
md5 file.txt                          # MD5 (macOS)
sha256sum file.txt                    # SHA256 (Linux)
shasum -a 256 file.txt                # SHA256 (macOS)
```

---

## Productivity Tips

### History Management
```bash
# View history
history
history 20                            # Last 20 commands

# Search history
Ctrl+R                                # Reverse search
history | grep "keyword"

# Execute from history
!number                               # Run command number
!!                                    # Last command
!-2                                   # Two commands ago
!string                               # Last command starting with string

# Clear history
history -c                            # Clear session
rm ~/.bash_history                    # Delete history file
```

### Keyboard Shortcuts
```bash
# Navigation
Ctrl+A      # Beginning of line
Ctrl+E      # End of line
Ctrl+B      # Back one character
Ctrl+F      # Forward one character
Alt+B       # Back one word
Alt+F       # Forward one word

# Editing
Ctrl+U      # Delete to beginning of line
Ctrl+K      # Delete to end of line
Ctrl+W      # Delete previous word
Ctrl+Y      # Paste (yank)
Ctrl+T      # Swap characters
Alt+T       # Swap words

# Control
Ctrl+C      # Kill process
Ctrl+Z      # Suspend process
Ctrl+D      # EOF / Logout
Ctrl+L      # Clear screen
```

### Quick Tips
```bash
# Previous command as sudo
sudo !!

# Replace in previous command
^old^new

# Use output of previous command
command $(previous_command)

# Quick backup
cp file.txt{,.bak}                    # Creates file.txt.bak

# Create directory and cd into it
mkdir mydir && cd mydir

# Multiple commands with brace expansion
touch file{1..10}.txt                 # Creates file1.txt to file10.txt
mkdir -p project/{src,bin,docs}       # Create multiple directories
```

---

## Troubleshooting

### Common Issues
```bash
# Permission denied
sudo command                          # Run with elevated privileges
chmod +x script.sh                    # Make executable

# Command not found
which command                         # Check if installed
echo $PATH                            # Check PATH variable
type command                          # Check command type

# Port already in use
lsof -i :8080                         # See what's using port
sudo kill -9 PID                      # Kill the process

# Disk full
df -h                                 # Check disk usage
du -sh /*                             # Find large directories
sudo du -sh /var/*                    # Check /var
```

### System Recovery
```bash
# Boot into single user mode (varies by system)
# Add 'single' or '1' to kernel parameters

# Reset password (single user mode)
passwd username

# Check filesystem on boot
# Add fsck.mode=force to kernel parameters

# Recovery from broken packages (Ubuntu/Debian)
sudo dpkg --configure -a
sudo apt-get -f install
```

---

## Additional Resources

### Man Page Sections
```bash
man 1 command    # User commands
man 2 syscall    # System calls
man 3 function   # Library functions
man 5 file       # File formats
man 8 admin      # System administration

# Example
man 5 passwd     # Password file format
man 1 passwd     # passwd command
```

### Getting More Help
```bash
# Info pages (GNU documentation)
info command

# Online help
man -k keyword                        # Search manual pages
apropos keyword                       # Same as man -k

# Command examples
tldr command                          # Simplified examples (may need install)
```

---

## Practice Exercises

### Beginner
1. Navigate to your home directory and list all files including hidden ones
2. Create a directory structure: `project/src/main` in one command
3. Create 5 empty files named `file1.txt` through `file5.txt`
4. Find all `.txt` files in your home directory

### Intermediate
1. Write a script that backs up a directory with a timestamp
2. Find all files larger than 100MB in your system
3. Create an alias that shows disk usage of current directory in human-readable format
4. Use `awk` to calculate the total size of all files in a directory

### Advanced
1. Write a script that monitors CPU usage and sends alert if over 80%
2. Set up a cron job that cleans temporary files weekly
3. Create a function that searches for and replaces text in multiple files
4. Use process substitution to compare the output of two different commands

---

## Conclusion

This guide covers commands from basic navigation to advanced system administration. Practice regularly to build muscle memory. Remember:

- Use `man` and `--help` for detailed information
- Test commands in safe environments first
- Use version control for scripts
- Document your complex commands
- Be cautious with `sudo` and destructive commands

Happy learning!
keep learning and keep exploring !  