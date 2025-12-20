# Lab 2: Advanced Linux Command Shell Automation

---

## **Objectives**

By the end of this lab, students will be able to:
- Develop intelligent navigation systems with logging capabilities
- Create error-resistant file operation scripts
- Build interactive menu-driven applications
- Implement automated backup and monitoring solutions
- Apply advanced bash scripting techniques for system administration
- Design robust scripts with proper error handling and validation

---

## **Lab Introduction**

### **Purpose of This Lab**
Welcome, interns! This lab is designed to transform you from basic command line users into proficient Linux automation engineers. You'll learn to create intelligent, robust scripts that can handle real-world system administration tasks.

### **What You'll Achieve**
By completing this lab, you will be able to:
- Create scripts that remember and track their actions
- Build error-resistant file operations
- Develop interactive menu systems
- Implement automated backup solutions
- Monitor system health proactively

### **Lab Structure**
We'll progress from foundational concepts to advanced automation, with clear explanations at each step.

---

## **Part 1: Intelligent Navigation System**

### **Concept Overview: Why Smart Navigation?**

**The Problem**: Basic `cd` commands don't remember where you've been, making it hard to retrace steps or automate complex directory traversals.

**The Solution**: We'll create a navigation system that:
- Logs every directory change
- Allows you to see your navigation history
- Enables returning to previous directories
- Provides safety checks before navigating

### **Exercise 1.1: Building the Navigation Logger**

#### **Step 1: Understanding the Components**

Let's examine what each part of our script will do:

1. **History File**: A simple text file that records each directory change with timestamps
2. **Navigation Function**: A safe version of `cd` that checks if directories exist
3. **History Viewer**: A way to see where you've been
4. **Back Function**: Return to your previous location

#### **Step 2: Create the Script Foundation**

**Action**: Create a new script file
```bash
nano smart_navigator.sh
```

**Explanation**: We're using `nano` to create a new file. The `.sh` extension indicates this is a shell script.

#### **Step 3: Build the History Tracking System**

**Add this code to your file**:
```bash
#!/bin/bash
# smart_navigator.sh - Intelligent navigation with memory

# Configuration: Where to store our navigation history
NAVIGATION_HISTORY="$HOME/navigation_history.txt"
```

**Concept Explanation**:
- `#!/bin/bash`: This tells the system to use the bash shell to interpret this script
- `NAVIGATION_HISTORY`: This is a **variable** that stores the path to our history file
- `$HOME`: This expands to your home directory path

#### **Step 4: Create the Navigation Logger Function**

**Add this function**:
```bash
# Function to record each navigation in our history file
log_navigation() {
    # Get current timestamp and directory
    local timestamp=$(date +"%Y-%m-%d %H:%M:%S")
    local current_dir=$(pwd)
    
    # Append to history file
    echo "$timestamp | $current_dir" >> "$NAVIGATION_HISTORY"
    echo "📝 Navigation logged: $current_dir"
}
```

