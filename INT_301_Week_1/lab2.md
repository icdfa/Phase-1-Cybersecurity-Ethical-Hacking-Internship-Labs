# **Lab 2: Advanced Package Management and Application Deployment**

## **Enhanced Objectives**
In this lab, you will:
- Master Advanced Package Tool (APT) for comprehensive package management.
- Install, upgrade, and remove applications using command-line tools.
- Search for packages and manage repositories effectively.
- Troubleshoot dependency issues and resolve conflicts.
- Work with multiple package formats (DEB, Snap, source).
- Create and manage custom repositories.

## **Background / Scenario**
As a security professional, you often need to install specialized tools, maintain multiple versions of software, and troubleshoot dependency issues. This lab expands your package management skills beyond basic installation to include advanced scenarios you'll encounter in real-world engagements.

## **Required Resources**
- Kali Linux virtual machine (VM).
- Internet access.
- Minimum 20GB free disk space.

---

## **Instructions**

### **Part 1: Advanced APT Operations**

#### **Step 1: System Preparation**
```bash
# Update and upgrade the system
sudo apt update && sudo apt full-upgrade -y

# Install essential build tools
sudo apt install build-essential devscripts debhelper -y
```

**Exercise 1.1:** What is the difference between `apt upgrade` and `apt full-upgrade`?

#### **Step 2: Package Information and Dependency Analysis**
```bash
# Get detailed information about a package
apt show nmap

# List package dependencies
apt-cache depends nmap

# Find reverse dependencies (what packages depend on this one)
apt-cache rdepends python3

# Check if a package is installed
dpkg -l | grep python3
```

**Exercise 1.2:** What are the dependencies for the `wireshark` package? Which packages depend on `python3`?

#### **Step 3: Package Searching and Filtering**
```bash
# Search for packages with detailed output
apt search "password crack" --names-only

# Search by specific architecture
apt search "tool" | grep amd64

# List all available tools in a category
apt search "kali-tool-" | head -20
```

**Exercise 1.3:** Find three different password cracking tools available in Kali repositories.

### **Part 2: Advanced Installation Techniques**

#### **Step 1: Specific Version Installation**
```bash
# Check available versions of a package
apt-cache policy python3

# Install a specific version
sudo apt install python3=3.9.2-1

# Hold a package at current version to prevent updates
sudo apt-mark hold python3
```

**Exercise 2.1:** What version of python3 is currently available? What happens when you try to hold a package?

#### **Step 2: Download Packages Without Installing**
```bash
# Download a package for offline installation
apt download nmap

# Download with all dependencies
apt-get download --download-only nmap

# List downloaded packages
ls *.deb
```

#### **Step 3: Install from Local DEB Files**
```bash
# Install a local DEB package
sudo dpkg -i nmap*.deb

# Fix dependency issues if they occur
sudo apt install -f
```

**Exercise 2.2:** Download the `htop` package and install it from the local file. What happens if dependencies are missing?

### **Part 3: Dependency Management and Troubleshooting**

#### **Step 1: Dependency Resolution**
```bash
# Simulate installation to see what would happen
apt install -s metasploit-framework

# Check for broken dependencies
apt check

# Fix broken packages
sudo apt --fix-broken install
```

#### **Step 2: Package Removal Scenarios**
```bash
# Remove package but keep configuration files
sudo apt remove firefox-esr

# Remove package and configuration files
sudo apt purge firefox-esr

# Remove orphaned dependencies
sudo apt autoremove

# Clean package cache
sudo apt autoclean
```

**Exercise 3.1:** What's the difference between `remove` and `purge`? When would you use each?

### **Part 4: Repository Management**

#### **Step 1: Advanced Repository Configuration**
```bash
# View all repository sources
cat /etc/apt/sources.list
ls /etc/apt/sources.list.d/

# Add a custom repository (example with GitKraken)
echo "deb [arch=amd64] https://packagecloud.io/gitkraken/repos/any/ any main" | sudo tee /etc/apt/sources.list.d/gitkraken.list

# Add repository key
curl -L https://packagecloud.io/gitkraken/repos/gpgkey | sudo apt-key add -
```

#### **Step 2: Repository Priority and Pinning**
```bash
# Create preferences file for package pinning
sudo nano /etc/apt/preferences.d/custom-pinning

# Add content to pin specific packages
Package: *
Pin: release o=Kali
Pin-Priority: 900

Package: *
Pin: release o=Debian
Pin-Priority: 100
```

