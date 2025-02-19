## **1. Introduction to Networking**
Networking in Ubuntu is a crucial aspect of system administration. Whether configuring a server, setting up a local network, or troubleshooting connectivity issues, understanding Ubuntu's networking stack is essential.

### **Key Components**
- **Network Interfaces**: Physical (e.g., Ethernet, Wi-Fi) and virtual (e.g., bridges, tunnels) network interfaces.
- **Netplan**: The default network configuration utility for Ubuntu.
- **NetworkManager**: A utility for easily managing network connections (mostly for desktops and laptops).
- **Systemd-networkd**: A network service manager optimized for servers.
- **Diagnostic Tools**: Commands such as `ip`, `nmcli`, `ifconfig`, `ping`, `netstat`, and `traceroute`.
- **Firewall & Security**: Managed via `ufw`, `iptables`, and `firewalld`.

---

## **2. Understanding Netplan**

### **What is Netplan?**
Netplan is a network configuration utility introduced in Ubuntu 17.10. It uses YAML configuration files to define network settings, making it easy to configure complex networking setups.

### **Netplan Renderers**
Netplan can use different **backends** (renderers) to apply configurations:
- **NetworkManager**: Used in **desktop/laptop** environments where dynamic configuration and easy management via GUI are preferred.
- **systemd-networkd**: Used in **server environments** where lightweight, persistent networking is required.

### **Checking Available Renderers**
```bash
networkctl status
```

---

## **3. Viewing Network Configuration**

### **Checking Current Network Interfaces**
```bash
ip a
```
Lists all network interfaces and their assigned IP addresses.

Alternative command:
```bash
ifconfig  # Older method, requires `net-tools` package
```

### **Displaying the Routing Table**
```bash
ip route show
```
Shows the system’s current routing table, which determines how packets are forwarded.

### **Showing DNS Configuration**
```bash
cat /etc/resolv.conf
```
Lists the nameservers used for DNS resolution.

---

## **4. Configuring Network Interfaces with Netplan**

### **Use Case: Setting a Static IP Address**
Modify the Netplan configuration file (usually `/etc/netplan/01-netcfg.yaml`):

```yaml
network:
  version: 2
  renderer: networkd  # Use NetworkManager for desktops
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4
```
Apply changes:
```bash
sudo netplan apply
```

### **Use Case: Configuring a DHCP Client**
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: true
```
Apply changes:
```bash
sudo netplan apply
```

### **Use Case: Setting Up a Bridge Interface**
```yaml
network:
  version: 2
  renderer: networkd
  bridges:
    br0:
      interfaces: [eth0]
      addresses: [192.168.1.200/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```
Apply changes:
```bash
sudo netplan apply
```

---

## **5. Managing Network Connections**

### **Using NetworkManager (`nmcli`)**
**List Active Connections**
```bash
nmcli con show
```

**Connect to a Wi-Fi Network**
```bash
nmcli dev wifi connect "SSID" password "yourpassword"
```

**Configure a Static IP Using nmcli**
```bash
nmcli con mod "Wired connection 1" ipv4.method manual ipv4.addresses 192.168.1.150/24 ipv4.gateway 192.168.1.1 ipv4.dns "8.8.8.8 8.8.4.4"
nmcli con up "Wired connection 1"
```

---

## **6. Testing Network Connectivity**

### **Ping a Host**
```bash
ping -c 5 google.com
```
Tests connectivity to a remote host.

### **Trace Network Route**
```bash
traceroute google.com
```
Shows the path packets take to reach their destination.

### **Check Open Ports**
```bash
netstat -tulnp
```
Lists active network connections and listening ports.

---

## **7. Managing the Firewall (UFW)**

### **Enable Firewall**
```bash
sudo ufw enable
```

### **Allow SSH and HTTP Traffic**
```bash
sudo ufw allow ssh
sudo ufw allow http
```

### **View Firewall Status**
```bash
sudo ufw status verbose
```

---

## **8. Network Troubleshooting**

### **Restart Network Services**
```bash
sudo systemctl restart NetworkManager
```

### **Check Network Logs**
```bash
journalctl -u NetworkManager --no-pager
```

### **Identify Listening Ports**
```bash
ss -tulnp
```

---

## **9. Advanced Network Configurations**

### **Setting Up a Static Route**
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      routes:
        - to: 10.10.10.0/24
          via: 192.168.1.1
```
Apply changes:
```bash
sudo netplan apply
```

### **Setting Up a VPN Connection**
For OpenVPN:
```bash
sudo apt install openvpn
sudo openvpn --config myvpn.conf
```

