# **INT302: Kali Linux Tools and System Security – Lab 1: Advanced Reconnaissance and Information Gathering**

## **Lab Overview**

This comprehensive lab introduces advanced reconnaissance techniques essential for professional penetration testing and security assessment. You'll master both passive and active information gathering methods using Kali Linux tools to build detailed target profiles. Beyond basic commands, you'll learn to automate reconnaissance, analyze results, and document findings for professional security reports.

---

## **Lab Objectives**

By the end of this lab, you will be able to:
1. **Master Basic Reconnaissance**: Use `ping`, `whois`, and `nslookup` for initial target profiling
2. **Conduct Advanced DNS Analysis**: Extract comprehensive DNS records and identify subdomains
3. **Perform Passive Intelligence Gathering**: Leverage public sources without direct target interaction
4. **Automate Reconnaissance Workflows**: Create bash scripts for efficient information gathering
5. **Document and Analyze Findings**: Generate professional reconnaissance reports
6. **Understand Legal and Ethical Boundaries**: Conduct reconnaissance within proper scope and authorization

---

## **Tools Used**
- **Kali Linux**: Penetration testing distribution
- **Terminal**: Command-line interface
- **dig**: Advanced DNS query tool
- **theHarvester**: Passive intelligence gathering
- **sublist3r**: Subdomain enumeration tool
- **Bash Scripting**: Automation of reconnaissance tasks

---

## **Prerequisites**
- Basic Kali Linux familiarity
- Internet access for domain lookups
- Understanding of DNS concepts
- **Legal Notice**: Only test domains you own or have explicit permission to assess

---

## **Part 1: Fundamental Reconnaissance Techniques**

### **Exercise 1.1: Advanced Target Profiling with `ping`**

**Learning Objective**: Understand how ICMP protocols work and extract maximum information from basic connectivity tests.

#### **Step 1: Basic Ping Analysis**
```bash
# Basic domain ping
ping -c 4 google.com

# Output explanation:
# - '-c 4': Send 4 packets then stop
# - '64 bytes': Packet size
# - 'icmp_seq=1': Sequence number
# - 'ttl=57': Time to live (indicates OS/network distance)
# - 'time=15.4 ms': Round-trip time
```

#### **Step 2: Advanced Ping Techniques**
```bash
# Ping with timestamp for network analysis
ping -D -c 5 google.com

# Flood ping for network stress testing (use with caution)
ping -f -c 100 target-domain.com

# Ping with specific packet size
ping -s 1000 -c 4 google.com

# Record route ping (if supported)
ping -R -c 4 google.com
```

#### **Step 3: Create a Target Analysis Script**
```bash
nano basic_recon.sh
```

```bash
#!/bin/bash
# Basic Reconnaissance Script
# Usage: ./basic_recon.sh <domain>

DOMAIN="$1"
LOG_FILE="recon_${DOMAIN}_$(date +%Y%m%d_%H%M%S).txt"

echo "🎯 Starting Basic Reconnaissance for: $DOMAIN" | tee "$LOG_FILE"
echo "==========================================" | tee -a "$LOG_FILE"

# Function to perform ping analysis
ping_analysis() {
    echo "🔍 Ping Analysis for $DOMAIN" | tee -a "$LOG_FILE"
    echo "----------------------------------------" | tee -a "$LOG_FILE"
    
    if ping -c 4 "$DOMAIN" > /dev/null 2>&1; then
        echo "✅ Target is reachable" | tee -a "$LOG_FILE"
        ping -c 4 "$DOMAIN" | tee -a "$LOG_FILE"
        
        # Extract IP address from ping
        IP_ADDRESS=$(ping -c 1 "$DOMAIN" | head -1 | cut -d'(' -f2 | cut -d')' -f1)
        echo "📡 IP Address: $IP_ADDRESS" | tee -a "$LOG_FILE"
    else
        echo "❌ Target is not reachable via ICMP" | tee -a "$LOG_FILE"
    fi
    echo "" | tee -a "$LOG_FILE"
}

ping_analysis "$DOMAIN"
```

**Make it executable and test:**
```bash
chmod +x basic_recon.sh
./basic_recon.sh google.com
```

