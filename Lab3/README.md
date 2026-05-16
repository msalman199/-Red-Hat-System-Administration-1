# Managing Files and Directories via CLI

This repository contains a hands-on lab focused on mastering essential Linux command-line tools for file and directory management, analyzing file system metadata, and handling input/output streams.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Create, move, copy, and delete files and directories using CLI commands.
- Inspect detailed file metadata using `ls -l` and `stat`.
- Control command data flows using standard redirection (`>`) and append (`>>`) operators.

## 📋 Prerequisites
- A Linux-based operating system (e.g., RHEL, Fedora, Ubuntu).
- Terminal access with standard user privileges.
- Basic familiarity with CLI directory navigation (`cd`).

---

## 🛠️ Lab Tasks

### Task 1: Creating Files and Directories

#### Subtask 1.1: Create a Directory
1. Open your terminal.
2. Initialize a new folder named `lab3_files`:
   ```bash
   mkdir lab3_files
   ```
3. Verify the directory creation:
   ```bash
   ls
   ```
   *Expected Output:* `lab3_files` appears in the item list.

#### Subtask 1.2: Create a File
1. Step into the newly created folder:
   ```bash
   cd lab3_files
   ```
2. Generate an empty file named `notes.txt`:
   ```bash
   touch notes.txt
   ```
3. Confirm the file exists:
   ```bash
   ls
   ```
   *Expected Output:* `notes.txt` appears in the item list.

---

### Task 2: Copying and Moving Files

#### Subtask 2.1: Copy a File
1. Duplicate your file into a backup copy:
   ```bash
   cp notes.txt notes_backup.txt
   ```
2. Verify both files exist side by side:
   ```bash
   ls
   ```
   *Expected Output:* Both `notes.txt` and `notes_backup.txt` are listed.

#### Subtask 2.2: Move a File
1. Create a dedicated storage subdirectory:
   ```bash
   mkdir backup
   ```
2. Relocate the backup file into that subdirectory:
   ```bash
   mv notes_backup.txt backup/
   ```
3. Verify the file path relocation:
   ```bash
   ls backup/
   ```
   *Expected Output:* `notes_backup.txt` is visible inside the `backup/` folder.

---

### Task 3: Exploring File Metadata

#### Subtask 3.1: List Files with Detailed Information
1. Use the long listing flag to view primary file attributes:
   ```bash
   ls -l
   ```
   *Expected Output:* Terminal displays ownership, permissions, size, and last modification timestamp.

#### Subtask 3.2: Use stat for Advanced Metadata
1. Extract extensive low-level file system metadata:
   ```bash
   stat notes.txt
   ```
   *Expected Output:* Detailed readout displaying the inode index number, access/modify/change time states, and explicit size in bytes.

---

### Task 4: Redirecting Output

#### Subtask 4.1: Redirect Output to a File
1. Direct the standard output stream of your directory list into a file (overwriting existing content):
   ```bash
   ls -l > file_list.txt
   ```
2. View the resulting file contents:
   ```bash
   cat file_list.txt
   ```
   *Expected Output:* The file contents mimic the direct terminal readout of `ls -l`.

#### Subtask 4.2: Append Output to a File
1. Concat the `stat` data stream to the end of the same file without overwriting it:
   ```bash
   stat notes.txt >> file_list.txt
   ```
2. Review the combined log file:
   ```bash
   cat file_list.txt
   ```
   *Expected Output:* The file displays the initial `ls -l` results followed immediately by the `stat` block.

---

### Task 5: Deleting Files and Directories

#### Subtask 5.1: Delete a File
1. Remove `notes.txt` from the directory:
   ```bash
   rm notes.txt
   ```
2. Verify the deletion:
   ```bash
   ls
   ```
   *Expected Output:* `notes.txt` is no longer visible.

#### Subtask 5.2: Delete a Directory
1. Delete the `backup` subdirectory along with all files nested within it:
   ```bash
   rm -r backup
   ```
2. Run a final directory check:
   ```bash
   ls
   ```
   *Expected Output:* The `backup` directory is entirely removed.

---

## 💡 Troubleshooting Tips

* **Permission Denied**: If your target path permissions are restricted, elevate your command execution privileges by prefixing it with `sudo` (e.g., `sudo rm -r backup`).
* **File Not Found**: Carefully verify exact spelling, capitalization, and relative path structures using `pwd`.
* **Accidental Deletion**: Exercise extreme caution when running `rm -r`. The Linux command-line does not have a recycle bin; deletions are immediate and permanent.

---

## 🏁 Conclusion
Through this lab, you developed essential CLI file and directory management skills covering core generation, movement tracking, structural deletion, system metadata scanning, and input/output stream management. These commands serve as fundamental building blocks for server engineering, scripting, and system administration routines.

## 🚀 Next Steps
- Reinforce your CLI capabilities by repeating these basic routines until they feel natural.
- Explore safety flags and advanced parameters like interactive confirmation (`cp -i`, `rm -i`) and viewing hidden files (`ls -a`).

---

## 📊 Lab Completion Checklist
- [x] Created files and directories
- [x] Copied and moved files
- [x] Viewed file metadata
- [x] Redirected output streams
- [x] Deleted files and directories
