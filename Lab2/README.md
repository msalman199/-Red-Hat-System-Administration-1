# Logging into RHEL and Using the Shell

This repository contains a hands-on lab designed to guide you through accessing a Red Hat Enterprise Linux (RHEL) system locally and remotely, executing core shell commands, and configuring your command-line environment.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Log in to a RHEL system locally via the console.
- Log in to a RHEL system remotely using SSH.
- Execute basic shell navigation and help commands (`pwd`, `ls`, `man`, `exit`).
- Customize the shell prompt environment using the `PS1` variable.

## 📋 Prerequisites
- A RHEL 8 or RHEL 9 system (physical hardware or virtual machine).
- Active network connectivity (required for remote SSH access).
- A valid user account with standard privileges.
- An SSH server (`sshd`) installed and running on the target RHEL system.

---

## 🛠️ Lab Tasks

### Task 1: Local Console Login
**Objective**: Access the RHEL system directly from the physical hardware or VM console.

1. **Power on** your RHEL system or start the VM from your hypervisor.
2. Wait for the terminal login screen to display:
   ```text
   Red Hat Enterprise Linux 9.0 (Plow)
   Kernel 5.14.0-70.el9.x86_64 on an x86_64

   localhost login:
   ```
3. Type your **username**, press `Enter`, and type your **password** (note: characters will not echo on screen).
4. Verify your successful login by checking for the command prompt:
   ```bash
   [user@localhost ~]\$
   ```

💡 **Troubleshooting**: If you receive a `Login incorrect` error, check your Caps Lock key and verify credentials with your system administrator.

---

### Task 2: Remote SSH Login
**Objective**: Establish a secure remote connection to your RHEL system from a client machine.

1. **Verify SSH Status**: On the RHEL system, ensure the SSH service is running:
   ```bash
   sudo systemctl status sshd
   ```
   *(Output must state `active (running)`)*

2. **Find the IP Address**: Check the RHEL system network interface configuration:
   ```bash
   ip a
   ```
   *(Locate your active interface, such as `ens192` or `eth0`, and note the `inet` address)*

3. **Connect Remotely**: From your external client terminal (Linux, macOS, or Windows WSL), execute:
   ```bash
   ssh username@rhel-system-ip
   ```
   *Example:* `ssh user@192.168.1.100`

4. **Authenticate**: Type `yes` to accept the security host fingerprint if prompted, then enter your user password.

💡 **Troubleshooting**: If the connection times out, test connectivity using `ping rhel-system-ip`. If pinging fails, verify your physical network cables/vSwitches and check the target firewall configuration via `sudo firewall-cmd --list-all`.

---

### Task 3: Basic Shell Commands
**Objective**: Navigate the file system structure and review core documentation utilities.

* **Subtask 3.1: Print Working Directory**
  ```bash
  pwd
  ```
  *Expected Output:* `/home/username`

* **Subtask 3.2: List Directory Contents**
  ```bash
  ls
  ```
  *Common options:*
  - `ls -l` : Long listing format (shows permissions, owners, sizes, dates).
  - `ls -a` : Include hidden files (names starting with a dot `.`).
  - `ls -lh` : Human-readable file sizes (e.g., K, M, G).

* **Subtask 3.3: Access Manual Pages**
  ```bash
  man ls
  ```
  *(Navigate using arrow keys, search using `/searchterm`, and press `q` to quit)*

* **Subtask 3.4: Exit the Shell**
  ```bash
  exit
  ```
  *(Closes the active SSH remote stream or logs you out of the local console console session)*

---

### Task 4: Customize Shell Prompt (PS1)
**Objective**: Personalize the appearance of your CLI prompt layout.

1. **View Current Prompt Structure**:
   ```bash
   echo \$PS1
   ```
   *Default fallback configuration:* `[\u@\h \W]\$`

2. **Temporarily Modify Prompt**: Inject the current system time dynamically into your session layout:
   ```bash
   PS1="[\u@\h \W \t]\$ "
   ```

3. **Make Changes Permanent**: Append the variable rule directly to your local shell profile profile configuration:
   ```bash
   nano ~/.bashrc
   ```
   Add the following line to the absolute bottom of the file:
   ```bash
   export PS1="[\u@\h \W \t]\$ "
   ```
   Save the changes (`Ctrl+O`, `Enter`) and exit (`Ctrl+X`). Reload the environment profile mapping:
   ```bash
   source ~/.bashrc
   ```

#### 📌 Common PS1 Symbols Reference Table

| Symbol | Representation |
| :--- | :--- |
| `\u` | Current user account username |
| `\h` | Machine host name |
| `\W` | Present working directory name |
| `\t` | Live time sequence (HH:MM:SS format) |

---

## 🏁 Conclusion
In this lab, you have completed the following milestones:
- Authenticated via local system consoles and remote SSH utilities.
- Handled vital manual routing tools and base file listings.
- Customized shell prompts for enhanced personal workflows.

These core competencies serve as the foundational starting point for system operations in Red Hat enterprise environments and prepare you for containerized applications like Podman in OpenShift ecosystems.

## 🚀 Next Steps
- Reinforce your memory by repeating navigation syntax routines regularly.
- Discover advanced piping operators and basic content search rules via `cd`, `cat`, and `grep`.
- Explore fundamental shell scripting concepts to automate manual system operations.