#### **Exercise Tasks**:
1. **TTL Analysis**: 
   - Ping `microsoft.com`, `apple.com`, and `ubuntu.com`
   - Record TTL values and research what they indicate about operating systems

2. **Network Performance**:
   - Compare response times for domains in different geographic regions
   - Analyze packet loss patterns

**Record Your Findings**:
| Domain | IP Address | Average Response Time | TTL Value | Inferred OS |
|--------|------------|---------------------|-----------|-------------|
| google.com | | | | |
| microsoft.com | | | | |
| github.com | | | | |

---

## **Part 2: Advanced Domain Intelligence**

### **Exercise 2.1: Comprehensive WHOIS Analysis**

**Learning Objective**: Extract and interpret domain registration data for threat intelligence.

#### **Step 1: Basic WHOIS Query**
```bash
# Basic whois lookup
whois google.com

# Save output to file for analysis
whois google.com > google_whois.txt
```

#### **Step 2: Advanced WHOIS Techniques**
```bash
# Query specific WHOIS server
whois -h whois.verisign-grs.com google.com

# Show brief information
whois -q google.com

# Parse specific information fields
whois google.com | grep -i "creation date"
whois google.com | grep -i "registrar"
whois google.com | grep -i "name server"
```

#### **Step 3: Create WHOIS Analysis Function**
Add to your `basic_recon.sh` script:

```bash
# Function to perform whois analysis
whois_analysis() {
    local domain="$1"
    echo "📋 WHOIS Analysis for $domain" | tee -a "$LOG_FILE"
    echo "----------------------------------------" | tee -a "$LOG_FILE"
    
    if command -v whois >/dev/null 2>&1; then
        # Extract key information
        echo "📍 Registrar Information:" | tee -a "$LOG_FILE"
        whois "$domain" | grep -i "registrar" | head -5 | tee -a "$LOG_FILE"
        
        echo "" | tee -a "$LOG_FILE"
        echo "📅 Dates Information:" | tee -a "$LOG_FILE"
        whois "$domain" | grep -E -i "(creation date|expiration|updated)" | head -5 | tee -a "$LOG_FILE"
        
        echo "" | tee -a "$LOG_FILE"
        echo "🌍 Contact Information:" | tee -a "$LOG_FILE"
        whois "$domain" | grep -E -i "(country|state|email)" | head -5 | tee -a "$LOG_FILE"
        
        echo "" | tee -a "$LOG_FILE"
        echo "🔗 Name Servers:" | tee -a "$LOG_FILE"
        whois "$domain" | grep -i "name server" | head -10 | tee -a "$LOG_FILE"
    else
        echo "❌ whois command not available" | tee -a "$LOG_FILE"
    fi
    echo "" | tee -a "$LOG_FILE"
}
```

#### **Exercise Tasks**:
1. **Domain History Analysis**:
   - Compare creation dates of `netflix.com` vs `hulu.com`
   - Identify the registrar for `twitter.com`

2. **Geographic Analysis**:
   - Determine the registered country for `alibaba.com`
   - Find administrative contact email patterns

**Analysis Questions**:
1. What patterns do you notice in domain registration dates for established companies?
2. How might registrar information be useful in a security assessment?
3. What privacy protection services are commonly used?

---

## **Part 3: Comprehensive DNS Analysis**

### **Exercise 3.1: Advanced DNS Reconnaissance with `nslookup` and `dig`**

**Learning Objective**: Master DNS enumeration to map target infrastructure.

#### **Step 1: Basic nslookup Usage**
```bash
# Interactive nslookup mode
nslookup
> set type=any
> google.com
> server 8.8.8.8  # Use specific DNS server
> exit

# Command-line mode
nslookup -type=ANY google.com
```

#### **Step 2: Comprehensive DNS Record Analysis**
```bash
# Different record types
nslookup -type=A google.com      # IPv4 addresses
nslookup -type=AAAA google.com   # IPv6 addresses
nslookup -type=MX google.com     # Mail servers
nslookup -type=TXT google.com    # Text records
nslookup -type=NS google.com     # Name servers
nslookup -type=CNAME google.com  # Canonical names
```

