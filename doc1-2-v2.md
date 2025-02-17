## **First `sudo`**

### **What is `sudo`?**
- **`sudo` (Superuser Do)** allows a user to execute commands as another user, typically as the **root (administrator) user**.
- It is used to **elevate privileges** for tasks that require administrative access, such as installing software, modifying system files, or changing configurations.

### **Why is `sudo` important?**
- Unlike **Windows administrator accounts**, Linux operates under the **principle of least privilege**—regular users do not have unrestricted access to system-critical files.
- **Using `sudo` instead of logging in as root** prevents accidental system-wide damage and improves security.

### **Basic Usage of `sudo`**
```sh
sudo command
```
- Example: Update package lists
  ```sh
  sudo apt update
  ```
- Example: Restart a service
  ```sh
  sudo systemctl restart apache2
  ```

### **Checking and Managing `sudo` Permissions**
- **List who has `sudo` access**:
  ```sh
  getent group sudo  # On Ubuntu/Debian-based systems
  getent group wheel  # On RHEL/CentOS-based systems
  ```
- **Add a user to the `sudo` group** (Requires root access):
  ```sh
  sudo usermod -aG sudo username  # Ubuntu/Debian
  sudo usermod -aG wheel username  # RHEL/CentOS
  ```
- **Check which commands a user can run with `sudo`**:
  ```sh
  sudo -l
  ```

### **Best Practices for Using `sudo` Securely**
- **Do not use `sudo` for every command unnecessarily.**
- **Never execute untrusted scripts with `sudo`.**
- **Use `sudo -i` or `sudo su` carefully**, as it provides a root shell, which can be risky.
- **Monitor sudo usage** with logs:
  ```sh
  sudo cat /var/log/auth.log | grep sudo  # Debian/Ubuntu
  sudo cat /var/log/secure | grep sudo  # RHEL/CentOS
  ```



---




## **1. Terminal**
- **What is a terminal?**
  - A command-line interface (CLI) used to interact with Linux.
  - More powerful and efficient than a graphical interface for many tasks.
- **How to open the terminal?**
  - **Ubuntu/Linux Mint:** `Ctrl + Alt + T`
  - **CentOS/RHEL:** Applications > Terminal
  - **Arch-based distros:** Open via menu or shortcut

---

## **2. Basic Commands for Navigation**
- **`pwd`** – Show current directory path  
  ```sh
  pwd
  ```
- **`ls`** – List files and directories  
  ```sh
  ls -lA   # Detailed list including hidden files with permissions, size, owner, etc.
  ```
- **`cd`** – Change directory  
  ```sh
  cd /home/user/Documents  # Move to a specific directory
  cd ..                    # Move up one level
  cd ~                     # Move to home directory
  ```
- **`tree`** – Display directory structure (requires installation)  
  ```sh
  tree
  ```

---

## **3. File and Directory Operations**
- **`touch`** – Create an empty file  
  ```sh
  touch newfile.txt
  ```
- **`mkdir`** – Create a new directory  
  ```sh
  mkdir secure_dir
  ```
- **`rm`** – Delete files and directories  
  ```sh
  rm -rf temp_data  # Securely delete files and directories
  ```
- **`chmod`** – Change file permissions  
  ```sh
  chmod 700 sensitive.txt  # Restrict access to owner only
  ```
- **`chown`** – Change file ownership  
  ```sh
  sudo chown user:group file.txt  # Change owner and group
  ```

---

## **4. System Security & Monitoring Commands**
- **Checking Active Users**  
  ```sh
  who  # Shows logged-in users
  ```
- **Process Monitoring**  
  ```sh
  ps aux | grep suspicious  # Check for unknown running processes
  ```
- **Network Monitoring**  
  ```sh
  netstat -tulnp  # View open ports and active connections
  ```
- **File Integrity Checking**  
  ```sh
  sha256sum important_file.txt  # Verify file integrity
  ```
- **System Logs**  
  ```sh
  journalctl -xe  # View system logs for debugging security issues
  ```

---

## **5. Working with Text Files**
- **`nano`** – Simple text editor  
  ```sh
  nano file.txt  # Open file in nano editor (Ctrl + X to exit)
  ```
- **`vim`** – Advanced text editor  
  ```sh
  vim file.txt  # Open file in Vim (Press "i" to insert, ESC to exit, ":wq" to save)
  ```
- **`echo`** – Print text to the terminal or file  
  ```sh
  echo "Hello, Linux!"  # Print text
  echo "Hello, Linux!" > file.txt  # Save text to file
  ```

---

## **6. File and Directory Permissions**
- **`ls -l`** – Show file permissions  
  ```sh
  ls -l file.txt
  ```
- **`chmod`** – Change file permissions  
  ```sh
  chmod 644 file.txt  # Set read/write for owner, read-only for others
  chmod +x script.sh  # Make script executable
  ```
- **`chown`** – Change file ownership  
  ```sh
  sudo chown user:group file.txt  # Change owner and group
  ```
- **`setfacl`** – Assign fine-grained permissions to files  
  ```sh
  setfacl -m u:username:rwx file.txt  # Give user full access
  ```

---

## **7. System Information and Process Management**
- **`uname -a`** – Show detailed system info  
  ```sh
  uname -a
  ```
- **`whoami`** – Display current user  
  ```sh
  whoami
  ```
- **`ps`** – List running processes  
  ```sh
  ps aux  # Detailed process list
  ```
- **`top` / `htop`** – Monitor system processes  
  ```sh
  top  # Live process monitoring (press "q" to exit)
  htop  # More interactive (requires installation)
  ```

---

## **8. Searching and Finding Files**
- **`find`** – Search for files and directories  
  ```sh
  find /home -name "*.txt"  # Find all .txt files in home directory
  find /var/log -type f -mtime -7  # Find files modified in the last 7 days
  find / -type d -name "Documents"  # Find directories named "Documents"
  find /home -user username  # Find files owned by a specific user
  ```
- **`locate`** – Search for files and directories with locate (needs update database) 
  ```sh
  sudo updatedb  # Update file database
  locate file.txt  # Find file using locate
  ```
- **`grep`** – Search inside files  
  ```sh
  grep "error" logfile.txt  # Find "error" in logfile.txt
  ```
- **`auditctl`** – Monitor system events and file access  
  ```sh
  sudo auditctl -w /etc/passwd -p wa -k passwd_changes  # Track changes to /etc/passwd
  ```
- **`which`** – Find location of a command  
  ```sh
  which python  # Show where Python is installed
  ```

This enhanced version keeps your original content while adding **cybersecurity-focused commands**, **file integrity verification**, and **system monitoring tools** to provide hands-on security awareness. Let me know if you need any refinements! 🚀

