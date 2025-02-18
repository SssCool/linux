# User and Group Management in Linux

## Introduction
In Linux, users and groups are essential for managing access to files, directories, and system resources. Each user has a unique identifier (UID) and belongs to one or more groups, each with a group identifier (GID). Proper user and group management ensures system security and controlled access.

---

## 1. User Management

### 1.1 User Accounts
- **Root User**: The superuser with full system access (UID 0). This user has unrestricted permissions and should be used with caution.
- **Regular Users**: Standard users with limited permissions (UID starting from 1000). These users can perform everyday tasks without compromising system security.

### 1.2 Key Files
- **`/etc/passwd`**: Stores user account information (username, UID, GID, home directory, shell). Each line in this file represents a user account.
- **`/etc/shadow`**: Stores encrypted passwords and password-related settings. Only accessible by the root user for security reasons.
- **`/etc/group`**: Stores group information (group name, GID, members). Helps manage group memberships and permissions efficiently.

### 1.3 Commands for User Management
- **`useradd <username>`**: Create a new user with default settings.
- **`usermod -aG <group> <username>`**: Add an existing user to a group.
- **`userdel -r <username>`**: Delete a user and remove their home directory.
- **`passwd <username>`**: Set or change a user's password.
- **`id <username>`**: Display UID, GID, and group memberships of a user.
- **`who`**: Display currently logged-in users.
- **`whoami`**: Show the current logged-in user.
- **`last`**: Show the login history of users.

---

## 2. Group Management

### 2.1 Groups
- **Primary Group**: Each user has one primary group, which is assigned when the user is created. This is usually the same as the username.
- **Secondary Groups**: Users can belong to multiple secondary groups, which provide additional permissions and access rights.

### 2.2 Commands for Group Management
- **`groupadd <groupname>`**: Create a new group.
- **`groupmod -n <newgroupname> <oldgroupname>`**: Rename an existing group.
- **`groupdel <groupname>`**: Delete a group.
- **`gpasswd -a <username> <groupname>`**: Add a user to a group.
- **`gpasswd -d <username> <groupname>`**: Remove a user from a group.
- **`groups <username>`**: List all groups a user belongs to.

---

## 3. File Permissions and Ownership

### 3.1 Ownership
- **`chown <user>:<group> <file>`**: Change the ownership of a file.
- **`chgrp <group> <file>`**: Change the group ownership of a file.
- **`ls -l`**: Display file ownership and permissions.

### 3.2 Permissions
Linux file permissions follow the **rwx (Read, Write, Execute)** model and are categorized into three types:
- **User (`u`)**: The file owner’s permissions.
- **Group (`g`)**: Permissions for users in the file’s group.
- **Others (`o`)**: Permissions for all other users.

#### Changing Permissions
- **`chmod u+x <file>`**: Grant execute permission to the owner.
- **`chmod g-w <file>`**: Remove write permission from the group.
- **`chmod 755 <file>`**: Assign permissions using numeric notation (owner: rwx, group: r-x, others: r-x).

---

## 4. Switching Users

### 4.1 `su` Command
- **`su <username>`**: Switch to another user account.
- **`su -`**: Switch to root user and load their environment.
- **`exit`**: Return to the previous user.

### 4.2 `sudo` Command
- **`sudo <command>`**: Execute a command as another user (usually root).
- **`sudo -i`**: Open a root shell.
- **`sudo visudo`**: Edit the `/etc/sudoers` file to configure sudo access.

---

## 5. Advanced User and Group Management

### 5.1 Managing Expiration and Account Locking
- **`chage -l <username>`**: View password expiration details.
- **`chage -M 90 <username>`**: Set password expiration to 90 days.
- **`usermod -L <username>`**: Lock a user account.
- **`usermod -U <username>`**: Unlock a user account.

### 5.2 Monitoring User Activity
- **`w`**: Show who is logged in and their activity.
- **`lastlog`**: Display the last login time of all users.
- **`faillog -a`**: Show failed login attempts.

----

## BONUS : Understanding Numeric File Permissions
Each permission in Linux is assigned a number:

| Permission Type | Symbol | Numeric Value |
|---------------|--------|--------------|
| Read (`r`)    | `4`    | `4`          |
| Write (`w`)   | `2`    | `2`          |
| Execute (`x`) | `1`    | `1`          |

Each file has three permission categories:
1. **Owner (User)**
2. **Group**
3. **Others (World)**

A three-digit number is used to define permissions for each of these categories. The numbers are calculated by adding up the values for read, write, and execute permissions.

---

## Common Permission Examples

### **644 (rw-r--r--)**
- **Owner:** Read (`4`) + Write (`2`) = **6** (**rw-**)
- **Group:** Read (`4`) = **4** (**r--**)
- **Others:** Read (`4`) = **4** (**r--**)
- **Usage:** Default permission for text files; only the owner can modify the file, while others can only read.

### **755 (rwxr-xr-x)**
- **Owner:** Read (`4`) + Write (`2`) + Execute (`1`) = **7** (**rwx**)
- **Group:** Read (`4`) + Execute (`1`) = **5** (**r-x**)
- **Others:** Read (`4`) + Execute (`1`) = **5** (**r-x**)
- **Usage:** Common for executable files and directories; allows others to execute but not modify.

### **777 (rwxrwxrwx)**
- **Owner:** Read (`4`) + Write (`2`) + Execute (`1`) = **7** (**rwx**)
- **Group:** Read (`4`) + Write (`2`) + Execute (`1`) = **7** (**rwx**)
- **Others:** Read (`4`) + Write (`2`) + Execute (`1`) = **7** (**rwx**)
- **Usage:** Full access to everyone (unsafe!); typically used for temporary permission changes.

### **700 (rwx------)**
- **Owner:** Read (`4`) + Write (`2`) + Execute (`1`) = **7** (**rwx**)
- **Group:** No permission = **0** (**---**)
- **Others:** No permission = **0** (**---**)
- **Usage:** Used for private files or scripts where only the owner has full access.