#### **Step 3: Using `dig` for Advanced DNS Analysis**
```bash
# Comprehensive DNS query
dig google.com ANY

# Specific record types
dig google.com A +short
dig google.com MX +short
dig google.com TXT +short

# Trace DNS resolution path
dig google.com +trace

# Query specific DNS server
dig @8.8.8.8 google.com
```

#### **Step 4: Create DNS Analysis Function**
Add to your reconnaissance script:

```bash
# Function to perform DNS analysis
dns_analysis() {
    local domain="$1"
    echo "🌐 DNS Analysis for $domain" | tee -a "$LOG_FILE"
    echo "----------------------------------------" | tee -a "$LOG_FILE"
    
    echo "📍 A Records (IPv4):" | tee -a "$LOG_FILE"
    dig "$domain" A +short | tee -a "$LOG_FILE"
    
    echo "" | tee -a "$LOG_FILE"
    echo "🔷 AAAA Records (IPv6):" | tee -a "$LOG_FILE"
    dig "$domain" AAAA +short | tee -a "$LOG_FILE"
    
    echo "" | tee -a "$LOG_FILE"
    echo "📧 MX Records (Mail Servers):" | tee -a "$LOG_FILE"
    dig "$domain" MX +short | tee -a "$LOG_FILE"
    
    echo "" | tee -a "$LOG_FILE"
    echo "📝 TXT Records:" | tee -a "$LOG_FILE"
    dig "$domain" TXT +short | tee -a "$LOG_FILE"
    
    echo "" | tee -a "$LOG_FILE"
    echo "🔗 NS Records (Name Servers):" | tee -a "$LOG_FILE"
    dig "$domain" NS +short | tee -a "$LOG_FILE"
    
    echo "" | tee -a "$LOG_FILE"
    echo "🔄 CNAME Records:" | tee -a "$LOG_FILE"
    dig "$domain" CNAME +short | tee -a "$LOG_FILE"
}
```

#### **Exercise Tasks**:
1. **DNS Record Mapping**:
   - Map all DNS records for `microsoft.com`
   - Identify mail servers for `amazon.com`
   - Find SPF/DKIM records in TXT entries

2. **DNS Infrastructure Analysis**:
   - Compare name servers across different domains
   - Identify CDN usage through CNAME records

**DNS Analysis Table**:
| Domain | Primary IP | Mail Servers | Name Servers | CDN Detected |
|--------|------------|--------------|--------------|--------------|
| spotify.com | | | | |
| linkedin.com | | | | |
| github.com | | | | |

---

## **Part 4: Passive Intelligence Gathering**

### **Exercise 4.1: Using theHarvester for OSINT**

**Learning Objective**: Gather information without direct target interaction.

#### **Step 1: Install and Configure theHarvester**
```bash
# Update Kali Linux
sudo apt update

# Install theHarvester
sudo apt install theharvester

# Verify installation
theHarvester -h
```

#### **Step 2: Basic theHarvester Usage**
```bash
# Search for emails, subdomains, and hosts
theHarvester -d microsoft.com -l 100 -b google

# Search multiple sources
theHarvester -d target.com -l 200 -b google,bing,linkedin

# Save results to file
theHarvester -d target.com -l 100 -b all -f results.html
```

#### **Step 3: Create Passive Intelligence Script**
```bash
nano passive_intel.sh
```

