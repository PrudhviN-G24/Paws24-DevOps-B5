# File Permissions and Archiving in Linux

## Table of Contents

1. [File Permissions and Ownership](#file-permissions-and-ownership)
   - [Understanding File Permissions](#understanding-file-permissions)
   - [Changing Permissions with chmod](#changing-permissions-with-chmod)
   - [Changing Ownership with chown](#changing-ownership-with-chown)
   - [Real-world Examples for Permissions](#real-world-examples-for-permissions)
   - [Sticky Bit](#sticky-bit)
2. [File Compression and Archiving](#file-compression-and-archiving)
   - [Working with zip and unzip](#working-with-zip-and-unzip)
   - [Using tar for Archiving](#using-tar-for-archiving)
   - [Working with gzip and gunzip](#working-with-gzip-and-gunzip)
   - [Using bzip2 and bunzip2](#using-bzip2-and-bunzip2)
   - [Using xz and unxz](#using-xz-and-unxz)

---

## File Permissions and Ownership

File permissions and ownership in Linux determine who can access or modify files and directories.

### Understanding File Permissions

Each file or directory has three types of permissions:

- **Read (r)**: Permission to view the contents.
- **Write (w)**: Permission to modify the contents.
- **Execute (x)**: Permission to execute files (if they are scripts or binaries).

These permissions are divided into three categories:
- **Owner**: The user who owns the file.
- **Group**: A group of users who share access.
- **Others**: Everyone else.

![image](https://github.com/user-attachments/assets/f86f672f-8c0a-482c-b02e-f3758c793709)


Permissions are displayed using `ls -l`, with the format `-rwxr-xr--`:

| Character | Meaning               |
|-----------|-----------------------|
| `-`       | Regular file          |
| `d`       | Directory             |
| `r`       | Read permission       |
| `w`       | Write permission      |
| `x`       | Execute permission    |
| `-`       | No permission         |

#### Example:
```bash
ls -l file.txt
-rw-r--r-- 1 user group 1024 Jan 1 12:00 file.txt
```
- **Owner**: `rw-` (read, write)
- **Group**: `r--` (read-only)
- **Others**: `r--` (read-only)

---

### Changing Permissions with `chmod`

The `chmod` command is used to modify file permissions.

#### Syntax
```bash
chmod [permissions] [file/directory]
```

#### Examples
1. **Grant Execute Permission to the Owner**:
   ```bash
   chmod u+x script.sh
   ```
   Before: `-rw-r--r--`
   After:  `-rwxr--r--`

2. **Set Permissions Numerically**:
   ```bash
   chmod 755 script.sh
   ```
   - `7` (Owner): Read, write, execute (`4+2+1`)
   - `5` (Group): Read, execute (`4+1`)
   - `5` (Others): Read, execute (`4+1`)

3. **Remove Write Permission from Group and Others**:
   ```bash
   chmod go-w file.txt
   ```
   Before: `-rw-rw-r--`
   After:  `-rw-r--r--`

---

### Changing Ownership with `chown`

The `chown` command changes file or directory ownership.

#### Syntax
```bash
chown [owner][:group] [file/directory]
```

#### Examples
1. **Change the Owner**:
   ```bash
   chown alice file.txt
   ```
   Before: `-rw-r--r-- 1 bob users file.txt`
   After:  `-rw-r--r-- 1 alice users file.txt`

2. **Change the Owner and Group**:
   ```bash
   chown alice:developers file.txt
   ```
   Before: `-rw-r--r-- 1 alice users file.txt`
   After:  `-rw-r--r-- 1 alice developers file.txt`

3. **Recursively Change Ownership**:
   ```bash
   chown -R alice:developers project/
   ```
   Changes the owner and group for all files and subdirectories in `project/`.

---

### Real-world Examples for Permissions

#### Scenario 1: Restricting Access to a File
If a file has the following permissions:
```bash
-rw------- 1 test users 1024 Jan 1 12:00 confidential.txt
```
- **Owner (`test`)** can read and write the file.
- **Others (including `ec2-user`)** cannot access the file unless:
  1. **`ec2-user` is granted access** via `chmod` or `chown`.
  2. **`ec2-user` uses `sudo` privileges**:
     ```bash
     sudo cat confidential.txt
     ```
     `sudo` overrides file permissions as it grants root privileges.

#### Scenario 2: Restricting Access to a Directory
For a directory:
```bash
drwx------ 2 test users 4096 Jan 1 12:00 private_dir
```
- Only the **Owner (`test`)** can access the directory.
- **Others (including `ec2-user`)** cannot list or access the contents unless:
  1. **`ec2-user` uses `sudo`** to override permissions:
     ```bash
     sudo ls private_dir
     ```

#### Scenario 3: Granting Access to a Group
If a directory should be accessible to the group `developers`:
1. Change the group:
   ```bash
   chown :developers shared_dir
   ```
2. Add group permissions:
   ```bash
   chmod g+rwx shared_dir
   ```
   Result:
   ```bash
drwxrwx--- 2 alice developers 4096 Jan 1 12:00 shared_dir
   ```
   - Now all members of the `developers` group can access the directory.

---

### Sticky Bit

The **sticky bit** is a special permission that can be set on directories to restrict file deletion.

#### Purpose
When the sticky bit is set on a directory:
- Only the **owner** of a file or directory (or the `root` user) can delete or modify it.
- Even users with write access to the directory cannot delete files they do not own.

#### Common Use Case
The sticky bit is often used on shared directories like `/tmp` to prevent users from deleting or modifying each other's files.

#### Syntax
```bash
chmod +t [directory]
```

#### Examples
1. **Set the Sticky Bit**
   ```bash
   chmod +t shared_dir
   ```
   Before:
   ```bash
drwxrwxrwx 2 alice developers 4096 Jan 1 12:00 shared_dir
   ```
   After:
   ```bash
drwxrwxrwt 2 alice developers 4096 Jan 1 12:00 shared_dir
   ```
   The `t` at the end indicates the sticky bit is set.

2. **Remove the Sticky Bit**
   ```bash
   chmod -t shared_dir
   ```

3. **Verify the Sticky Bit**
   Use `ls -ld` to verify:
   ```bash
   ls -ld /tmp
   drwxrwxrwt 10 root root 4096 Jan 1 12:00 /tmp
   ```

In the above example, `/tmp` is a shared directory where the sticky bit ensures that users cannot delete files owned by others.

---

## File Compression and Archiving

Linux offers several tools for compressing and archiving files to save space and facilitate file transfers.

### Working with `zip` and `unzip`

#### Syntax
```bash
zip [options] [archive-name.zip] [file/directory]
unzip [archive-name.zip]
```

#### Examples
1. **Create a Zip Archive**:
   ```bash
   zip archive.zip file1.txt file2.txt
   ```
2. **Compress a Directory**:
   ```bash
   zip -r archive.zip directory/
   ```
3. **Extract a Zip Archive**:
   ```bash
   unzip archive.zip
   ```

---

### Using `tar` for Archiving

The `tar` command creates, extracts, or modifies archives.

#### Syntax
```bash
tar [options] [archive-name.tar] [file/directory]
```

#### Examples
1. **Create a tar Archive**:
   ```bash
   tar -cvf archive.tar file1.txt file2.txt
   ```
2. **Extract a tar Archive**:
   ```bash
   tar -xvf archive.tar
   ```
3. **Compress with gzip**:
   ```bash
   tar -czvf archive.tar.gz directory/
   ```
4. **Extract a gzipped Archive**:
   ```bash
   tar -xzvf archive.tar.gz
   ```

---

### Working with `gzip` and `gunzip`

#### Syntax
```bash
gzip [file]
gunzip [file.gz]
```

#### Examples
1. **Compress a File**:
   ```bash
   gzip file.txt
   ```
   Result: `file.txt.gz`
2. **Decompress a File**:
   ```bash
   gunzip file.txt.gz
   ```

---

### Using `bzip2` and `bunzip2`

#### Syntax
```bash
bzip2 [file]
bunzip2 [file.bz2]
```

#### Examples
1. **Compress a File**:
   ```bash
   bzip2 file.txt
   ```
   Result: `file.txt.bz2`
2. **Decompress a File**:
   ```bash
   bunzip2 file.txt.bz2
   ```

---

### Using `xz` and `unxz`

#### Syntax
```bash
xz [file]
unxz [file.xz]
```

#### Examples
1. **Compress a File**:
   ```bash
   xz file.txt
   ```
   Result: `file.txt.xz`
2. **Decompress a File**:
   ```bash
   unxz file.txt.xz
   ```

---

