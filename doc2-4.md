
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

## 4. Expanding an Existing Disk

### Command: `lvextend` and `resize2fs`
#### Example: Extend a Logical Volume (LVM)
```bash
lvextend -L +10G /dev/vg01/lv01
resize2fs /dev/vg01/lv01
```
**lvextend**: The command to extend a logical volume.

**-L +10G**: Increase the size of the logical volume by 10GB.

**/dev/vg01/lv01**: The logical volume to be extended.

**resize2fs**: The command to resize the filesystem on the logical volume.

**/dev/vg01/lv01**: The logical volume whose filesystem will be resized.

#### Exercise:
- Increase the size of `/dev/vg01/data` by 5GB and resize its filesystem.

---

## 5. Adding a Disk and Mounting to a Path

### Command: `mkfs.ext4` and `mount`
#### Example: Add a New Disk
```bash
mkfs.ext4 /dev/sdb1
mount /dev/sdb1 /mnt/mydisk
```
**mkfs.ext4**: The command to create an ext4 filesystem on a partition.

**/dev/sdb1**: The partition to be formatted.

**mount**: The command to attach a filesystem to a directory.

**/dev/sdb1**: The partition to be mounted.

**/mnt/mydisk**: The directory where the partition will be mounted.

#### Exercise:
- Format `/dev/sdc1` with the ext4 filesystem and mount it to `/mnt/storage/`.

---

## 6. Filesystem Checks and Repairs

### Command: `fsck`
#### Example: Check and Repair a Filesystem
```bash
fsck /dev/sda1
```
**fsck**: The command to check and repair a filesystem.

**/dev/sda1**: The partition to be checked and repaired.

#### Exercise:
- Check and repair the filesystem on `/dev/sdb2`.

---

## 7. Quota Examples

### Command: `quotacheck`, `quotaon`, and `edquota`
#### Example: Set Up Disk Quotas
```bash
quotacheck -cug /mnt/data
quotaon /mnt/data
edquota -u username
```
#### Exercise:
- Enable user and group quotas on `/home/` and edit quotas for `john_doe`.

---

## 8. Rsync and Timeshift

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
