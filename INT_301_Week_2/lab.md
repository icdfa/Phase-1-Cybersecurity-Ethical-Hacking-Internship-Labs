# **Lab 1: Bash Scripting - Complete Beginner to Advanced Guide**

## **Objectives**

By the end of this lab, students will be able to:
- Understand the fundamentals of bash scripting and shell programming
- Create, edit, and execute bash scripts effectively
- Use variables, conditionals, and loops in bash scripts
- Implement functions for code organization and reusability
- Develop practical security automation scripts
- Apply best practices for bash script development

---

## **Lab Overview**
This lab will take you from absolute beginner to advanced bash scripting step by step. We'll start with the very basics and gradually build up to creating professional security automation scripts.

### **Learning Path:**
1. **Absolute Basics** - Your first script
2. **Variables & Input** - Storing and using data
3. **Conditionals** - Making decisions
4. **Loops** - Repeating tasks
5. **Functions** - Organizing code
6. **Real Projects** - Practical applications
7. **Advanced Topics** - Professional scripts

---

## **Part 1: Absolute Basics - Your First Script**

### **1.1 What is Bash Scripting?**
Think of bash scripting like writing a recipe for your computer. You tell it exactly what to do, step by step.

### **1.2 Creating Your Very First Script**
```bash
#!/bin/bash
# This is my first script!
# Lines starting with # are comments - the computer ignores them

echo "Hello, World!"
echo "I'm learning bash scripting!"
```

**Step-by-Step Creation:**
1. Open terminal
2. Type: `nano first_script.sh`
3. Copy the code above into the file
4. Press `Ctrl+X`, then `Y`, then `Enter` to save
5. Make it executable: `chmod +x first_script.sh`
6. Run it: `./first_script.sh`

**Exercise 1.1:** Modify the script to print your name and today's date.

---

## **Part 2: Variables - Storing Information**

### **2.1 What are Variables?**
Variables are like boxes where you can store information to use later.

### **2.2 Basic Variable Usage**
```bash
#!/bin/bash

# Storing text
name="John"
greeting="Hello"

# Storing numbers
age=25
score=100

# Using variables
echo "$greeting, $name!"
echo "You are $age years old"
echo "Your score is: $score"

# You can also change variables
name="Sarah"
echo "Now the name is: $name"
```

### **2.3 Getting Input from User**
```bash
#!/bin/bash

echo "What's your name?"
read username

echo "How old are you?"
read userage

echo "Hello $username, you are $userage years old!"
```

**Exercise 2.1:** Create a script that asks for someone's favorite color and food, then prints a sentence using both.

---

## **Part 3: Making Decisions - If Statements**

### **3.1 Basic If Statements**
```bash
#!/bin/bash

echo "Enter a number:"
read number

if [ $number -gt 10 ]; then
    echo "Your number is greater than 10"
else
    echo "Your number is 10 or less"
fi
```

### **3.2 Comparison Operators**
- `-eq` = equal to
- `-ne` = not equal to
- `-gt` = greater than
- `-lt` = less than
- `-ge` = greater than or equal to
- `-le` = less than or equal to

### **3.3 Multiple Conditions**
```bash
#!/bin/bash

echo "Enter your age:"
read age

if [ $age -lt 13 ]; then
    echo "You're a child"
elif [ $age -ge 13 ] && [ $age -lt 20 ]; then
    echo "You're a teenager"
else
    echo "You're an adult"
fi
```

**Exercise 3.1:** Create a simple password checker that asks for a password and says "Access granted" if it's "secret123".

---

## **Part 4: Repeating Tasks - Loops**

### **4.1 For Loops - Doing Something Multiple Times**
```bash
#!/bin/bash

# Loop through numbers 1 to 5
for i in 1 2 3 4 5
do
    echo "Loop number: $i"
done

# Loop through a list of names
for name in Alice Bob Charlie
do
    echo "Hello, $name!"
done
```

### **4.2 While Loops - Keep Going Until Condition Changes**
```bash
#!/bin/bash

# Count from 1 to 5
count=1
while [ $count -le 5 ]
do
    echo "Count: $count"
    count=$((count + 1))
done

# Keep asking until user says 'quit'
echo "Type messages (type 'quit' to exit):"
read message
while [ "$message" != "quit" ]
do
    echo "You said: $message"
    read message
done
```

