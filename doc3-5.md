
## **Processess**
A **process** in Linux is an instance of a running program. The Linux operating system manages processes to allocate system resources efficiently. Every process has a unique **Process ID (PID)** and operates within a user-defined execution environment.

### **Types of Processes in Linux**
- **Foreground Process**: A process that runs in the terminal and requires user interaction.
- **Background Process**: A process that runs without user interaction.
- **Daemon Process**: A process that runs in the background continuously (e.g., system services).
- **Zombie Process**: A completed process that still has an entry in the process table.
- **Orphan Process**: A process whose parent has terminated but is still running.

### **Cybersecurity Considerations**
- **Malicious Processes**: Attackers often use disguised or hidden processes to run malware.
- **Process Monitoring**: Regularly inspecting running processes can help detect intrusions.
- **Privilege Escalation Risks**: Some processes run with elevated privileges; compromising them can allow attackers to gain root access.

---

## **2. Viewing and Managing Processes**
Linux provides several tools to monitor and manage processes.

### **Listing Active Processes**
#### **1. Using `ps` (Process Status)**
The `ps` command provides a snapshot of currently running processes.
```bash
ps aux
```
- `a` → Show processes from all users.
- `u` → Display user-oriented format.
- `x` → Show processes without a controlling terminal.

To display hierarchical processes:
```bash
ps -ef --forest
```
- `-e` → Show all processes.
- `-f` → Full-format listing.
- `--forest` → Show parent-child relationships.

#### **2. Using `top` (Real-Time Process Monitoring)**
```bash
top
```
- Displays dynamic, real-time information about system processes.
- Press `q` to exit.

Alternative: `htop` (interactive and more user-friendly)
```bash
htop
```

#### **Cybersecurity Considerations**
- **Detecting Rogue Processes**: Suspicious processes consuming unusual CPU or memory resources could be an indicator of malware.
- **Checking Unauthorized Privilege Escalation**: Processes running as `root` that shouldn’t be might indicate a security issue.

---

## **3. Managing Processes**

### **Starting a Process**
```bash
echo "Process Running" &
```
- `&` → Runs the process in the background.

### **Bringing a Background Process to Foreground**
```bash
fg %1
```
- `fg` → Brings a background process to the foreground.
- `%1` → Refers to the job number.

### **Stopping a Process**
```bash
kill -STOP 1234
```
- Sends `SIGSTOP` to suspend the process with **PID 1234**.

To resume the process:
```bash
kill -CONT 1234
```

### **Cybersecurity Considerations**
- **Preventing Unauthorized Process Termination**: Attackers may try to stop security-related processes such as firewalls or antivirus services.
- **Monitoring Process Integrity**: Ensure security services (like `fail2ban`, `iptables`, or intrusion detection systems) are always running.

---

## **4. Process Priorities & Scheduling**
Linux assigns each process a priority level, which determines how CPU time is allocated.

### **Checking Process Priority**
```bash
ps -eo pid,comm,pri,ni
```
- `pri` → Kernel scheduling priority.
- `ni` → User-set niceness level.

### **Adjusting Process Priority with `nice`**
Start a new process with lower priority:
```bash
nice -n 10 ./my_script.sh
```
- `-n 10` → Sets nice value to **10** (lower priority).

### **Changing Priority of a Running Process with `renice`**
```bash
renice -5 -p 1234
```
- `-5` → Increases priority (lower nice value).
- `-p 1234` → Targets process with PID **1234**.

### **Cybersecurity Considerations**
- **Ensuring Critical Security Processes Have High Priority**: Security services like **firewalls, intrusion detection systems, and authentication daemons** should run with high priority.

---

## **5. Identifying and Mitigating Malicious Processes**

### **Finding Hidden or Suspicious Processes**
```bash
ps aux | grep suspicious_process
```
- Look for unusual processes consuming high CPU or running under unexpected users.

### **Detecting Network-Connected Processes**
```bash
netstat -tulnp | grep LISTEN
```
- Identifies running processes that are listening for incoming network connections.

### **Checking for Malware with `lsof` (List Open Files)**
```bash
lsof -i
```
- Lists processes using network connections.

### **Preventing Process Injection Attacks**
Use **AppArmor** or **SELinux** to restrict process behavior:
```bash
sudo aa-status  # Check AppArmor status
```
```bash
sudo setenforce 1  # Enable SELinux enforcement
```

---

## **6. Monitoring System-Wide Processes for Security**

### **Finding the Process Using the Most CPU**
```bash
top -o %CPU
```
- Sorts processes by **CPU usage**.

### **Finding the Process Using the Most Memory**
```bash
top -o %MEM
```
- Sorts processes by **memory usage**.

### **Logging Process Activity**
```bash
strace -p 1234
```
- Monitors **system calls** made by the process with PID **1234**.

### **Cybersecurity Considerations**
- **Preventing Process Spoofing**: Ensure that no unexpected processes are running with system-critical names.
- **Using IDS (Intrusion Detection Systems)**: Tools like **Tripwire** can help monitor unauthorized changes in processes.
