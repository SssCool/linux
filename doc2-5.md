# Secure Shell (SSH)

## Introduction
Secure Shell (SSH) is a cryptographic network protocol that enables secure communication over an unsecured network. It is widely used for remote command-line login, file transfers, and secure remote system management.

---

## Why Use SSH?
SSH provides:
- **Confidentiality**: Encrypts all data transmitted between client and server.
- **Integrity**: Ensures data is not altered during transmission.
- **Authentication**: Verifies identity through passwords or key-based methods.

---

## SSH Components
SSH consists of three main components:
1. **SSH Client**: The program initiating the connection.
2. **SSH Server**: The program receiving and handling the connection.
3. **SSH Protocol**: The rules governing secure communication.

---

## How SSH Works
### 1. Establishing a Connection
- The client requests a connection to the SSH server.
- The server provides a public key to initiate encryption.
- The client verifies the server identity.
- A secure, encrypted session is established.

### 2. Authentication Methods
- **Password-Based Authentication**: The user provides a username and password.
- **Public-Key Authentication**: Uses a cryptographic key pair (private and public keys).

---

## Generating SSH Keys
To use key-based authentication, generate an SSH key pair:
```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
- `-t rsa` specifies the RSA algorithm.
- `-b 4096` sets the key size to 4096 bits.
- `-C` adds a comment (usually an email address).

The command generates:
- **Private Key (`id_rsa`)**: Kept secret by the user.
- **Public Key (`id_rsa.pub`)**: Shared with remote servers.

To copy the public key to a server:
```sh
ssh-copy-id user@server_ip
```

---

## Common SSH Commands
| Command | Description |
|---------|-------------|
| `ssh user@server` | Connects to a remote server |
| `ssh -i keyfile user@server` | Connects using a specific key file |
| `scp file user@server:/path` | Securely copies a file to a server |
| `rsync -avz file user@server:/path` | Efficient file transfer |
| `ssh -L local_port:remote_host:remote_port user@server` | Port forwarding |

---

## SSH Configuration
The SSH configuration file is located at:
- **Client Config**: `~/.ssh/config`
- **Server Config**: `/etc/ssh/sshd_config`

Example client configuration (`~/.ssh/config`):
```sh
Host myserver
    HostName server_ip
    User username
    IdentityFile ~/.ssh/id_rsa
```
This allows you to connect using `ssh myserver` instead of `ssh user@server_ip`.

---

## Hardening SSH Security
### 1. Disable Root Login
Edit `/etc/ssh/sshd_config`:
```sh
PermitRootLogin no
```
Restart SSH service:
```sh
sudo systemctl restart sshd
```

### 2. Change Default SSH Port
Edit `/etc/ssh/sshd_config`:
```sh
Port 2222
```
Restart SSH service:
```sh
sudo systemctl restart sshd
```

### 3. Use Only Key-Based Authentication
Disable password authentication:
```sh
PasswordAuthentication no
```

---

# BONUS - SSH Tunneling
SSH tunneling is a technique used to securely forward network traffic between local and remote systems. It is useful in situations where direct network access is restricted or needs to be encrypted. SSH tunneling enables a secure pathway through an otherwise untrusted network.

Example of local port forwarding:
```sh
ssh -L 8080:localhost:80 user@server
```
This forwards local port `8080` to the remote machine's port `80`.




## Types of SSH Tunneling
1. **Local Port Forwarding** (Forward local traffic to a remote machine)
2. **Remote Port Forwarding** (Expose a local service on a remote machine)
3. **Dynamic Port Forwarding** (Use SSH as a SOCKS proxy)

---

## Local Port Forwarding (Local-to-Remote)
**Definition:** Local port forwarding allows forwarding a local machine's port to a specific port on a remote machine through an SSH tunnel.

**Syntax:**
```sh
ssh -L [LOCAL_PORT]:[DESTINATION_HOST]:[DESTINATION_PORT] user@remote_server
```

### Example Use Cases:
1. **Access a Database Securely**  
   Suppose a MySQL database is running on a remote server, but it is only accessible from `localhost` on that server. You can create an SSH tunnel to access it securely from your local machine.
   ```sh
   ssh -L 3306:localhost:3306 user@remote_server
   ```
   Now, you can connect to the remote database using:
   ```sh
   mysql -h 127.0.0.1 -P 3306 -u user -p
   ```

2. **Access Web Applications Behind a Firewall**  
   Suppose a web server is running on `remote_server` at port `8000`, but it is not publicly accessible. You can create a tunnel:
   ```sh
   ssh -L 8080:localhost:8000 user@remote_server
   ```
   Now, visiting `http://localhost:8080` on your browser will load the web application running on `remote_server:8000`.

---

## Remote Port Forwarding (Remote-to-Local)
**Definition:** Remote port forwarding allows exposing a local service running on your machine to a remote server.

**Syntax:**
```sh
ssh -R [REMOTE_PORT]:[LOCAL_HOST]:[LOCAL_PORT] user@remote_server
```

### Example Use Cases:
1. **Access a Local Development Server Remotely**  
   If you are running a development web server on your local machine at port `5000` and want to make it accessible on a remote server, you can use:
   ```sh
   ssh -R 9000:localhost:5000 user@remote_server
   ```
   Now, the remote server can access your local web server using:
   ```
   http://localhost:9000
   ```

2. **Provide Remote Access to an Internal Service**  
   If an internal application is running on your laptop (e.g., a Jupyter Notebook), you can allow a remote colleague to access it:
   ```sh
   ssh -R 8888:localhost:8888 user@remote_server
   ```
   Now, anyone logged into `remote_server` can access your Jupyter Notebook.

---

## Dynamic Port Forwarding (SOCKS Proxy)
**Definition:** Dynamic port forwarding allows SSH to act as a proxy, enabling access to the internet through an encrypted tunnel.

**Syntax:**
```sh
ssh -D [LOCAL_PORT] user@remote_server
```

### Example Use Cases:
1. **Bypass Firewall Restrictions**  
   If you're on a restricted network that blocks certain websites, you can use an SSH SOCKS proxy to bypass the restrictions:
   ```sh
   ssh -D 8080 user@remote_server
   ```
   Then, configure your web browser to use `localhost:8080` as a SOCKS5 proxy.

2. **Securely Browse the Internet Over Public Wi-Fi**  
   If you’re using public Wi-Fi and don’t trust the network, use an SSH SOCKS proxy to encrypt and route your traffic through a remote trusted server.