**Breaking Down the Function**:
- `log_navigation()`: Defines a reusable function
- `local timestamp`: Creates a variable that stores the current date/time
- `$(date +"%Y-%m-%d %H:%M:%S")`: Runs the `date` command and captures its output
- `$(pwd)`: Runs `pwd` (print working directory) and captures the output
- `>>`: Appends to a file (creates it if it doesn't exist)
- `echo`: Prints messages to the screen

#### **Step 5: Create Safe Navigation Function**

**Add this function**:
```bash
# Safe navigation function with error checking
smart_cd() {
    local target_dir="$1"
    
    echo "🧭 Attempting to navigate to: $target_dir"
    
    # Check if directory exists before navigating
    if [ -d "$target_dir" ]; then
        cd "$target_dir"
        log_navigation
        echo "✅ Successfully navigated to: $(pwd)"
    else
        echo "❌ Error: Directory '$target_dir' does not exist"
        return 1  # Return error code
    fi
}
```

**Understanding the Safety Checks**:
- `[ -d "$target_dir" ]`: Tests if the directory exists
- `if/then/else`: Conditional logic - only navigate if directory exists
- `return 1`: Returns an error code if navigation fails
- `$(pwd)`: Shows the new current directory after successful navigation

#### **Step 6: Create History Viewer**

**Add this function**:
```bash
# Display recent navigation history
show_history() {
    echo "=== 🕐 Recent Navigation History ==="
    
    # Check if history file exists
    if [ -f "$NAVIGATION_HISTORY" ]; then
        # Show last 10 entries
        tail -10 "$NAVIGATION_HISTORY"
    else
        echo "No navigation history found."
        echo "Start using smart_cd to build history!"
    fi
}
```

**Understanding History Display**:
- `[ -f "$NAVIGATION_HISTORY" ]`: Checks if the history file exists
- `tail -10`: Shows the last 10 lines of a file
- **Why last 10?**: This gives recent context without overwhelming you

### **Exercise 1.2: Testing Your Navigation System**

#### **Step 1: Make Your Script Executable**

**Action**:
```bash
chmod +x smart_navigator.sh
```

**Explanation**: 
- `chmod`: Change file permissions
- `+x`: Add execute permission
- This allows the script to be run as a program

#### **Step 2: Load Functions into Current Shell**

**Action**:
```bash
source smart_navigator.sh
```

**Explanation**:
- `source`: Loads the functions into your current shell session
- This makes `smart_cd` and `show_history` available as commands
- Without this, you could only run the entire script

#### **Step 3: Test Your Navigation System**

**Test 1: Navigate to existing directory**
```bash
smart_cd /tmp
```
**Expected Output**:
```
🧭 Attempting to navigate to: /tmp
📝 Navigation logged: /tmp
✅ Successfully navigated to: /tmp
```

**Test 2: Try to navigate to non-existent directory**
```bash
smart_cd /this_directory_does_not_exist
```
**Expected Output**:
```
🧭 Attempting to navigate to: /this_directory_does_not_exist
❌ Error: Directory '/this_directory_does_not_exist' does not exist
```

**Test 3: View your navigation history**
```bash
show_history
```
**Expected Output**:
```
=== 🕐 Recent Navigation History ===
2024-01-15 10:30:45 | /home/yourusername
2024-01-15 10:30:50 | /tmp
```

### **Discussion Questions for Interns**

1. **Error Handling**: What happens if you try to navigate to a file instead of a directory? How could we improve our error checking?

2. **History Management**: What would happen if the history file becomes very large? How could we implement automatic cleanup?

3. **Real-world Use**: When would this type of navigation tracking be particularly useful in system administration?

---

## **Part 2: Robust File Operations**

### **Concept Overview: Why Safe File Operations?**

**The Problem**: Basic file operations (`cp`, `mv`, `rm`) can be destructive if used incorrectly. Lost files and accidental overwrites are common.

**The Solution**: We'll create file operations that:
- Verify success of each operation
- Create backups before overwriting
- Handle errors gracefully
- Provide clear feedback

### **Exercise 2.1: Creating Safe File Operations**

#### **Step 1: Create File Operations Script**

**Action**:
```bash
nano file_manager.sh
```

#### **Step 2: Build Secure File Creation Function**

**Add this code**:
```bash
#!/bin/bash
# file_manager.sh - Safe file operations with verification

create_secure_file() {
    local file_path="$1"    # First argument: file path
    local content="$2"      # Second argument: file content
    local permissions="${3:-644}"  # Third argument: permissions (default: 644)
    
    echo "🛠️  Creating file: $file_path"
    
    # Extract directory path from full file path
    local dir_path=$(dirname "$file_path")
    
    # Create directory structure if it doesn't exist
    if [ ! -d "$dir_path" ]; then
        echo "📁 Creating directory structure: $dir_path"
        mkdir -p "$dir_path"
        
        # Verify directory was created
        if [ ! -d "$dir_path" ]; then
            echo "❌ Critical: Failed to create directory: $dir_path"
            return 1
        fi
    fi
    
    # Create file with content
    echo "$content" > "$file_path"
    
    # Set permissions
    chmod "$permissions" "$file_path"
    
    # Comprehensive verification
    if [ -f "$file_path" ]; then
        local actual_perms=$(stat -c "%a" "$file_path")
        local file_size=$(stat -c "%s" "$file_path")
        
        echo "✅ File creation successful!"
        echo "   📍 Location: $file_path"
        echo "   🔐 Permissions: $actual_perms"
        echo "   📊 Size: $file_size bytes"
        echo "   📝 Content: '$content'"
        return 0
    else
        echo "❌ File creation failed: $file_path"
        return 1
    fi
}
```

#### **Step 3: Understanding the Security Features**

**Directory Creation**:
- `$(dirname "$file_path")`: Extracts directory path from full file path
- `mkdir -p`: Creates parent directories if needed (`-p` flag)
- **Example**: For `/home/user/docs/report.txt`, it ensures `/home/user/docs/` exists

**Permission Management**:
- `${3:-644}`: Uses third argument or defaults to 644
- `chmod`: Changes file permissions
- `stat -c "%a"`: Gets actual permissions set on file

**Verification Steps**:
1. Check if directory was created
2. Check if file was created  
3. Verify permissions were set correctly
4. Display file size and content preview

#### **Step 4: Create Safe Move Function**

**Add this function**:
```bash
safe_move() {
    local source="$1"
    local destination="$2"
    local backup_suffix=".backup.$(date +%Y%m%d_%H%M%S)"
    
    echo "🚚 Moving: $source → $destination"
    
    # Validation checks
    if [ ! -e "$source" ]; then
        echo "❌ Source does not exist: $source"
        return 1
    fi
    
    if [ ! -r "$source" ]; then
        echo "❌ Cannot read source file: $source"
        return 1
    fi
    
    # Create backup if destination exists
    if [ -e "$destination" ]; then
        echo "⚠️  Destination exists! Creating backup..."
        cp -r "$destination" "$destination$backup_suffix"
        
        if [ ! -e "$destination$backup_suffix" ]; then
            echo "❌ Backup creation failed! Aborting move."
            return 1
        fi
        echo "✅ Backup created: $destination$backup_suffix"
    fi
    
    # Perform the move operation
    mv "$source" "$destination"
    
    # Verify the move was successful
    if [ -e "$destination" ] && [ ! -e "$source" ]; then
        echo "✅ Move operation successful!"
        echo "   📦 Source: $source"
        echo "   🎯 Destination: $destination"
        if [ -e "$destination$backup_suffix" ]; then
            echo "   💾 Backup: $destination$backup_suffix"
        fi
        return 0
    else
        echo "❌ Move operation failed!"
        echo "   Please check file permissions and disk space."
        return 1
    fi
}
```

### **Exercise 2.2: Testing File Operations**

#### **Step 1: Make Executable and Load**
```bash
chmod +x file_manager.sh
source file_manager.sh
```

#### **Step 2: Test Secure File Creation**

**Test 1: Create simple file**
```bash
create_secure_file "/tmp/intern_test/sample.txt" "Hello from the file manager!" 644
```

**Expected Output**:
```
🛠️  Creating file: /tmp/intern_test/sample.txt
📁 Creating directory structure: /tmp/intern_test
✅ File creation successful!
   📍 Location: /tmp/intern_test/sample.txt
   🔐 Permissions: 644
   📊 Size: 27 bytes
   📝 Content: 'Hello from the file manager!'
```

**Test 2: Test with existing directory**
```bash
create_secure_file "/tmp/intern_test/another.txt" "Second test file" 755
```

**Expected Output**:
```
🛠️  Creating file: /tmp/intern_test/another.txt
✅ File creation successful!
   📍 Location: /tmp/intern_test/another.txt
   🔐 Permissions: 755
   📊 Size: 15 bytes
   📝 Content: 'Second test file'
```

#### **Step 3: Test Safe Move Operations**

**Test 1: Move to new location**
```bash
echo "Source file content" > source_file.txt
safe_move "source_file.txt" "destination_file.txt"
```

**Expected Output**:
```
🚚 Moving: source_file.txt → destination_file.txt
✅ Move operation successful!
   📦 Source: source_file.txt
   🎯 Destination: destination_file.txt
```

**Test 2: Move with overwrite (backup test)**
```bash
echo "First version" > existing_file.txt
echo "Second version" > file_to_move.txt
safe_move "file_to_move.txt" "existing_file.txt"
```

**Expected Output**:
```
🚚 Moving: file_to_move.txt → existing_file.txt
⚠️  Destination exists! Creating backup...
✅ Backup created: existing_file.txt.backup.20240115_103045
✅ Move operation successful!
   📦 Source: file_to_move.txt
   🎯 Destination: existing_file.txt
   💾 Backup: existing_file.txt.backup.20240115_103045
```

### **Critical Thinking Exercise**

**Scenario Analysis**:
1. What happens if the disk is full during file creation?
2. How does our script handle permission denied errors?
3. What additional safety features could we add?

**Improvement Ideas**:
- Add file content verification (checksums)
- Implement rollback functionality for failed operations
- Add logging to a system log file

---

## **Part 3: Interactive Menu System**

### **Concept Overview: User-Friendly Automation**

**The Problem**: Complex scripts with many functions can be confusing for users. Command-line arguments are hard to remember.

**The Solution**: Create an interactive menu that:
- Presents clear options
- Handles user input validation
- Provides helpful feedback
- Allows easy access to all functions

### **Exercise 3.1: Building the Menu Interface**

#### **Step 1: Create Menu Script**
```bash
nano automation_dashboard.sh
```

#### **Step 2: Build Main Menu Function**
```bash
#!/bin/bash
# automation_dashboard.sh - User-friendly automation interface

# Source our previous scripts to get the functions
source smart_navigator.sh 2>/dev/null || echo "Note: smart_navigator.sh not found"
source file_manager.sh 2>/dev/null || echo "Note: file_manager.sh not found"

# Function to display main menu
show_main_menu() {
    clear
    echo "=========================================="
    echo "🤖 LINUX AUTOMATION DASHBOARD"
    echo "=========================================="
    echo ""
    echo "Navigation Tools:"
    echo "  1. 📂 Smart Navigation"
    echo "  2. 🕐 View Navigation History"
    echo ""
    echo "File Operations:"
    echo "  3. 🛠️  Create Secure File"
    echo "  4. 🚚 Safe File Move"
    echo "  5. 📊 System Information"
    echo ""
    echo "Utilities:"
    echo "  6. 🧹 Clean Temporary Files"
    echo "  7. 💾 Quick Backup"
    echo "  0. ❌ Exit"
    echo ""
    echo "=========================================="
}

# Function to handle menu selection
handle_menu_selection() {
    local choice
    read -p "Enter your choice [0-7]: " choice
    
    case $choice in
        1)
            smart_navigation_menu
            ;;
        2)
            show_history
            pause
            ;;
        3)
            file_creation_menu
            ;;
        4)
            file_move_menu
            ;;
        5)
            show_system_info
            pause
            ;;
        6)
            cleanup_menu
            ;;
        7)
            backup_menu
            ;;
        0)
            echo "👋 Thank you for using Automation Dashboard!"
            exit 0
            ;;
        *)
            echo "❌ Invalid option. Please try again."
            pause
            ;;
    esac
}

# Helper function to pause execution
pause() {
    read -p "Press [Enter] to continue..."
}
```

#### **Step 3: Create Sub-menus for Specific Functions**

**Add Smart Navigation Sub-menu**:
```bash
smart_navigation_menu() {
    clear
    echo "=========================================="
    echo "📂 SMART NAVIGATION MENU"
    echo "=========================================="
    echo ""
    echo "Current directory: $(pwd)"
    echo ""
    
    local target_dir
    read -p "Enter directory path to navigate to: " target_dir
    
    if [ -n "$target_dir" ]; then
        smart_cd "$target_dir"
    else
        echo "❌ No directory specified."
    fi
    
    pause
}
```

**Add File Creation Sub-menu**:
```bash
file_creation_menu() {
    clear
    echo "=========================================="
    echo "🛠️  SECURE FILE CREATION"
    echo "=========================================="
    echo ""
    
    local file_path
    local content
    local permissions
    
    read -p "Enter file path: " file_path
    read -p "Enter file content: " content
    read -p "Enter permissions (default 644): " permissions
    
    # Use default if no permissions specified
    if [ -z "$permissions" ]; then
        permissions="644"
    fi
    
    create_secure_file "$file_path" "$content" "$permissions"
    pause
}
```

#### **Step 4: Add System Information Function**
```bash
show_system_info() {
    clear
    echo "=========================================="
    echo "📊 SYSTEM INFORMATION"
    echo "=========================================="
    echo ""
    
    echo "💻 Hostname: $(hostname)"
    echo "🤵 Current User: $(whoami)"
    echo "📁 Working Directory: $(pwd)"
    echo ""
    
    echo "💾 Disk Usage:"
    df -h / | tail -1
    echo ""
    
    echo "🧠 Memory Usage:"
    free -h | head -2
    echo ""
    
    echo "📈 System Uptime:"
    uptime
}
```

#### **Step 5: Main Program Loop**
```bash
# Main program loop
main() {
    # Check if required functions are available
    if ! command -v smart_cd &> /dev/null; then
        echo "⚠️  Warning: Some functions not loaded properly"
        echo "   Make sure smart_navigator.sh and file_manager.sh are available"
        pause
    fi
    
    while true; do
        show_main_menu
        handle_menu_selection
    done
}

# Start the program
main
```

### **Exercise 3.2: Testing the Menu System**

#### **Step 1: Make Executable and Run**
```bash
chmod +x automation_dashboard.sh
./automation_dashboard.sh
```

#### **Step 2: Test Menu Navigation**

**Expected Behavior**:
1. Clear menu display with options 0-7
2. Ability to navigate through different functions
3. Proper error handling for invalid inputs
4. Return to main menu after each operation

#### **Step 3: Test Individual Functions**

**Test File Creation through Menu**:
- Select option 3
- Enter: `/tmp/menu_test.txt` for file path
- Enter: `Created via menu system` for content  
- Enter: `644` for permissions
- Verify file creation and return to menu

**Test System Information**:
- Select option 5
- View system statistics
- Press Enter to return to menu

### **Learning Reflection**

**Discussion Points**:
1. **User Experience**: How does the menu system improve usability compared to command-line arguments?
2. **Error Handling**: What happens if a user enters invalid data in the menus?
3. **Extensibility**: How easy would it be to add new functions to this menu system?
4. **Real-world Application**: Where could this type of interface be useful in system administration?

---

## **Part 4: Advanced Exercises**

### **Exercise 4.1: Automated Backup System**

**Challenge**: Create a backup system that:
- Creates timestamped backups
- Compresses the backups
- Maintains a rotation of backups
- Verifies backup integrity

**Starter Code**:
```bash
create_backup() {
    local source_dir="$1"
    local backup_dir="$2"
    local max_backups="${3:-5}"  # Default to 5 backups
    
    # Implementation guide:
    # 1. Check if source directory exists
    # 2. Create backup directory if needed
    # 3. Create timestamped backup file
    # 4. Compress the backup
    # 5. Verify the backup
    # 6. Clean up old backups beyond max_backups
    # 7. Provide detailed status report
}
```

### **Exercise 4.2: System Health Monitor**

**Challenge**: Create a monitoring script that:
- Checks disk space and alerts if low
- Monitors memory usage
- Checks critical services
- Sends alerts if issues detected

### **Exercise 4.3: Log File Analyzer**

**Challenge**: Create a script that:
- Analyzes log files for errors
- Generates summary reports
- Sends daily reports via email
- Archives old log files

---

## **Lab Completion Checklist**

- [ ] Successfully created and tested smart navigation system
- [ ] Implemented and verified safe file operations  
- [ ] Built and used interactive menu interface
- [ ] Understand error handling and verification concepts
- [ ] Can explain the purpose of each script component
- [ ] Completed at least one advanced exercise

## **Next Steps**

Congratulations on completing this lab! You now have practical experience with:
- Advanced bash scripting techniques
- Robust error handling
- User interface design for scripts
- System automation concepts

Continue practicing by modifying and extending these scripts. Try adding new features, improving error handling, or integrating with other system tools.

**Remember**: The best system administrators are those who automate themselves out of repetitive tasks! 
