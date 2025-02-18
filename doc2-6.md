# SSH Tutorial with Examples and Exercises

## **1. Getting Started with SSH**
### **1.1 Connecting to a Remote Server**
#### **Command:**
```sh
ssh user@remote_server_ip
```
#### **Explanation:**
- `user` is the username on the remote server.
- `remote_server_ip` is the IP address or hostname of the remote server.
- The default SSH port is `22`.

#### **Exercise:**
- Try connecting to a remote machine using SSH.
- If you don’t have a remote machine, set up an SSH server on a virtual machine and connect to it.

---

## **2. Using SSH Keys for Authentication**
### **2.1 Generating SSH Keys**
#### **Command:**
```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
#### **Explanation:**
- This generates a pair of RSA keys (`id_rsa` and `id_rsa.pub`).
- The private key is kept secret, while the public key is shared.

### **2.2 Copying SSH Public Key to Server**
#### **Command:**
```sh
ssh-copy-id user@remote_server_ip
```
#### **Explanation:**
- This command copies the public key to the remote server for password-less authentication.

### **"Key SSH Configuration Tips"** (Between Password and Key Authentication)
To ensure secure SSH access, configure the SSH server (`/etc/ssh/sshd_config`) with the following:

- **"Disable Password Authentication (If Using Key-Based Authentication)"**
  ```sh
  PasswordAuthentication no
  ```
- **"Allow Only Specific Users to Connect"**
  ```sh
  AllowUsers your_user another_user
  ```
- **"Disable Root Login"**
  ```sh
  PermitRootLogin no
  ```
- **"Use a Custom SSH Port (To Avoid Scans and Attacks)"**
  ```sh
  Port 2222
  ```
- **"Limit Failed Login Attempts"**
  ```sh
  MaxAuthTries 3
  ```
- **"Enable Public Key Authentication"**
  ```sh
  PubkeyAuthentication yes
  ```
- **"Restrict SSH Access to Specific IPs"** (If needed)
  ```sh
  AllowUsers your_user@192.168.1.*
  ```
  
After applying these configurations, restart the SSH service:
```sh
sudo systemctl restart sshd
```

#### **Exercise:**
- Modify your SSH server configuration to enhance security.
- Disable password authentication and only allow key-based authentication.
- Restrict SSH access to specific users and IPs.

---

## **3. Transferring Files Securely with SCP**
### **3.1 Copying Files to a Remote Server**
#### **Command:**
```sh
scp localfile.txt user@remote_server_ip:/remote/path/
```
#### **Explanation:**
- Securely copies `localfile.txt` to the remote server’s `/remote/path/` directory.

### **3.2 Copying Files from a Remote Server**
#### **Command:**
```sh
scp user@remote_server_ip:/remote/path/remote_file.txt local_folder/
```
#### **Explanation:**
- Copies `remote_file.txt` from the remote server to a local directory.

#### **Exercise:**
- Copy a file to and from a remote server using `scp`.

---

## **4. Syncing Files with Rsync**
### **4.1 Syncing Files Efficiently**
#### **Command:**
```sh
rsync -avz local_folder/ user@remote_server_ip:/remote/path/
```
#### **Explanation:**
- Syncs `local_folder/` to the remote server while preserving attributes (`-a`) and compressing data (`-z`).

#### **Exercise:**
- Sync a local directory with a remote server using `rsync`.

---

## **5. SSH Tunneling and Port Forwarding**
### **5.1 Local Port Forwarding**
#### **Command:**
```sh
ssh -L 8080:localhost:3306 user@remote_server_ip
```
#### **Explanation:**
- Forwards local port `8080` to `localhost:3306` on the remote server.

### **5.2 Remote Port Forwarding**
#### **Command:**
```sh
ssh -R 9000:localhost:5000 user@remote_server_ip
```
#### **Explanation:**
- Exposes `localhost:5000` to the remote machine’s port `9000`.

#### **Exercise:**
- Use SSH tunneling to access a database securely.
- Forward a local web server to a remote machine.

---

## **6. Advanced SSH Configuration**
### **6.1 Configuring SSH Client Settings**
#### **File:** `~/.ssh/config`
#### **Configuration:**
```sh
Host myserver
    HostName remote_server_ip
    User user
    IdentityFile ~/.ssh/id_rsa
```
#### **Explanation:**
- Simplifies SSH connections so you can connect using `ssh myserver` instead of `ssh user@remote_server_ip`.

#### **Exercise:**
- Set up an SSH config file for easier remote access.

---

## **7. Using SSH with Git**
### **7.1 Authenticating Git with SSH**
#### **Command:**
```sh
git clone git@github.com:your_username/repository.git
```
#### **Explanation:**
- Uses SSH authentication instead of HTTPS.

#### **Exercise:**
- Configure SSH authentication for GitHub and clone a repository.

---

## **8. Final Challenge**
### **Scenario:**
You are given a remote server and need to:
1. Set up SSH key-based authentication.
2. Transfer files using `scp`.
3. Set up an SSH tunnel to forward a database connection.
4. Harden SSH security by disabling root login and changing the port.

#### **Tasks:**
- Implement all the above steps and verify secure connections.