**Exercise 4.1:** Why would you want to pin packages from specific repositories?

### **Part 5: Alternative Package Managers**

#### **Step 1: Snap Package Management**
```bash
# Install snapd if not available
sudo apt install snapd

# Install packages using snap
sudo snap install code --classic
sudo snap install slack

# List installed snaps
snap list
```

#### **Step 2: Flatpak Installation**
```bash
# Install flatpak
sudo apt install flatpak

# Add flathub repository
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# Install applications
flatpak install flathub org.gimp.GIMP
```

**Exercise 5.1:** Compare the installation locations of APT, Snap, and Flatpak packages.

### **Part 6: Source Compilation and Installation**

#### **Step 1: Compile from Source**
```bash
# Create development directory
mkdir ~/src && cd ~/src

# Download and compile a tool from source (example: ffuf)
git clone https://github.com/ffuf/ffuf.git
cd ffuf
go build
sudo cp ffuf /usr/local/bin/

# Verify installation
ffuf --help
```

#### **Step 2: Create DEB Packages**
```bash
# Install packaging tools
sudo apt install dh-make devscripts

# Practice with a simple package
mkdir -p ~/packaging/mytool-1.0
cd ~/packaging/mytool-1.0
```

**Exercise 6.1:** What are the advantages and disadvantages of compiling from source vs using package managers?

### **Part 7: Advanced Troubleshooting Scenarios**

#### **Step 1: Dependency Hell Resolution**
```bash
# Simulate a complex dependency issue
sudo apt install kali-linux-default

# If conflicts occur, use aptitude for resolution
sudo apt install aptitude
sudo aptitude install kali-linux-default
```

#### **Step 2: Package Forensic Analysis**
```bash
# Examine package contents without installing
dpkg -c nmap*.deb

# Extract package contents
dpkg -x nmap*.deb /tmp/nmap-extract/

# Check package integrity
dpkg --verify nmap
```

**Exercise 7.1:** What files does the nmap package install on the system?

### **Part 8: Automation and Scripting**

#### **Step 1: Bulk Package Operations**
```bash
# Create a package list for installation
echo "htop vim git curl wget tree" > tools.txt

# Install multiple packages from list
xargs sudo apt install -y < tools.txt

# Export list of installed packages
dpkg --get-selections > installed_packages.txt
```

#### **Step 2: System Setup Script**
```bash
# Create an automated setup script
cat > setup_tools.sh << 'EOF'
#!/bin/bash
TOOLS="python3-pip git curl wget nmap wireshark tcpdump"
echo "Installing essential tools: $TOOLS"
sudo apt update
sudo apt install -y $TOOLS
echo "Installation complete"
EOF

chmod +x setup_tools.sh
./setup_tools.sh
```

## **Challenge Exercises**

**Challenge 1: Repository Migration**
- Add the Kali testing repository to your sources.list
- Install one package from testing while keeping the rest from stable
- Document the process and potential risks

**Challenge 2: Dependency Graph**
- Choose a complex package (like `kali-linux-large`)
- Create a dependency graph showing all required packages
- Use `apt-rdepends` or similar tools to generate the graph

**Challenge 3: Custom Package Creation**
- Create a simple script that displays system information
- Package it as a DEB file with proper dependencies
- Install and test your custom package

**Challenge 4: Recovery Scenario**
- Simulate a broken package situation by forcibly removing a critical dependency
- Document your troubleshooting steps to recover the system
- Time how long it takes to identify and fix the issue

## **Troubleshooting Common Issues**

1. **GPG Key Errors**
   ```bash
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys [KEY_ID]
   ```

2. **Repository 404 Errors**
   ```bash
   sudo apt update --fix-missing
   ```

3. **Locked Package Manager**
   ```bash
   sudo rm /var/lib/dpkg/lock
   sudo rm /var/lib/apt/lists/lock
   ```

## **Conclusion**
You have now mastered advanced package management techniques essential for cybersecurity professionals. These skills enable you to maintain systems efficiently, troubleshoot complex dependency issues, and deploy tools reliably across different environments.

## **Additional Resources**
- **Kali Linux Package Management**: https://www.kali.org/docs/general-use/apt/
- **Debian Administrator's Handbook**: https://debian-handbook.info/
- **APT User Guide**: https://wiki.debian.org/Apt
- **Snapcraft Documentation**: https://snapcraft.io/docs