```bash
#!/bin/bash
# Passive Intelligence Gathering Script
# Usage: ./passive_intel.sh <domain>

DOMAIN="$1"
PASSIVE_LOG="passive_intel_${DOMAIN}_$(date +%Y%m%d_%H%M%S).txt"

echo "🕵️ Passive Intelligence Gathering for: $DOMAIN" | tee "$PASSIVE_LOG"
echo "==========================================" | tee -a "$PASSIVE_LOG"

# Function to run theHarvester
run_theharvester() {
    echo "🔍 Running theHarvester..." | tee -a "$PASSIVE_LOG"
    echo "----------------------------------------" | tee -a "$PASSIVE_LOG"
    
    if command -v theHarvester >/dev/null 2>&1; then
        theHarvester -d "$DOMAIN" -l 100 -b google,bing,linkedin -f "harvest_${DOMAIN}.html"
        echo "✅ theHarvester completed. Results saved to harvest_${DOMAIN}.html" | tee -a "$PASSIVE_LOG"
    else
        echo "❌ theHarvester not installed" | tee -a "$PASSIVE_LOG"
    fi
    echo "" | tee -a "$PASSIVE_LOG"
}

# Function to check domain with sublist3r
run_sublist3r() {
    echo "🔎 Running Subdomain Enumeration..." | tee -a "$PASSIVE_LOG"
    echo "----------------------------------------" | tee -a "$PASSIVE_LOG"
    
    if command -v sublist3r >/dev/null 2>&1; then
        sublist3r -d "$DOMAIN" -o "subdomains_${DOMAIN}.txt"
        echo "✅ Subdomain enumeration completed." | tee -a "$PASSIVE_LOG"
        echo "📋 Discovered subdomains:" | tee -a "$PASSIVE_LOG"
        cat "subdomains_${DOMAIN}.txt" | tee -a "$PASSIVE_LOG"
    else
        echo "❌ sublist3r not installed" | tee -a "$PASSIVE_LOG"
    fi
    echo "" | tee -a "$PASSIVE_LOG"
}

run_theharvester "$DOMAIN"
run_sublist3r "$DOMAIN"
```

#### **Exercise Tasks**:
1. **Email Harvesting**:
   - Use theHarvester to find emails associated with a domain
   - Analyze email naming conventions

2. **Subdomain Discovery**:
   - Identify subdomains for `google.com`
   - Categorize subdomains by function (api, admin, mail, etc.)

---

## **Part 5: Automated Reconnaissance Framework**

### **Exercise 5.1: Build Comprehensive Reconnaissance Script**

**Learning Objective**: Create an automated tool for complete target assessment.

#### **Step 1: Create Advanced Reconnaissance Script**
```bash
nano advanced_recon.sh
```

