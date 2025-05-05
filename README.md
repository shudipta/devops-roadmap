# devops-roadmap

A detailed DevOps roadmap with explanations, practice tasks, and real-world examples.

## DevOps Roadmap – Stage 1: Fundamentals

This section focuses on Stage 1: Fundamentals. I’ll continue step-by-step and build out the entire series for you.

### 🧑‍💻 Linux & Shell Scripting

#### 🧠 Why it’s important:

DevOps tools run on Linux. You’ll often work in CLI environments on remote servers (SSH), containers, and VMs.

* **🔍 Key Topics:**

  | Command/Concept |	What It Does |
  | --------------- | ------------ |
  | cd, ls, pwd	| Navigate directories |
  | chmod, chown |	Change file permissions/ownership |
  | grep, awk, sed |	Filter and process text data |
  | ps, top, kill	| View or terminate processes |
  | crontab |	Schedule scripts |
  | ssh |	Remote server access |

* **✅ Practice:**

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

* **🛠 Task:**
  - Write a bash script to back up a directory to a .tar.gz file.
  - Automate it using cron to run every day at 1AM.

