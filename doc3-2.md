## **1. Updating and Upgrading Packages**

### **Example: Update and Upgrade the System**
Updating the package list ensures that you get the latest versions, and upgrading applies those updates.

```bash
# Update package list
sudo apt update

# Upgrade all installed packages
sudo apt upgrade -y
```

### **Exercise 1**
1. Update your package list.
2. Upgrade all installed packages.
3. Check which packages were upgraded using:
   ```bash
   cat /var/log/apt/history.log | grep 'upgrade'
   ```

---

## **2. Installing Packages with dpkg**

### **Example: Install a .deb Package Using dpkg**
`dpkg` is used to manually install `.deb` files.

```bash
# Download a package (e.g., Google Chrome)
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb

# Install the downloaded package
sudo dpkg -i google-chrome-stable_current_amd64.deb

# Fix missing dependencies if any
sudo apt install -f
```

### **Exercise 2**
1. Download and install a `.deb` package of your choice (e.g., **VLC** from the official site).
2. If there are missing dependencies, resolve them using:
   ```bash
   sudo apt install -f
   ```
3. Verify the installation using:
   ```bash
   dpkg -l | grep package-name
   ```

---

## **3. Security Updates**

### **Example: Install Security Updates**
Security updates keep your system protected.

```bash
# Check available security updates
sudo unattended-upgrade --dry-run

# Apply security updates
sudo apt install unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades
```

### **Exercise 3**
1. Check if **unattended-upgrades** is installed.
2. Enable automatic security updates.
3. Run a dry-run security update check.
4. Install any pending security updates manually.

---

## **4. Adding Repositories**

### **Example: Add a PPA Repository**
Adding a **PPA (Personal Package Archive)** allows you to install software not available in official repositories.

```bash
# Add a PPA repository (e.g., for LibreOffice)
sudo add-apt-repository ppa:libreoffice/ppa

# Update package list
sudo apt update
```

### **Example: Add a Repository Manually (sources.list)**
Instead of a PPA, you can manually add a repository to your sources list.

```bash
# Add repository key (example for Google Chrome)
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo gpg --dearmor -o /usr/share/keyrings/google-keyring.gpg

# Add repository to sources.list.d
echo "deb [signed-by=/usr/share/keyrings/google-keyring.gpg] http://dl.google.com/linux/chrome/deb/ stable main" | sudo tee /etc/apt/sources.list.d/google-chrome.list

# Update package list
sudo apt update
```

### **Exercise 4**
1. Add the **PPA repository** for **Mozilla Firefox**.
2. Install Firefox from the new repository.
3. Manually add the **Google Chrome** repository using sources.list.
4. Install **Google Chrome** from the newly added repository.

---

## **5. Holding Packages**

### **Example: Prevent a Package from Being Upgraded**
Holding a package prevents it from being updated.

```bash
# Hold a package (e.g., VLC)
sudo apt-mark hold vlc

# Check held packages
apt-mark showhold
```

### **Exercise 5**
1. Install the **vlc** package if it's not already installed.
2. Hold the package to prevent it from being updated.
3. Verify that the package is held.
4. Unhold the package to allow updates:
   ```bash
   sudo apt-mark unhold vlc
   ```

---

## **6. Upgrading a Specific Package**

### **Example: Upgrade Only One Package**
If you only want to upgrade one package and not the entire system, use:

```bash
# Upgrade a specific package (e.g., Firefox)
sudo apt install --only-upgrade firefox
```

### **Exercise 6**
1. Check if **curl** is installed on your system.
2. If installed, upgrade it to the latest version.
3. Verify the upgraded version using:
   ```bash
   curl --version
   ```

---

## **7. Installing a Specific Package Version**

### **Example: Install a Specific Version of a Package**
If you need a specific version of a package, list available versions and install one.

```bash
# List available versions
apt-cache madison firefox

# Install a specific version
sudo apt install firefox=100.0+build1-0ubuntu0.22.04.1
```

### **Exercise 7**
1. List available versions of **vim**.
2. Install an older version (if available).
3. Verify the installed version using:
   ```bash
   vim --version
   ```