**Exercise 4.1:** Create a script that counts from 10 down to 1, then says "Blast off!"

---

## **Part 5: Organizing Code - Functions**

### **5.1 What are Functions?**
Functions are like mini-scripts inside your script. They help organize your code.

### **5.2 Creating Simple Functions**
```bash
#!/bin/bash

# Define a function
greet_user() {
    echo "Hello, $1!"
    echo "Have a great day!"
}

# Use the function
greet_user "Alice"
greet_user "Bob"

# Function with multiple parameters
introduce() {
    echo "Name: $1"
    echo "Age: $2"
    echo "City: $3"
}

introduce "John" "25" "New York"
```

### **5.3 Function with Return Value**
```bash
#!/bin/bash

# Function that calculates square
calculate_square() {
    local num=$1
    local square=$((num * num))
    echo $square
}

# Using the function
result=$(calculate_square 5)
echo "The square of 5 is: $result"

result=$(calculate_square 8)
echo "The square of 8 is: $result"
```

**Exercise 5.1:** Create a function that takes two numbers and returns their sum.

---

## **Part 6: Your First Real Project - Simple Calculator**

### **6.1 Building a Calculator Step by Step**
```bash
#!/bin/bash

# Function to show menu
show_menu() {
    echo "=== Simple Calculator ==="
    echo "1. Add"
    echo "2. Subtract"
    echo "3. Multiply"
    echo "4. Divide"
    echo "5. Exit"
    echo -n "Choose an option (1-5): "
}

# Function to get numbers
get_numbers() {
    echo -n "Enter first number: "
    read num1
    echo -n "Enter second number: "
    read num2
}

# Main program
while true; do
    show_menu
    read choice
    
    case $choice in
        1)
            get_numbers
            result=$((num1 + num2))
            echo "Result: $num1 + $num2 = $result"
            ;;
        2)
            get_numbers
            result=$((num1 - num2))
            echo "Result: $num1 - $num2 = $result"
            ;;
        3)
            get_numbers
            result=$((num1 * num2))
            echo "Result: $num1 * $num2 = $result"
            ;;
        4)
            get_numbers
            if [ $num2 -eq 0 ]; then
                echo "Error: Cannot divide by zero!"
            else
                result=$((num1 / num2))
                echo "Result: $num1 / $num2 = $result"
            fi
            ;;
        5)
            echo "Goodbye!"
            exit 0
            ;;
        *)
            echo "Invalid choice! Please enter 1-5."
            ;;
    esac
    
    echo  # Empty line for spacing
    echo -n "Press Enter to continue..."
    read
done
```

**Exercise 6.1:** Add a "Power" option that calculates num1 to the power of num2.

---

## **Part 7: Intermediate Project - File Organizer**

### **7.1 Automatic File Organizer**
```bash
#!/bin/bash

# Create directories if they don't exist
mkdir -p Documents Images Music Videos Others

# Organize files by extension
for file in *; do
    if [ -f "$file" ]; then  # Check if it's a file (not directory)
        case "${file##*.}" in
            txt|pdf|doc|docx)
                mv "$file" Documents/
                echo "Moved $file to Documents/"
                ;;
            jpg|png|gif|bmp)
                mv "$file" Images/
                echo "Moved $file to Images/"
                ;;
            mp3|wav|flac)
                mv "$file" Music/
                echo "Moved $file to Music/"
                ;;
            mp4|avi|mkv|mov)
                mv "$file" Videos/
                echo "Moved $file to Videos/"
                ;;
            *)
                mv "$file" Others/
                echo "Moved $file to Others/"
                ;;
        esac
    fi
done

echo "File organization complete!"
```

**Exercise 7.1:** Modify the script to also count how many files were moved to each folder.

---

## **Part 8: Advanced Beginner - System Monitor**

### **8.1 Simple System Monitoring Script**
```bash
#!/bin/bash

# Function to get system information
get_system_info() {
    echo "=== System Information ==="
    echo "Current user: $(whoami)"
    echo "Hostname: $(hostname)"
    echo "Uptime: $(uptime -p)"
    echo "Date: $(date)"
    echo
}

# Function to get disk space
get_disk_space() {
    echo "=== Disk Space ==="
    df -h | grep -v tmpfs
    echo
}

# Function to get memory usage
get_memory_usage() {
    echo "=== Memory Usage ==="
    free -h
    echo
}

# Function to show running processes
get_top_processes() {
    echo "=== Top 5 Processes by CPU ==="
    ps aux --sort=-%cpu | head -6
    echo
}

# Main monitoring function
monitor_system() {
    clear
    echo "System Monitor - $(date)"
    echo "=========================="
    echo
    
    get_system_info
    get_disk_space
    get_memory_usage
    get_top_processes
    
    echo "Monitoring complete!"
}

# Run the monitor
monitor_system
```

