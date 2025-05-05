# devops-roadmap

A detailed DevOps roadmap with explanations, practice tasks, and real-world examples.

## DevOps Roadmap – Stage 1: Fundamentals

This section focuses on Stage 1: Fundamentals. I’ll continue step-by-step and build out the entire series for you.

### 🧑‍💻 01. Linux & Shell Scripting

#### 🧠 Why it’s important:

DevOps tools run on Linux. You’ll often work in CLI environments on remote servers (SSH), containers, and VMs.

##### **🔍 Key Topics:**

| Command/Concept |	What It Does |
| --------------- | ------------ |
| cd, ls, pwd	| Navigate directories |
| chmod, chown |	Change file permissions/ownership |
| grep, awk, sed |	Filter and process text data |
| ps, top, kill	| View or terminate processes |
| crontab |	Schedule scripts |
| ssh |	Remote server access |

##### **✅ Practice:**

```bash
# List all files including hidden
ls -la
  
# Find all .log files in /var/log
find /var/log -name "*.log"

# Replace "error" with "issue" in a file
sed -i 's/error/issue/g' filename.txt
  
# Check memory and CPU usage
free -m
top
```
##### **🛠 Task:**

- [ ] Write a bash script to back up a directory to a .tar.gz file.
- [ ] Automate it using cron to run every day at 1AM.

### 🌐 02. Networking Basics for DevOps

#### 🧠 Why it’s important:

Understanding how data flows in a network is key for troubleshooting, firewall rules, ports, and DNS.

##### 🔍 Key Concepts:

IP address (e.g. 192.168.0.1)

Port (e.g. 80, 443, 22)

DNS – Maps domain to IP

TCP/UDP – Transport protocols

HTTP Methods – GET, POST, PUT, DELETE

##### ✅ Practice:

```bash
# Check DNS resolution
nslookup google.com

# Check if a service is reachable
curl -I https://example.com

# Open port test
nc -zv google.com 443
```

##### 🛠 Task:

- [ ] Use curl or httpie to simulate requests to a local or remote API.
- [ ] Use tcpdump or wireshark to sniff packets locally (optional advanced).