```bash
#!/bin/bash
# Advanced Reconnaissance Framework
# Usage: ./advanced_recon.sh <domain>

DOMAIN="$1"
OUTPUT_DIR="recon_${DOMAIN}_$(date +%Y%m%d_%H%M%S)"
COMPREHENSIVE_REPORT="${OUTPUT_DIR}/comprehensive_report.txt"

# Create output directory
mkdir -p "$OUTPUT_DIR"

echo "🎯 Advanced Reconnaissance Framework" | tee "$COMPREHENSIVE_REPORT"
echo "Target: $DOMAIN" | tee -a "$COMPREHENSIVE_REPORT"
echo "Date: $(date)" | tee -a "$COMPREHENSIVE_REPORT"
echo "==========================================" | tee -a "$COMPREHENSIVE_REPORT"

# Function to perform comprehensive ping analysis
advanced_ping_analysis() {
    echo "🔍 Advanced Ping Analysis" | tee -a "$COMPREHENSIVE_REPORT"
    echo "----------------------------------------" | tee -a "$COMPREHENSIVE_REPORT"
    
    local ping_file="${OUTPUT_DIR}/ping_analysis.txt"
    ping -c 10 "$DOMAIN" > "$ping_file"
    
    # Analyze ping statistics
    local avg_ping=$(grep "avg" "$ping_file" | awk -F'/' '{print $5}')
    local packet_loss=$(grep "packet loss" "$ping_file" | awk '{print $6}')
    
    echo "📊 Network Statistics:" | tee -a "$COMPREHENSIVE_REPORT"
    echo "  Average RTT: $avg_ping ms" | tee -a "$COMPREHENSIVE_REPORT"
    echo "  Packet Loss: $packet_loss" | tee -a "$COMPREHENSIVE_REPORT"
    echo "" | tee -a "$COMPREHENSIVE_REPORT"
}

# Function for comprehensive DNS reconnaissance
comprehensive_dns_scan() {
    echo "🌐 Comprehensive DNS Analysis" | tee -a "$COMPREHENSIVE_REPORT"
    echo "----------------------------------------" | tee -a "$COMPREHENSIVE_REPORT"
    
    local dns_file="${OUTPUT_DIR}/dns_records.txt"
    
    # Get all DNS record types
    for record in A AAAA MX TXT NS SOA CNAME; do
        echo "📝 $record Records:" | tee -a "$COMPREHENSIVE_REPORT"
        dig "$DOMAIN" $record +short | tee -a "$COMPREHENSIVE_REPORT" | tee -a "$dns_file"
        echo "" | tee -a "$COMPREHENSIVE_REPORT"
    done
    
    # DNS reputation check
    echo "🛡️ DNS Blacklist Check:" | tee -a "$COMPREHENSIVE_REPORT"
    local domain_ip=$(dig +short "$DOMAIN" | head -1)
    echo "Checking IP $domain_ip against blacklists..." | tee -a "$COMPREHENSIVE_REPORT"
    echo "" | tee -a "$COMPREHENSIVE_REPORT"
}

# Function to generate reconnaissance summary
generate_summary() {
    echo "📈 Reconnaissance Summary" | tee -a "$COMPREHENSIVE_REPORT"
    echo "----------------------------------------" | tee -a "$COMPREHENSIVE_REPORT"
    
    local ip_count=$(dig "$DOMAIN" A +short | wc -l)
    local mx_count=$(dig "$DOMAIN" MX +short | wc -l)
    local ns_count=$(dig "$DOMAIN" NS +short | wc -l)
    
    echo "📊 Infrastructure Overview:" | tee -a "$COMPREHENSIVE_REPORT"
    echo "  IP Addresses: $ip_count" | tee -a "$COMPREHENSIVE_REPORT"
    echo "  Mail Servers: $mx_count" | tee -a "$COMPREHENSIVE_REPORT"
    echo "  Name Servers: $ns_count" | tee -a "$COMPREHENSIVE_REPORT"
    echo "" | tee -a "$COMPREHENSIVE_REPORT"
    
    echo "💡 Security Observations:" | tee -a "$COMPREHENSIVE_REPORT"
    # Add automated security observations based on findings
    echo "  - Check for SPF/DKIM/DMARC records in TXT" | tee -a "$COMPREHENSIVE_REPORT"
    echo "  - Verify name server security" | tee -a "$COMPREHENSIVE_REPORT"
    echo "  - Analyze subdomain structure" | tee -a "$COMPREHENSIVE_REPORT"
    echo "" | tee -a "$COMPREHENSIVE_REPORT"
}

# Main execution
main() {
    if [ -z "$DOMAIN" ]; then
        echo "Usage: $0 <domain>"
        exit 1
    fi
    
    echo "🚀 Starting comprehensive reconnaissance..." | tee -a "$COMPREHENSIVE_REPORT"
    echo "" | tee -a "$COMPREHENSIVE_REPORT"
    
    advanced_ping_analysis
    comprehensive_dns_scan
    generate_summary
    
    echo "✅ Reconnaissance complete!" | tee -a "$COMPREHENSIVE_REPORT"
    echo "📁 Results saved in: $OUTPUT_DIR" | tee -a "$COMPREHENSIVE_REPORT"
    echo "📄 Main report: $COMPREHENSIVE_REPORT" | tee -a "$COMPREHENSIVE_REPORT"
}

main "$@"
```

#### **Step 2: Run Comprehensive Reconnaissance**
```bash
chmod +x advanced_recon.sh
./advanced_recon.sh example.com
```

---

## **Part 6: Professional Reporting and Analysis**

### **Exercise 6.1: Create Reconnaissance Report Template**

**Learning Objective**: Document findings professionally for security assessments.

#### **Step 1: Create Report Template**
```bash
nano recon_report_template.md
```