**Exercise 8.1:** Add a function that shows network connections.

---

## **Part 9: Security Project - Simple Port Scanner**

### **9.1 Basic Network Port Scanner**
```bash
#!/bin/bash

# Function to scan a single port
scan_port() {
    local host=$1
    local port=$2
    
    # Try to connect to the port (timeout after 1 second)
    if timeout 1 bash -c "echo >/dev/tcp/$host/$port" 2>/dev/null; then
        echo "Port $port: OPEN"
    else
        echo "Port $port: CLOSED"
    fi
}

# Main scanning function
simple_port_scanner() {
    echo "=== Simple Port Scanner ==="
    echo -n "Enter target IP or hostname: "
    read target
    
    echo -n "Enter port range (e.g., 80 100): "
    read start_port end_port
    
    echo "Scanning $target from port $start_port to $end_port"
    echo "========================================="
    
    for ((port=start_port; port<=end_port; port++)); do
        scan_port $target $port
    done
    
    echo "Scan complete!"
}

# Run the scanner
simple_port_scanner
```

**Exercise 9.1:** Modify the scanner to only show open ports, not closed ones.

---

## **Part 10: Advanced Project - Automated Backup System**

### **10.1 Smart Backup Script**
```bash
#!/bin/bash

# Configuration
BACKUP_DIR="/home/$(whoami)/backups"
SOURCE_DIR="/home/$(whoami)/important_files"
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_FILE="backup_$DATE.tar.gz"

# Function to create backup
create_backup() {
    echo "Starting backup process..."
    echo "Source: $SOURCE_DIR"
    echo "Backup: $BACKUP_DIR/$BACKUP_FILE"
    echo
    
    # Create backup directory if it doesn't exist
    mkdir -p "$BACKUP_DIR"
    
    # Create the backup
    if tar -czf "$BACKUP_DIR/$BACKUP_FILE" "$SOURCE_DIR" 2>/dev/null; then
        echo "✓ Backup created successfully!"
        
        # Show backup size
        size=$(du -h "$BACKUP_DIR/$BACKUP_FILE" | cut -f1)
        echo "Backup size: $size"
        
        # List all backups
        list_backups
    else
        echo "✗ Backup failed!"
        exit 1
    fi
}

# Function to list existing backups
list_backups() {
    echo
    echo "Existing backups:"
    echo "================="
    ls -lh "$BACKUP_DIR"/*.tar.gz 2>/dev/null || echo "No backups found"
}

# Function to restore backup
restore_backup() {
    echo "Available backups:"
    ls "$BACKUP_DIR"/*.tar.gz 2>/dev/null || {
        echo "No backups available"
        return
    }
    
    echo -n "Enter backup filename to restore: "
    read backup_file
    
    if [ -f "$BACKUP_DIR/$backup_file" ]; then
        echo "Restoring from $backup_file..."
        tar -xzf "$BACKUP_DIR/$backup_file" -C /
        echo "✓ Restore completed!"
    else
        echo "✗ Backup file not found!"
    fi
}

# Main menu
while true; do
    echo
    echo "=== Backup System ==="
    echo "1. Create new backup"
    echo "2. List existing backups"
    echo "3. Restore from backup"
    echo "4. Exit"
    echo -n "Choose an option (1-4): "
    read choice
    
    case $choice in
        1) create_backup ;;
        2) list_backups ;;
        3) restore_backup ;;
        4) echo "Goodbye!"; exit 0 ;;
        *) echo "Invalid choice!" ;;
    esac
done
```

**Exercise 10.1:** Add a feature to automatically delete backups older than 7 days.

---

## **Part 11: Final Master Project - Complete Security Scanner**

