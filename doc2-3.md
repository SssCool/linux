# Linux Filesystem

## Introduction
The Linux filesystem is a hierarchical structure that organizes files and directories in a logical way. Understanding the filesystem is crucial for effective system administration, troubleshooting, and everyday usage.

## 1. Basics of the Linux Filesystem
### 1.1 Root Directory (`/`)
The root directory is the top-level directory in Linux from which all other directories branch out.

### 1.2 Common Directories
- `/bin` - Essential command binaries (e.g., `ls`, `cp`, `mv`)
- `/boot` - Bootloader files and kernel images
- `/dev` - Device files (e.g., `/dev/sda` for storage devices)
- `/etc` - System configuration files
- `/home` - User home directories
- `/lib` - Shared libraries and kernel modules
- `/mnt` - Temporary mount points for filesystems
- `/opt` - Optional software packages
- `/proc` - Virtual filesystem for system processes
- `/root` - Home directory of the root user
- `/sbin` - System binaries (e.g., `fdisk`, `shutdown`)
- `/tmp` - Temporary files (cleared on reboot)
- `/usr` - User utilities and applications
- `/var` - Variable data files (e.g., logs, cache)

### 1.3 File Types in Linux
- **Regular files**: Text, binary, scripts, etc.
- **Directories**: Containers for files and subdirectories
- **Symbolic links**: Shortcuts pointing to other files/directories
- **Special files**: Character (`c`) and block (`b`) device files
- **Sockets**: Used for inter-process communication
- **Named pipes**: Used for communication between processes

## 2. Understanding Filesystem Hierarchy Standard (FHS)
The FHS defines the directory structure and directory contents in Linux. It ensures consistency across different distributions.

## 3. Filesystem Permissions
### 3.1 Understanding Permission Format
Permissions are represented as `rwx` (read, write, execute). Example:
```
-rw-r--r--  1 user user 1234 Feb 18 10:00 file.txt
```
Breakdown:
- `-rw-r--r--`: Permissions
- `1`: Number of hard links
- `user`: Owner
- `user`: Group
- `1234`: File size in bytes
- `Feb 18 10:00`: Last modified date
- `file.txt`: File name

### 3.2 Changing Permissions
- `chmod`: Change file permissions (`chmod 755 script.sh`)
- `chown`: Change file owner (`chown user:group file.txt`)
- `chgrp`: Change group ownership (`chgrp group file.txt`)

## 4. Filesystem Management
### 4.1 Disk Partitioning
- `fdisk`: Manage disk partitions
- `parted`: Advanced partitioning tool
- `lsblk`: Display block devices
- `blkid`: Display partition UUIDs

### 4.2 Mounting and Unmounting Filesystems
- `mount`: Attach a filesystem (`mount /dev/sdb1 /mnt`)
- `umount`: Detach a filesystem (`umount /mnt`)
- `/etc/fstab`: Configures filesystems to be mounted at boot

### 4.3 Filesystem Types
- **Ext4**: Default filesystem in many Linux distros
- **XFS**: High-performance journaling filesystem
- **Btrfs**: Advanced features like snapshots and compression
- **NTFS, FAT32, exFAT**: Used for Windows compatibility

## 5. Advanced Filesystem Concepts
### 5.1 Logical Volume Manager (LVM)
LVM provides flexible disk management features:
- **Physical Volume (PV)**: Underlying physical storage
- **Volume Group (VG)**: Pool of PVs
- **Logical Volume (LV)**: Virtual partition from VG
- `lvcreate`, `lvextend`, `lvreduce`: Manage LVM partitions

### 5.2 Filesystem Checks and Repair
- `fsck`: Check and repair filesystems (`fsck /dev/sda1`)
- `tune2fs`: Adjust filesystem parameters
- `e2fsck`: Check and repair ext filesystems

### 5.3 Disk Usage Monitoring
- `df -h`: Show disk usage
- `du -sh`: Show directory size
- `ncdu`: Interactive disk usage analyzer

### 5.4 Quotas and Limits
- `quota`: Display user quotas
- `edquota`: Edit user quotas
- `repquota`: Report quota usage

## 6. Backups and Snapshots
- `rsync`: Synchronize and backup files (`rsync -av /source /destination`)
- `tar`: Archive files (`tar -cvf backup.tar /home/user`)
- `btrfs snapshots`: Create snapshots for rollback
- `timeshift`: GUI tool for system backups

## Conclusion
Understanding the Linux filesystem is essential for system administration and daily tasks. Mastering permissions, disk management, and backup strategies will enhance your Linux proficiency.

