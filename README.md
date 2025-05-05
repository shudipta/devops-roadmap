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

### 🔧 03. Git & Version Control

#### 🧠 Why it’s important:

DevOps engineers manage IaC, pipelines, scripts, and configs. All of that lives in Git.

##### 🔍 Key Commands:

```bash
git init
git clone <repo>
git status
git add .
git commit -m "Initial commit"
git push origin main
git pull
```

##### ✅ Practice:

01. Create a GitHub repo called `devops-sandbox`
02. Clone it locally
03. Write a bash script in it (backup.sh)
04. Push changes

##### 🛠 Task:

- [ ] Create branches (`git checkout -b feature/xyz`)
- [ ] Make a pull request via GitHub
- [ ] Merge and resolve conflicts

## 📘 Resources to Study:

- [Learn Shell - Interactive](https://www.learnshell.org/)
- [Git Book (Pro Git)](https://git-scm.com/book/en/v2)
- [LinuxCommand.org](http://linuxcommand.org/)

## ✅ Deliverables for Stage 1:

- [ ] Daily automated backup shell script with cron
- [ ] GitHub repo with your Linux/Git practice
- [ ] Hands-on use of curl, grep, awk, and sed
- [ ] Notes on 10 essential Linux commands
