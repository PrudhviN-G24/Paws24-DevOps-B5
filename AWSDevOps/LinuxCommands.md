# Linux Command Guide

A comprehensive guide to commonly used Linux commands with examples and explanations.

---

## Table of Contents
1. [Introduction](#introduction)
2. [List Operations](#list-operations)
   - [Basic Listing](#basic-listing)
   - [Sorting](#sorting)
   - [Sorting by Size](#sorting-by-size)
   - [Different Formats](#different-formats)
   - [Miscellaneous Commands](#miscellaneous-commands)
3. [File and Directory Operations](#file-and-directory-operations)
   - [Creating Directories](#creating-directories)
   - [Viewing and Modifying Files](#viewing-and-modifying-files)
   - [Changing Directories](#changing-directories)
   - [Copy, Move, Rename, and Delete Files/Folders](#copy-move-rename-and-delete-filesfolders)
4. [Finding Files and Folders](#finding-files-and-folders)
5. [Filters in Linux](#filters-in-linux)
   - [Cut Command](#cut-command-in-linux)
   - [Grep Command](#grep-command-in-linux)
   - [Sed Command](#sed-command-in-linux)
   - [Tee Command](#tee-command-in-linux)
   - [Tr Command](#tr-command-in-linux)
   - [Uniq Command](#uniq-command-in-linux)
   - [Wc Command](#wc-command-in-linux)
   - [Sort Command](#sort-command-in-linux)
   - [AWK Command](#awk-command-in-linux)
6. [Vi Editor](#vi-editor)

---

## Introduction
Linux is a versatile operating system widely used for its command-line interface, which provides powerful tools for system administration, development, and data processing.

### Example Commands
- `uname -a` - Display all system information.
- `whoami` - Show the current logged-in user.
- `date` - Display the current system date and time.

---

## List Operations

### Basic Listing
- `ls` - List files and directories in the current directory.
- `ls -a` - Show all files, including hidden ones.
- `ls -l` - Display detailed information for files and directories.
  - Example:
    ```
    ls -l
    total 12
    -rw-r--r-- 1 user user  0 Jan  1 12:00 file1
    drwxr-xr-x 2 user user 64 Jan  1 12:00 dir1
    ```

### Sorting
- `ls -lt` - Sort files by modification time.
- `ls -ltr` - Sort files by modification time in reverse order.
- `ls -S` - Sort files by size.

### Sorting by Size
- `ls -lh` - Show file sizes in a human-readable format.
  - Example:
    ```
    ls -lh
    -rw-r--r-- 1 user user 1.2K Jan  1 12:00 file1
    ```

### Different Formats
- `ls -1` - Display one file per line.
- `ls -m` - List files separated by commas.

### Miscellaneous Commands
- `ls -R` - Recursively list directories.
- `ls -d */` - List only directories.
  - Example:
    ```
    ls -d */
    dir1/  dir2/  dir3/
    ```

---

## File and Directory Operations

### Creating Directories
- `mkdir <directory>` - Create a new directory.
- `mkdir -p dir1/dir2` - Create nested directories.
  - Example:
    ```
    mkdir -p projects/code
    ```

### Viewing and Modifying Files
- `cat <file>` - Display the content of a file.
- `echo "Hello, World!" > file.txt` - Create a file with content.
- `echo "More Content" >> file.txt` - Append content to a file.
  - Example:
    ```
    cat file.txt
    Hello, World!
    More Content
    ```

### Changing Directories
- `cd <directory>` - Change to a specified directory.
- `cd ..` - Move to the parent directory.
- `cd` - Return to the home directory.

### Copy, Move, Rename, and Delete Files/Folders
- `cp <source> <destination>` - Copy files or directories.
- `mv <source> <destination>` - Move or rename files or directories.
- `rm <file>` - Remove a file.
  - Example:
    ```
    rm old_file.txt
    ```
- `rm -r <directory>` - Remove a directory and its contents.
  - Example:
    ```
    rm -r old_directory
    ```
- `rm -rf <directory>` - Forcefully remove a directory and its contents (use with caution).
  - Example:
    ```
    rm -rf critical_directory
    ```
  - **Precautionary Note**: Be extremely careful when using `rm -rf`, especially as the root user. It can permanently delete critical system files if used incorrectly. Always double-check the command before execution.
- `rmdir <directory>` - Remove an empty directory.
  - Example:
    ```
    rmdir empty_directory
    ```
  - Example:
    ```
    cp file1.txt backup/
    mv file1.txt renamed_file.txt
    rm renamed_file.txt
    ```

---

## Finding Files and Folders
- `find <path> -name <pattern>` - Search for files by name.
- `find <path> -type d` - Search for directories only.
  - Example:
    ```
    find /home/user -name "*.txt"
    ```

- `locate <pattern>` - Quickly find files using a pre-built index.
  - Example:
    ```
    locate file.txt
    ```

- `which <command>` - Locate the executable path of a command.
  - Example:
    ```
    which python
    /usr/bin/python
    ```

---

## Filters in Linux

Filters are used to process text or data streams and extract meaningful information.

---

### Cut Command in Linux
The `cut` command is useful for selecting specific columns of a file. It allows cutting sections by byte position, character, or field.

- `cut -d- -f(columnNumber) <fileName>` - Use hyphen `-` as a delimiter.
- `cut -d ' ' -f(columnNumber) <fileName>` - Use space as a delimiter.
- `cut -b <byte number> <fileName>` - Cut by byte position.
- `cut -c <characters> <fileName>` - Cut by character(s) (ranges allowed).
  - Example: `cut -c1-5 <fileName>` extracts characters from position 1 to 5.
- `cut --complement <complement pattern> <fileName>` - Use complement patterns to exclude specific fields.
  - Example:
    ```
    echo "a-b-c" | cut -d- -f2
    b
    ```

---

### Grep Command in Linux
The `grep` command searches for specific patterns or keywords in files or streams.

- `grep "pattern" <fileName>` - Search for a specific pattern.
- `grep -i "pattern" <fileName>` - Case-insensitive search.
- `grep "pattern" file1 file2` - Search across multiple files.
- `grep -v "pattern" <fileName>` - Exclude lines matching the pattern.
- `grep -c "pattern" <fileName>` - Count matching lines.
- `grep -n "pattern" <fileName>` - Display line numbers with matches.
- `grep -w "pattern" <fileName>` - Search for the whole word only.
- `grep "pattern" -r <dir>` - Search recursively in a directory.
- `grep -A/B/C <lines> "pattern" <fileName>` - Display lines before (`-B`), after (`-A`), or surrounding (`-C`) the match.
- `grep -E 'pattern1|pattern2' <fileName>` - Use extended regular expressions to match multiple patterns.
  - Example:
    ```
    grep -E 'cat|dog' animals.txt
    ```

---

### Sed Command in Linux
The `sed` command is a powerful stream editor for performing text manipulations.

- `sed 's/old/new/' <file>` - Search and replace the first occurrence.
- `sed 's/old/new/g' <file>` - Replace all occurrences globally.
- `sed -i 's/old/new/' <file>` - Edit the file in place.
- `sed '/pattern/d' <file>` - Delete lines matching a pattern.
- `sed -n '/pattern/p' <file>` - Print lines matching a pattern.
- `sed '/pattern/i Inserted text' <file>` - Insert text before a pattern.
- `sed '/pattern/a Appended text' <file>` - Append text after a pattern.
  - Example:
    ```
    echo -e "apple\nbanana\ncherry" | sed 's/apple/orange/'
    orange
    banana
    cherry
    ```

---

### Tee Command in Linux
The `tee` command reads input and writes it to both standard output and files.

- `tee <file>` - Write output to a file.
- `tee -a <file>` - Append to the file instead of overwriting.
  - Example:
    ```
    echo "Hello World" | tee file.txt
    ```

---

### Tr Command in Linux
The `tr` command translates, deletes, or squeezes repeated characters.

- `tr 'a-z' 'A-Z'` - Convert lowercase to uppercase.
- `tr -d '0-9'` - Delete digits.
- `tr -s ' '` - Squeeze repeated spaces.
- `tr -cd 'A-Za-z'` - Remove all non-alphabetic characters.
  - Example:
    ```
    echo "hello    world" | tr -s ' '
    hello world
    ```

---

### Uniq Command in Linux
The `uniq` command removes duplicate lines.

- `uniq <file>` - Display unique lines.
- `uniq -c <file>` - Count occurrences of each line.
- `uniq -d <file>` - Display only duplicate lines.
  - Example:
    ```
    echo -e "a\na\nb\nc\nc" | uniq -c
        2 a
        1 b
        2 c
    ```

---

### Wc Command in Linux
The `wc` command counts lines, words, and characters in files.

- `wc -l <file>` - Count lines.
- `wc -w <file>` - Count words.
- `wc -c <file>` - Count characters.
- `wc -L <file>` - Display the longest line's length.
  - Example:
    ```
    echo -e "Hello World\nLinux Commands" | wc -w
    4
    ```
- **Combining with Other Commands**:
  - `ls | wc -l` - Count the number of files in the current directory.
    ```
    ls | wc -l
    5
    ```

---

### Sort Command in Linux
The `sort` command organizes text lines in ascending/descending order.

- `sort <file>` - Sort alphabetically.
- `sort -n <file>` - Sort numerically.
- `sort -r <file>` - Reverse order.
- `sort -u <file>` - Remove duplicates.
  - Example:
    ```
    echo -e "3\n1\n2" | sort -n
    1
    2
    3
    ```

---

### AWK Command in Linux
The `awk` command processes and analyzes structured data.

- `awk '{print $1}' <file>` - Print the first column.
- `awk '/pattern/ {action}' <file>` - Perform actions for lines matching a pattern.
- `awk '{print NR, $0}' <file>` - Print line numbers with content.
  - Example:
    ```
    echo -e "apple banana\ncarrot dog" | awk '{print NR, $1}'
    1 apple
    2 carrot
    ```

---

## Vi Editor

The `vi` editor is a widely used text editor in Linux, known for its efficiency and versatility. It operates in two primary modes:

- **Command Mode**: For navigating and executing commands.
- **Insert Mode**: For editing text.

### Common Commands

#### Switching Modes
- `i` - Switch to Insert mode.
- `Esc` - Switch back to Command mode.

#### Saving and Exiting
- `:w` - Save changes.
- `:q` - Quit the editor.
- `:wq` - Save changes and quit.
- `:q!` - Quit without saving changes.

#### Navigation
- `h` - Move left.
- `l` - Move right.
- `k` - Move up.
- `j` - Move down.
- `0` - Move to the beginning of the line.
- `$` - Move to the end of the line.

#### Editing Text
- `x` - Delete a character.
- `dd` - Delete a line.
- `yy` - Copy (yank) a line.
- `p` - Paste copied text.

#### Searching
- `/pattern` - Search forward for a pattern.
- `?pattern` - Search backward for a pattern.
- `n` - Repeat the search in the same direction.
- `N` - Repeat the search in the opposite direction.

