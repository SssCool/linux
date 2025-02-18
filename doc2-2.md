
## 1. User Management

### Example 1: Create a New User
```bash
useradd -m -s /bin/bash john
```
**Breakdown:**
- `useradd`: Command to create a new user.
- `-m`: Ensures a home directory is created for the user.
- `-s /bin/bash`: Specifies the default shell for the user.
- `john`: The name of the new user.

**Exercise:**
- Create a new user named `alice` with a home directory and default shell set to `/bin/bash`.

---

### Example 2: Set a User Password
```bash
passwd john
```
**Breakdown:**
- `passwd`: The command to manage user passwords.
- `john`: The user whose password is being set.

**Exercise:**
- Set a password for the user `alice`.

---

### Example 3: Modify a User
```bash
usermod -aG sudo john
```
**Breakdown:**
- `usermod`: The command to modify user properties.
- `-aG`: Adds the user to a supplementary group without removing them from other groups.
- `sudo`: The group to which the user is added.
- `john`: The user being modified.

**Exercise:**
- Add the user `alice` to the `sudo` group.

---

### Example 4: Delete a User
```bash
userdel -r john
```
**Breakdown:**
- `userdel`: The command to delete a user.
- `-r`: Removes the user's home directory and mail spool.
- `john`: The user to be deleted.

**Exercise:**
- Delete the user `alice` and their home directory.

---

## 2. Group Management

### Example 1: Create a New Group
```bash
groupadd developers
```
**Breakdown:**
- `groupadd`: The command to create a new group.
- `developers`: The name of the new group.

**Exercise:**
- Create a new group named `admins`.

---

### Example 2: Add a User to a Group
```bash
usermod -aG developers john
```
**Breakdown:**
- `usermod`: The command to modify user properties.
- `-aG`: Adds the user to a supplementary group.
- `developers`: The group to which the user is added.
- `john`: The user being modified.

**Exercise:**
- Add the user `alice` to the `admins` group.

---

### Example 3: Delete a Group
```bash
groupdel developers
```
**Breakdown:**
- `groupdel`: The command to delete a group.
- `developers`: The group to be deleted.

**Exercise:**
- Delete the group `admins`.

---

## 3. File Ownership and Permissions

### Example 1: Change File Ownership
```bash
chown john:developers file.txt
```
**Breakdown:**
- `chown`: The command to change file ownership.
- `john:developers`: Sets the owner to `john` and the group to `developers`.
- `file.txt`: The file whose ownership is being changed.

**Exercise:**
- Change the ownership of a file named `report.txt` to `alice:admins`.

---

### Example 2: Change File Permissions
```bash
chmod 755 script.sh
```
**Breakdown:**
- `chmod`: The command to change file permissions.
- `755`: Numeric representation of permissions:
  - `7` (owner): rwx (read, write, execute).
  - `5` (group): r-x (read, execute).
  - `5` (others): r-x (read, execute).
- `script.sh`: The file whose permissions are being changed.

**Exercise:**
- Change the permissions of a file named `backup.sh` to `644`.

---

## 4. Switching Users

### Example 1: Switch to Another User
```bash
su - john
```
**Breakdown:**
- `su`: The command to switch users.
- `-`: Loads the target user's environment (e.g., home directory, shell settings).
- `john`: The user to switch to.

**Exercise:**
- Switch to the user `alice` and load their environment.

---

### Example 2: Run a Command as Another User
```bash
sudo -u john ls /home
```
**Breakdown:**
- `sudo`: The command to execute commands as another user.
- `-u john`: Specifies the user (`john`) to run the command as.
- `ls /home`: The command being executed.

**Exercise:**
- Run the command `whoami` as the user `alice`.

---

## 5. Advanced User and Group Management

### Example 1: Lock and Unlock a User Account
```bash
usermod -L john
usermod -U john
```
**Breakdown:**
- `usermod -L`: Locks the user account, preventing login.
- `usermod -U`: Unlocks the user account, allowing login.
- `john`: The user being locked/unlocked.

**Exercise:**
- Lock the user `alice` and then unlock them.

---

### Example 2: Check Password Expiry
```bash
chage -l john
```
**Breakdown:**
- `chage`: The command to manage password aging.
- `-l`: Lists the password expiry details for the user.
- `john`: The user being checked.

**Exercise:**
- Check the password expiry details for the user `alice`.