### **11.1 All-in-One Security Scanner**
```bash
#!/bin/bash

# Configuration
LOG_FILE="security_scan_$(date +%Y%m%d_%H%M%S).log"
TARGET_FILE="targets.txt"

# Function to log messages
log() {
    local message="$1"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    echo "[$timestamp] $message" | tee -a "$LOG_FILE"
}

# Function for network discovery
network_discovery() {
    log "Starting network discovery..."
    
    # Get local IP address
    local_ip=$(hostname -I | awk '{print $1}')
    log "Local IP: $local_ip"
    
    # Discover hosts on local network
    log "Discovering hosts on network..."
    nmap -sn "${local_ip%.*}.0/24" | grep "Nmap scan" | awk '{print $5, $6}' | tee -a "$LOG_FILE"
}

# Function for port scanning
port_scanning() {
    log "Starting port scanning..."
    
    if [ ! -f "$TARGET_FILE" ]; then
        echo "Please create $TARGET_FILE with target IPs, one per line"
        return
    fi
    
    while read -r target; do
        if [ -n "$target" ]; then
            log "Scanning ports on $target"
            nmap -sS -T4 "$target" | grep -E "(open|filtered|closed)" | tee -a "$LOG_FILE"
        fi
    done < "$TARGET_FILE"
}

# Function for vulnerability checking
vulnerability_check() {
    log "Checking for common vulnerabilities..."
    
    # Check for outdated packages
    log "Checking for outdated packages..."
    apt list --upgradable 2>/dev/null | tee -a "$LOG_FILE"
    
    # Check sudo version for known vulnerabilities
    log "Checking sudo version..."
    sudo --version | head -1 | tee -a "$LOG_FILE"
}

# Function for system security check
system_security_check() {
    log "Performing system security check..."
    
    # Check for unnecessary services
    log "Checking running services..."
    netstat -tuln | grep LISTEN | tee -a "$LOG_FILE"
    
    # Check firewall status
    log "Checking firewall status..."
    ufw status verbose | tee -a "$LOG_FILE"
    
    # Check for suspicious processes
    log "Checking for suspicious processes..."
    ps aux --sort=-%cpu | head -10 | tee -a "$LOG_FILE"
}

# Main function
main() {
    echo "=== Comprehensive Security Scanner ==="
    echo "Log file: $LOG_FILE"
    echo
    
    log "Security scan started"
    
    # Run all checks
    network_discovery
    port_scanning
    vulnerability_check
    system_security_check
    
    log "Security scan completed"
    
    echo
    echo "Scan complete! Check $LOG_FILE for details."
}

# Run the main function
main
```

**Exercise 11.1:** Add email notification when the scan finds critical issues.

---

## **Part 12: Practice Exercises - Build Your Skills**

### **Easy Exercises:**
1. **Greeting Script**: Ask for user's name and time of day, then give appropriate greeting
2. **File Counter**: Count how many files are in a directory and display the result
3. **Number Guesser**: Computer picks random number, user tries to guess it

### **Medium Exercises:**
1. **Password Generator**: Create random passwords of specified length
2. **Website Status Checker**: Check if websites are up or down
3. **Log File Analyzer**: Count how many times "ERROR" appears in a log file

### **Hard Exercises:**
1. **Automated Installer**: Script that installs and configures multiple software packages
2. **Network Monitor**: Continuously monitor network connectivity and log outages
3. **Security Hardener**: Automatically apply security settings to a Linux system

---

## **Part 13: Next Steps - Continue Learning**

### **What to Learn Next:**
1. **Regular Expressions** - Powerful text pattern matching
2. **AWK and SED** - Advanced text processing
3. **Cron Jobs** - Schedule scripts to run automatically
4. **Remote Execution** - Run scripts on other computers
5. **Error Handling** - Make your scripts more reliable

### **Practice Tips:**
- Start small and build up gradually
- Comment your code so you remember what it does
- Test each part as you build it
- Don't be afraid to make mistakes - that's how you learn!
- Look at other people's scripts to learn new techniques

---

## **Conclusion**

Congratulations! You've gone from writing your first "Hello World" script to creating sophisticated security automation tools. Remember:

- **Practice regularly** - Scripting is a skill that improves with use
- **Start simple** - Even professional scripts begin with basic concepts
- **Build gradually** - Add complexity step by step
- **Don't be afraid to experiment** - You can always undo changes

Keep this guide handy and refer back to it as you continue your bash scripting journey. Happy scripting! 
