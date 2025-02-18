
## 1. Copying Files and Directories

### Command: `cp`
#### Example 1: Copy a File
```bash
cp file.txt /home/user/documents/
```
**cp**: The command to copy files or directories.

**file.txt**: The source file to be copied.

**/home/user/documents/**: The destination directory where the file will be copied.

 

#### Example 2: Copy a Directory Recursively
```bash
cp -r /home/user/documents /backup/
```
**cp**: The command to copy files or directories.

**-r**: Recursively copy directories and their contents.

**/home/user/documents**: The source directory to be copied.

**/backup/**: The destination directory where the directory will be copied.

#### Exercise:
- Copy a file named `report.docx` to the `/tmp/backup/` directory.
- Copy the entire `/var/logs/` directory to `/home/user/log_backup/`.

---

## 2. Moving Files and Directories

### Command: `mv`
#### Example 1: Move a File
```bash
mv file.txt /home/user/documents/
```
**mv**: The command to move or rename files/directories.

**file.txt**: The source file to be moved.

**/home/user/documents/**: The destination directory where the file will be moved.

 

#### Example 2: Rename a File
```bash
mv oldname.txt newname.txt
```
**mv**: The command to move or rename files/directories.

**oldname.txt**: The current name of the file.

**newname.txt**: The new name for the file.

 

#### Exercise:
- Move a file named `data.csv` to `/home/user/archive/`.
- Rename the file `project.docx` to `final_project.docx`.

---

## 3. Compressing and Uncompressing with tar

### Command: `tar`
#### Example 1: Compress a Directory
```bash
tar -cvf archive.tar /home/user/documents
```
**tar**: The command to create or extract tar archives.

**-c**: Create a new archive.

**-v**: Verbose mode (show the files being processed).

**-f**: Specify the archive file name.

**archive.tar**: The name of the archive to be created.

**/home/user/documents**: The directory to be archived.

#### Example 2: Compress with Gzip
```bash
tar -czvf archive.tar.gz /home/user/documents
```
**tar**: The command to create or extract tar archives.

**-c**: Create a new archive.

**-z**: Compress the archive using gzip.

**-v**: Verbose mode (show the files being processed).

**-f**: Specify the archive file name.

**archive.tar.gz**: The name of the compressed archive.

**/home/user/documents**: The directory to be archived.

#### Example 3: Uncompress a Tar Archive
```bash
tar -xvf archive.tar
```
**tar**: The command to create or extract tar archives.

**-x**: Extract files from an archive.

**-v**: Verbose mode (show the files being processed).

**-f**: Specify the archive file name.

**archive.tar**: The name of the archive to be extracted.

#### Example 4: Uncompress a Gzip Tar Archive
```bash
tar -xzvf archive.tar.gz
```
**tar**: The command to create or extract tar archives.

**-x**: Extract files from an archive.

**-z**: Decompress the archive using gzip.

**-v**: Verbose mode (show the files being processed).

**-f**: Specify the archive file name.

**archive.tar.gz**: The name of the compressed archive to be extracted.

#### Exercise:
- Create a tar archive named `backup.tar` containing the `/etc/` directory.
- Extract the archive `logs.tar.gz` into `/var/tmp/`.

---
## 4. Disk extend and attach


Extending Disk

1. Verify hardware level disk expansion:
```bash
fdisk -l
```

2. Check volume information:
```bash
vgs    # Lists volume groups
lvs    # Lists logical volumes
```

3. Extend the physical partition:
```bash
growpart /dev/sda 1    # Replace sda with your disk and 1 with partition number
```

4. Extend the Physical Volume:
```bash
pvresize /dev/sda1    # Replace with your partition
```

5. Extend the Logical Volume:
```bash
lvextend -l +100%FREE /dev/mapper/vg-name-lv-name    # Replace with your VG and LV names
```

6. Resize the filesystem:
```bash
# For ext4 filesystem:
resize2fs /dev/mapper/vg-name-lv-name    
# OR for XFS filesystem:
xfs_growfs /dev/mapper/vg-name-lv-name   
```

## Attaching New Disk

1. Verify the new disk is visible:
```bash
fdisk -l
```

2. Create a new partition:
```bash
fdisk /dev/sdb
# Press 'n' for new partition
# Press 'p' for primary
# Accept defaults for partition number and sectors
# Press 'w' to write changes
```

3. Format the partition:
```bash
# For ext4:
mkfs.ext4 /dev/sdb1
# OR for XFS:
mkfs.xfs /dev/sdb1
```

4. Create mount point and mount:
```bash
mkdir /mnt/db_data
mount /dev/sdb1 /mnt/db_data
```

5. Add to /etc/fstab for permanent mounting:
```bash
echo "/dev/sdb1 /mnt/new_disk ext4 defaults 0 0" >> /etc/fstab
```


## 5. Rsync and Timeshift

### Command: `rsync`
#### Example 1: Backup with rsync
```bash
rsync -av /home/user /backup/
```
#### Exercise:
- Synchronize `/var/www/` with `/backup/www/` using rsync.

### Command: `timeshift`
#### Example 2: Create a Snapshot with timeshift
```bash
sudo apt install timeshift
```
#### Exercise:
- Install Timeshift and create a system snapshot.
