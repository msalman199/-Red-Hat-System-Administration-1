# Managing Users and Groups

This repository contains a hands-on lab focused on essential system administration tasks in Linux, specifically creating and managing user accounts, organizing groups, implementing strict password security policies, and performing clean user de-provisioning.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Create, modify, and manage local user accounts and system groups.
- Configure password aging and account expiration policies.
- Alter user/group attributes and group administrator privileges.
- Cleanly remove user profiles, homes, and groups from the system.

## 📋 Prerequisites
- A Linux operating system (Red Hat Enterprise Linux, CentOS Stream, or Fedora recommended).
- Root access or active `sudo` administrative privileges.
- Basic familiarity running command-line interface (CLI) commands.

---

## ⚙️ Lab Setup
1. Open your terminal application.
2. Verify your administrative elevation privileges:
   ```bash
   sudo -v
   ```
3. Ensure the vital user management utility binaries are installed on your RHEL system:
   ```bash
   sudo dnf install -y shadow-utils
   ```

---

## 🛠️ Lab Tasks

### Task 1: User Management

#### 1.1 Creating Users
1. Spin up a new standard user account with an explicit home directory (`-m`) and set their primary login shell environment map to Bash (`-s`):
   ```bash
   sudo useradd -m -s /bin/bash labuser1
   ```
2. Initialize an account access credential authentication password for the new user profile:
   ```bash
   sudo passwd labuser1
   ```

💡 **Troubleshooting**: If your deployment step throws an error, check whether that specific account string exists in the local user database using the command `id labuser1`.

#### 1.2 Modifying Users
1. Alter an existing system user's configurations to change their active default login shell mapping to Zsh:
   ```bash
   sudo usermod -s /bin/zsh labuser1
   ```
2. Append descriptive metadata text notes (GECOS comment string) directly inside the user account profile record:
   ```bash
   sudo usermod -c "Lab User 1" labuser1
   ```
3. Verify your backend configurations directly inside the main user account database:
   ```bash
   grep labuser1 /etc/passwd
   ```

---

### Task 2: Group Management

#### 2.1 Creating Groups
1. Generate an independent security grouping boundary container inside your local system:
   ```bash
   sudo groupadd labgroup
   ```
2. Safely append your user to this group as a secondary supplementary membership block (`-aG`) without resetting previous groupings:
   ```bash
   sudo usermod -aG labgroup labuser1
   ```
3. Audit and verify the secondary attachments:
   ```bash
   groups labuser1
   ```

#### 2.2 Group Administrators
1. Designate your laboratory user as an explicit owner administrator tracking this target group:
   ```bash
   sudo gpasswd -A labuser1 labgroup
   ```
2. Leverage the secondary administration tools mapping to bind an external secondary profile into the container:
   ```bash
   sudo gpasswd -a labuser2 labgroup
   ```

---

### Task 3: Password Policies

#### 3.1 Password Aging with chage
1. Implement security lifecycle rules enforcing password resets, minimum update gaps, and warning windows:
   ```bash
   sudo chage -M 90 -m 7 -W 14 labuser1
   ```
2. Read out the active password policy ledger mapping associated with the target profile layout:
   ```bash
   sudo chage -l labuser1
   ```

#### 📌 Password Management Variables Reference Matrix

| Parameter Flag | Policy Restriction Rule Mapping |
| :--- | :--- |
| `-M` | **Maximum days** a user password remains valid before an mandatory change. |
| `-m` | **Minimum days** required between successive user password changes. |
| `-W` | **Warning days** notice shown before password expires. |

---

### Task 4: Cleanup

#### 4.1 Removing Users
1. Wipe the target account profile ledger from the database while *retaining* files on disk:
   ```bash
   sudo userdel labuser1
   ```
2. Completely purge a secondary profile from the server database, including their home directory matching strings (`-r`):
   ```bash
   sudo userdel -r labuser2
   ```

#### 4.2 Removing Groups
1. Remove the security group index entry item:
   ```bash
   sudo groupdel labgroup
   ```

---

## 🔎 Verification Steps
Confirm your clean teardown actions worked perfectly and check the active local account database to verify no residual laboratory accounts or groups remain:
```bash
cut -d: -f1 /etc/passwd
```

---

## 🏁 Conclusion
During this lab session, you explored foundational infrastructure identity operations, including:
- Creating, adapting, and configuring functional system user records.
- Engineering custom groups and delegating secondary delegation rights.
- Architecting strict password aging controls.
- Executing structural cleanup operations.

These management utilities represent a critical component of security frameworks for server administration, cluster compliance, and access auditing workflows.

---

## 💡 Troubleshooting Guide


| Log Issue Symptom | Root Cause Verification Method & Resolution Fix |
| :--- | :--- |
| `"user already exists"` | Query the namespace via `id username`, then run `userdel` if cleaning is required. |
| `Permission denied` | Prepend your command lines with a valid prefix pointing to `sudo`. |
| `Group not found` | Confirm structural mapping entries across the system utilizing `getent group groupname`. |

---

## 📚 Additional Resources
- Local documentation guides: `man useradd`, `man groupadd`, `man chage`
- Security management specifications: `/etc/passwd`, `/etc/group`, `/etc/shadow`
