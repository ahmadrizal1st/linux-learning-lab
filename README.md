# Linux Learning Environment with Docker

A simple Docker-based Ubuntu environment for learning Linux command line basics.

## Prerequisites

- Docker installed on your system
- Docker Compose installed on your system
- Basic knowledge of terminal/command prompt

## Quick Start

1. **Clone or create the project directory:**
   ```bash
   mkdir linux-learning && cd linux-learning
   ```

2. **Create the docker-compose.yml file** (copy the content from below)

3. **Create necessary directories:**
   ```bash
   mkdir workspace scripts
   ```

4. **Start the container:**
   ```bash
   docker-compose up -d
   ```

5. **Access the container:**
   ```bash
   docker exec -it linux-learning-env bash
   ```

## Docker Compose Configuration

Create a file named `docker-compose.yml` with the following content:

```yaml
version: '3.8'

services:
  linux-learning:
    image: ubuntu:22.04
    container_name: linux-learning-env
    stdin_open: true
    tty: true
    working_dir: /workspace
    volumes:
      - ./workspace:/workspace
      - ./scripts:/scripts
    environment:
      - TERM=xterm-256color
    command: /bin/bash
```

## Container Management Commands

### Start the container
```bash
docker-compose up -d
```

### Stop the container
```bash
docker-compose down
```

### Access the container
```bash
docker exec -it linux-learning-env bash
```

### Check container status
```bash
docker-compose ps
```

### View container logs
```bash
docker-compose logs
```

## Creating a New User in Ubuntu Container

When you first access the container, you'll be logged in as root. Here's how to create a regular user:

1. **Access the container as root:**
   ```bash
   docker exec -it linux-learning-env bash
   ```

2. **Update package list:**
   ```bash
   apt-get update
   ```

3. **Install sudo (if not available):**
   ```bash
   apt-get install -y sudo
   
   # and
   apt-get install -y ubuntu-standard
   ```

4. **Create a new user:**
   ```bash
   adduser student
   ```
   Follow the prompts to set a password and user information.

5. **Add user to sudo group:**
   ```bash
   usermod -aG sudo student
   ```

6. **Switch to the new user:**
   ```bash
   su - student
   ```

7. **Verify the user:**
   ```bash
   whoami
   id
   ```

## Basic Linux Tutorial

### 1. Navigation Commands

```bash
# Print current directory
pwd

# List files and directories
ls
ls -l      # Detailed list
ls -a      # Include hidden files
ls -la     # Detailed list with hidden files

# Change directory
cd /path/to/directory
cd ~       # Home directory
cd ..      # Parent directory
cd -       # Previous directory
```

### 2. File Operations

```bash
# Create a file
touch filename.txt
echo "Hello World" > filename.txt

# View file content
cat filename.txt
less filename.txt    # Page through file
head filename.txt    # First 10 lines
tail filename.txt    # Last 10 lines

# Copy files
cp source.txt destination.txt
cp -r sourcedir/ destinationdir/  # Copy directory

# Move/Rename files
mv oldname.txt newname.txt
mv file.txt /path/to/destination/

# Delete files
rm filename.txt
rm -r directoryname/  # Delete directory
rm -rf directoryname/ # Force delete (be careful!)
```

### 3. Directory Operations

```bash
# Create directory
mkdir newdir
mkdir -p parent/child/grandchild  # Create nested directories

# Remove directory
rmdir emptydir
rm -r dirwithfiles

# Check disk usage
df -h
du -sh directoryname
```

### 4. File Permissions

```bash
# View permissions
ls -l

# Change permissions
chmod 755 filename.sh    # rwxr-xr-x
chmod +x script.sh       # Add execute permission
chmod 644 filename.txt   # rw-r--r--

# Change ownership
chown user:group filename
```

### 5. System Information

```bash
# System info
uname -a
lsb_release -a

# Process management
ps aux
top
htop

# Memory usage
free -h

# Network
ip addr show
ping google.com
```

### 6. Text Processing

```bash
# Search in files
grep "pattern" filename.txt
grep -r "pattern" directory/  # Recursive search

# Count lines, words, characters
wc filename.txt

# Sort lines
sort filename.txt

# Remove duplicates
uniq filename.txt
```

### 7. Package Management

```bash
# Update package list
sudo apt update

# Upgrade packages
sudo apt upgrade

# Install software
sudo apt install package-name

# Remove software
sudo apt remove package-name

# Search for packages
apt search keyword
```

### 8. User Management

```bash
# Show current user
whoami

# Show logged in users
who
w

# Change password
passwd

# Switch user
su - username
sudo -i  # Switch to root
```

### 9. Process Management

```bash
# List processes
ps aux
ps -ef

# Kill process
kill PID
kill -9 PID  # Force kill

# Run process in background
command &

# Jobs management
jobs
fg %1
bg %1
```

### 10. Useful Shortcuts

```bash
Ctrl + C    # Interrupt current process
Ctrl + Z    # Suspend current process
Ctrl + D    # Exit shell
Ctrl + A    # Move to beginning of line
Ctrl + E    # Move to end of line
Ctrl + U    # Clear line
Ctrl + R    # Search command history
Tab         # Auto-complete
```

## Practice Exercises

1. **Create a practice directory structure:**
   ```bash
   mkdir -p practice/{documents,images,scripts}
   cd practice
   ```

2. **Create some sample files:**
   ```bash
   touch documents/{file1.txt,file2.txt}
   echo "Hello World" > scripts/hello.sh
   chmod +x scripts/hello.sh
   ```

3. **Practice file operations:**
   ```bash
   cp documents/file1.txt documents/file1_backup.txt
   mv documents/file2.txt images/picture.txt
   ls -la
   ```

## Tips for Learning

1. **Use the manual pages:**
   ```bash
   man ls
   man grep
   ```

2. **Practice regularly in the container**

3. **Don't be afraid to make mistakes** - it's a safe learning environment

4. **Try different commands and options**

5. **Use online resources and Linux documentation**

## Cleaning Up

When you're done practicing:

```bash
# Stop and remove container
docker-compose down

# Remove created directories (optional)
rm -rf workspace scripts
```

## Troubleshooting

- **Container won't start**: Check if Docker is running
- **Permission denied**: Use `sudo` or check your user permissions
- **Command not found**: The package might not be installed. Use `apt install` to install it

Happy learning! 🐧