```markdown
# Security Reconnaissance Report

## Executive Summary
**Target**: [Domain Name]  
**Assessment Date**: [Date]  
**Scope**: Passive information gathering  
**Overall Risk Level**: [Low/Medium/High]

## 1. Target Overview
- **Domain**: [domain.com]
- **IP Address**: [Primary IP]
- **Registrar**: [Registrar Name]
- **Registration Date**: [Date]
- **Expiration Date**: [Date]

## 2. Network Infrastructure
### 2.1 IP Addresses
- Primary: [IP Address]
- Additional: [List additional IPs]

### 2.2 Network Performance
- Average Response Time: [Time] ms
- Packet Loss: [Percentage]%

## 3. DNS Configuration
### 3.1 Name Servers
- [NS1]
- [NS2]

### 3.2 Mail Servers
- [MX1 - Priority 10]
- [MX2 - Priority 20]

### 3.3 Security Records
- SPF: [Present/Absent]
- DKIM: [Present/Absent]
- DMARC: [Present/Absent]

## 4. Subdomain Analysis
### 4.1 Discovered Subdomains
- [subdomain1.domain.com]
- [subdomain2.domain.com]

## 5. Security Observations
### 5.1 Strengths
- [Positive finding 1]
- [Positive finding 2]

### 5.2 Concerns
- [Security concern 1]
- [Security concern 2]

## 6. Recommendations
1. [Recommendation 1]
2. [Recommendation 2]

## 7. Additional Information
- Tools Used: [List of tools]
- Assessment Type: Passive reconnaissance
- Legal Considerations: Conducted within authorized scope

---
*Report generated automatically by Advanced Reconnaissance Framework*
```

---

## **Lab Deliverables and Assessment**

### **Required Submissions**:
1. **Completed reconnaissance scripts** (`basic_recon.sh`, `passive_intel.sh`, `advanced_recon.sh`)
2. **Comprehensive report** for three different domains using your template
3. **Analysis document** answering the critical thinking questions

### **Critical Thinking Questions**:
1. **Legal and Ethical Considerations**:
   - What constitutes authorized vs unauthorized reconnaissance?
   - How do you ensure your activities remain within legal boundaries?

2. **Technical Analysis**:
   - What DNS misconfigurations commonly lead to security vulnerabilities?
   - How can TTL values be used in network mapping?

3. **Strategic Thinking**:
   - How would you prioritize findings for a penetration test?
   - What additional reconnaissance would you conduct for a comprehensive assessment?

### **Grading Rubric**:
| Category | Excellent (4) | Good (3) | Satisfactory (2) | Needs Improvement (1) |
|----------|---------------|----------|------------------|---------------------|
| **Tool Proficiency** | Mastered all tools with advanced options | Competent with basic tools | Basic understanding | Struggles with fundamental usage |
| **Script Development** | Created comprehensive automation | Developed functional scripts | Basic scripting ability | Limited scripting skills |
| **Analysis Depth** | Deep insights with strategic recommendations | Good analysis with practical findings | Basic observations | Superficial analysis |
| **Documentation** | Professional reports with executive summary | Clear documentation | Basic notes | Poor documentation |
| **Legal Awareness** | Strong understanding of ethics and scope | Good ethical understanding | Basic awareness | Limited ethical consideration |

---

## **Conclusion and Next Steps**

### **Key Skills Developed**:
- ✅ Advanced DNS analysis and enumeration
- ✅ Passive intelligence gathering techniques
- ✅ Automated reconnaissance workflows
- ✅ Professional security reporting
- ✅ Ethical assessment boundaries

### **Real-World Applications**:
- Penetration testing engagements
- Security compliance assessments
- Threat intelligence operations
- Incident response preparation

### **Next Lab Preview**: 
**INT302 Lab 2: Vulnerability Scanning and Network Mapping**
- Learn to use Nmap for comprehensive network scanning
- Conduct vulnerability assessments with OpenVAS
- Map network topology and identify attack surfaces
- Automate scanning workflows for large environments

---

## **Additional Resources**

### **Recommended Tools for Further Learning**:
- **Maltego**: Visual link analysis for intelligence gathering
- **Shodan**: Search engine for Internet-connected devices
- **Recon-ng**: Web reconnaissance framework
- **SpiderFoot**: Open source intelligence automation

### **Reference Materials**:
- NIST Cybersecurity Framework
- OSSTMM (Open Source Security Testing Methodology Manual)
- PTES (Penetration Testing Execution Standard)

**Congratulations on completing Advanced Reconnaissance Lab 1!**

You've built a solid foundation in information gathering techniques that will serve you throughout your cybersecurity career. Remember: always conduct reconnaissance ethically and with proper authorization.
