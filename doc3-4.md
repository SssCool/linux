## **1. Basic Network Configuration Exercises**

### **Exercise 1: Check Network Interfaces**
1. **List all active network interfaces and their assigned IP addresses:**
   ```bash
   ip a
   ```
   - `ip` → The primary command for managing networking.
   - `a` (short for `addr`) → Shows assigned IP addresses and network interface details.

2. **Verify the MAC address of your network adapter:**
   ```bash
   ip link show
   ```
   - `ip link` → Displays the link-layer information of interfaces.
   - `show` → Lists all network interfaces and their MAC addresses.

3. **Check the default gateway of your system:**
   ```bash
   ip route show
   ```
   - `ip route` → Displays the system’s routing table.
   - `show` → Lists the default gateway and other routes.

---

## **2. Network Configuration with Netplan**

### **Exercise 2: Configure a Static IP Address**
1. Edit the Netplan configuration file (usually `/etc/netplan/01-netcfg.yaml`).
2. Set a static IP of `192.168.1.100/24` with a gateway of `192.168.1.1`.
3. Apply the configuration.
   ```bash
   sudo netplan apply
   ```
   - `sudo` → Runs the command with superuser privileges.
   - `netplan apply` → Applies changes made in Netplan YAML configuration files.

4. Verify the changes using:
   ```bash
   ip a
   ```

### **Exercise 3: Switch to DHCP**
1. Modify the Netplan file to use DHCP instead of a static IP.
2. Apply the changes.
3. Verify that your system has received an IP from the DHCP server.
   ```bash
   ip a
   ```

---

## **3. Managing Network Connections with NetworkManager**

### **Exercise 4: Connect to a Wi-Fi Network**
1. **List available Wi-Fi networks:**
   ```bash
   nmcli dev wifi list
   ```
   - `nmcli` → Command-line interface for NetworkManager.
   - `dev wifi list` → Lists available Wi-Fi networks.

2. **Connect to a Wi-Fi network named `MyNetwork` with password `MyPassword`:**
   ```bash
   nmcli dev wifi connect "MyNetwork" password "MyPassword"
   ```
   - `dev wifi connect` → Initiates a Wi-Fi connection.
   - `"MyNetwork"` → Name (SSID) of the Wi-Fi network.
   - `password "MyPassword"` → Wi-Fi password.

3. **Verify the connection status:**
   ```bash
   nmcli con show
   ```
   - `con show` → Lists active connections.

---

## **4. Network Troubleshooting Exercises**

### **Exercise 6: Test Network Connectivity**
1. **Ping a remote host (`google.com`) to check connectivity:**
   ```bash
   ping -c 5 google.com
   ```
   - `ping` → Sends packets to test network reachability.
   - `-c 5` → Sends 5 packets before stopping.

2. **Use traceroute to identify the path packets take to `google.com`:**
   ```bash
   traceroute google.com
   ```
   - `traceroute` → Displays the path packets take to a destination.

3. **Check the name resolution settings:**
   ```bash
   cat /etc/resolv.conf
   ```
   - `cat` → Displays the contents of a file.
   - `/etc/resolv.conf` → Contains the system's DNS settings.

### **Exercise 7: Identify Network Issues**
1. **List all active TCP and UDP connections:**
   ```bash
   netstat -tulnp
   ```
   - `netstat` → Displays network statistics.
   - `-t` → Show TCP connections.
   - `-u` → Show UDP connections.
   - `-l` → Show listening ports.
   - `-n` → Show numerical addresses instead of hostnames.
   - `-p` → Show process ID (PID) using the connection.

2. **Display active network connections and their process IDs:**
   ```bash
   ss -tulnp
   ```
   - `ss` → Newer alternative to `netstat`.
   - `-tulnp` → Displays listening TCP and UDP ports with process IDs.

3. **Restart the network service:**
   ```bash
   sudo systemctl restart NetworkManager
   ```
   - `systemctl restart` → Restarts a service.
   - `NetworkManager` → The networking service managing connections.

---

## **5. Firewall and Security Exercises**

### **Exercise 8: Manage UFW Firewall Rules**
1. **Enable the firewall:**
   ```bash
   sudo ufw enable
   ```
   - `ufw enable` → Activates the Uncomplicated Firewall (UFW).

2. **Allow SSH and HTTP traffic:**
   ```bash
   sudo ufw allow ssh
   sudo ufw allow http
   ```
   - `ufw allow` → Allows traffic on a specified port/service.
   - `ssh` → Allows SSH connections.
   - `http` → Allows web server traffic.

3. **Check the firewall status:**
   ```bash
   sudo ufw status verbose
   ```
   - `ufw status verbose` → Shows detailed firewall rule status.

---

## **6. Advanced Network Configuration**

### **Exercise 9: Set Up a Static Route**
1. **Add a static route for the `10.10.10.0/24` network through `192.168.1.1`**
   ```bash
   sudo ip route add 10.10.10.0/24 via 192.168.1.1
   ```
   - `ip route add` → Adds a new route.
   - `10.10.10.0/24` → Destination subnet.
   - `via 192.168.1.1` → Specifies the next-hop gateway.

2. **Verify the routing table:**
   ```bash
   ip route show
   ```
