# Controlling File Permissions and Ownership

This repository contains a hands-on lab focused on managing Linux file system security. You will learn to interpret standard permissions, modify ownership models, configure advanced special permission bits (SUID, SGID, Sticky Bit), and audit basic SELinux security contexts.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- View and accurately interpret Linux standard file permissions using `ls -l`.
- Modify read, write, and execute permissions using symbolic and numeric `chmod` modes.
- Reassign file and directory infrastructure governance using `chown` and `chgrp`.
- Configure special operational security flags: **SUID**, **SGID**, and the **Sticky Bit**.
- Inspect and re-label **SELinux mandatory access control security contexts**.

## 📋 Prerequisites
- A system running Linux (Red Hat Enterprise Linux, Fedora, or CentOS Stream recommended).
- Basic familiarity running system command-line utilities.
- Administrative elevation privileges (`sudo` or `root`) to execute structural protection changes.

---

## ⚙️ Lab Setup
1. Open your terminal window.
2. Initialize and step into a isolated sandbox practice workspace:
   ```bash
   mkdir ~/permissions_lab
   cd ~/permissions_lab
   ```

---

## 🛠️ Lab Tasks

### Task 1: Viewing File Permissions

#### Subtask 1.1: Understanding ls -l Output
1. Generate a test file and folder instance:
   ```bash
   touch file1.txt
   ```
   ```bash
   mkdir dir1
   ```
2. Read out the access rights vector map:
   ```bash
   ls -l
   ```
   *Expected Output Layout:*
   ```text
   -rw-r--r-- 1 user user    0 Jan 1 10:00 file1.txt
   drwxr-xr-x 2 user user 4096 Jan 1 10:00 dir1
   ```

📌 **Metadata Component Matrix Breakdown**:
- **First Character**: `-` represents a regular standard file; `d` represents a directory folder structure.
- **Next 9 Characters**: Access bits grouped into sets of three tracking **User (Owner)**, **Group**, and **Others** (e.g., `rwx` = Read, Write, Execute).
- **Following Blocks**: Total hard link counts, Owner metadata name, Group metadata name, total file size, update timestamp, and file identifier name.

#### Subtask 1.2: Viewing Hidden Files
1. Use the all-inclusive flag to view directory system metadata entries and hidden configuration items (files starting with a dot `.`):
   ```bash
   ls -la
   ```

---

### Task 2: Modifying Permissions

#### Subtask 2.1: Using chmod (Symbolic Mode)
1. Grant explicit execute access privilege specifically to the User Owner metadata dimension:
   ```bash
   chmod u+x file1.txt
   ```
2. Strip out reading allowances away from the target group permissions boundary line:
   ```bash
   chmod g-r file1.txt
   ```
3. Batch assign explicit settings mapping multi-segment roles simultaneously while stripping others completely:
   ```bash
   chmod u=rwx,g=rx,o= file1.txt
   ```

#### Subtask 2.2: Using chmod (Numeric Mode)
1. Apply a standard binary-octal permission layout map yielding `rwxr-xr-x` properties across target nodes:
   ```bash
   chmod 755 file1.txt
   ```
2. Apply restrictive, secure settings (`rw-------`) isolating the file exclusively to the Owner workspace:
   ```bash
   chmod 600 file1.txt
   ```

#### 📌 Common Reference Values Quick Matrix


| Octal Value | Absolute Privilege Operational Mapping |
| :--- | :--- |
| `755` | **Owner**: Read/Write/Execute (`rwx`) \| **Group/Others**: Read/Execute Only (`r-x`) |
| `644` | **Owner**: Read/Write (`rw-`) \| **Group/Others**: Read-Only (`r--`) |
| `700` | **Owner**: Read/Write/Execute (`rwx`) \| **Group/Others**: Denied All Access (`---`) |

---

### Task 3: Managing Ownership

#### Subtask 3.1: Using chown
1. Change the primary user ownership assignment level of your file object over to the root administrative account:
   ```bash
   sudo chown root file1.txt
   ```
2. Reassign both the system user owner reference and the group association layout concurrently in one execution path:
   ```bash
   sudo chown user:users file1.txt
   ```

#### Subtask 3.2: Using chgrp
1. Pivot the isolated group administration boundary target independently without touching user maps:
   ```bash
   sudo chgrp wheel file1.txt
   ```

---

### Task 4: Special Permission Bits

#### Subtask 4.1: SUID (Set User ID)
1. Inspect a standard system authentication tool profile configuration to evaluate its structural bit properties:
   ```bash
   which passwd
   ls -l /usr/bin/passwd
   ```
2. Apply SUID privileges to an executable binary (allows processes to run inheriting the absolute authorization tier of the *file owner* rather than the running user):
   ```bash
   sudo chmod u+s /usr/bin/passwd
   ```

#### Subtask 4.2: SGID (Set Group ID)
1. Configure a collaboration folder framework where any newly created child elements automatically inherit the group context of the parent directory:
   ```bash
   mkdir shared_dir
   sudo chmod g+s shared_dir
   ```

#### Subtask 4.3: Sticky Bit
1. Enforce global access protection flags across public file pools (restricts delete actions exclusively to the explicit creator of a given file):
   ```bash
   sudo chmod +t /tmp
   ls -ld /tmp
   ```

---

### Task 5: SELinux Contexts

#### Subtask 5.1: Viewing Contexts
1. Deploy standard operational policy tools if missing from your active kernel image stack:
   ```bash
   sudo dnf install policycoreutils-python-utils -y
   ```
2. Audit the operational Mandatory Access Control (MAC) safety labels mapped to a file node target:
   ```bash
   ls -Z file1.txt
   ```

#### Subtask 5.2: Modifying Contexts
1. Alter a file security context to map manually against a runtime target (e.g., exposing content via web services):
   ```bash
   sudo chcon -t httpd_sys_content_t file1.txt
   ```
2. Strip out temporary configuration updates and reset default structural labels inherited from policy templates:
   ```bash
   sudo restorecon -v file1.txt
   ```

---

## 💡 Troubleshooting Tips

* **Permission Denied Across Targets**:
  - Audit active properties maps directly via `ls -l`.
  - Validate your current running workspace shell privileges.
  - If standard rules match up perfectly but authorization remains blocked, look up policy validation markers using `ls -Z`.
* **Ownership Change Failures**: Ensure you are running under a elevated context (`sudo`). Check existence mappings using system lookups: `getent passwd` and `getent group`.
* **Special Flags Missing**: Inspect your directory strings closely inside `ls -l`. SUID projects an `s` flag where the User execution bit sits; SGID places `s` inside the Group position; Sticky Bit shows a `t` flag within the public Others execution column.

---

## 🏁 Conclusion
During this lab session, you developed crucial production system security skills, including:
- Deciphering standard permissions attributes arrays.
- Changing infrastructure operational metadata identities.
- Constructing highly specialized security boundary layers (SUID/SGID/Sticky Bit).
- Modifying standard SELinux security contexts.

These skills are absolute essentials when securing isolated microservice nodes, locking down container disk assets, organizing large corporate developer structures, or securing cloud clusters running engine workloads like Podman and OpenShift.

---

## 🧹 Cleanup
Return your user system profile footprint back to normal by removing the workspace files path:
```bash
rm -rf ~/permissions_lab
```

---

## 🚀 Further Exploration
- Evaluate explicit advanced data access rule matrix grids using Access Control Lists via `getfacl` and `setfacl`.
- Investigate file safety properties integration points mapping across active Container Engine execution nodes.
- Experiment with customized workspace constraints tags by testing out the Podman engine runtime string parameter `--security-opt`.
