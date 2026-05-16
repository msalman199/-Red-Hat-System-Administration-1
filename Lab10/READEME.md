# Configuring and Securing SSH

This repository contains a hands-on lab focused on installing, configuring, hardening, and securing the OpenSSH server daemon (`sshd`). You will implement identity protection layers, transition to cryptography key-based authentication, and configure firewall rules to restrict access.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Install and deploy the OpenSSH server package for remote network access.
- Harden server configurations via `/etc/ssh/sshd_config` to eliminate common vulnerability vectors.
- Implement secure, passwordless **Key-Based Authentication** using elliptic-curve cryptography (`ed25519`).
- Restrict remote network footprint vectors utilizing platform firewalls (`ufw` / `firewalld`).

## 📋 Prerequisites
- A Linux-based operating system distribution (e.g., Ubuntu, RHEL, or CentOS Stream).
- Terminal access featuring elevated `sudo` system administration privileges.
- Basic familiarity running foundational command-line interface (CLI) commands.

---

## 🛠️ Lab Tasks

### Task 1: Install OpenSSH Server
**Objective**: Detect existing capabilities and provision core remote access infrastructure dependencies.

1. Open your terminal window and verify if the OpenSSH tool suite is already active:
   ```bash
   ssh -V
   ```
   *Expected Output Sample:* `OpenSSH_8.9p1 Ubuntu-3, OpenSSL 3.0.2 15 Mar 2022`

2. If the package binaries are missing, install them via your native platform manager:
   ```bash
   sudo apt update && sudo apt install openssh-server -y   # For Debian / Ubuntu
   ```
   ```bash
   sudo dnf install openssh-server -y                     # For RHEL / CentOS Stream
   ```
3. Evaluate the initialization daemon's runtime performance state:
   ```bash
   sudo systemctl status ssh   # Note: service may be named 'sshd' on RHEL-based systems
   ```

💡 **Troubleshooting**: If the service ledger reports an inactive or dead status state, kickstart the operational thread by executing `sudo systemctl start ssh` (or `sshd`).

---

### Task 2: Modify /etc/ssh/sshd_config for Security
**Objective**: Eliminate systemic vulnerabilities by applying defense-in-depth parameter modifications.

1. **Create a Backup**: Always save a pristine snapshot replica of your baseline configuration before manual edits:
   ```bash
   sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
   ```
2. Open the primary parameter layout configuration file inside your terminal editor:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
3. Locate and alter the following security policy lines within the text block:
   ```text
   Port 2222                  # Move off default port 22 to mitigate brute-force bots
   PermitRootLogin no         # Block direct administrative root accounts access
   PasswordAuthentication no  # Disable weak text password inputs globally
   PubkeyAuthentication yes   # Explicitly mandate cryptographic identity verification
   AllowUsers your_username   # Restrict authentication matching strictly to listed accounts
   ```
4. **Apply Changes**: Trigger a daemon runtime validation and environment recycle phase:
   ```bash
   sudo systemctl restart ssh
   ```
5. Verify that your server process listener successfully pinned onto the new custom network interface target:
   ```bash
   ss -tulnp | grep ssh
   ```

💡 **Troubleshooting**: If your service wrapper fails to cycle online cleanly, investigate configuration trace parameters immediately via `sudo journalctl -xe`.

---

### Task 3: Generate SSH Keys for Key-Based Authentication
**Objective**: Establish a high-security key-exchange profile architecture.

1. **Client-Side Generation**: Generate a secure public/private cryptographic keypair from your client machine:
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   *(Press `Enter` to confirm default folder routing pathways. Supplying a protective passphrase string is highly recommended for security).*

2. **Key Transmission**: Copy your public key footprint safely onto the remote machine layout node:
   ```bash
   ssh-copy-id -p 2222 username@server_ip
   ```
3. **Verify Passwordless Entry**: Confirm your external login routine drops straight into the remote shell:
   ```bash
   ssh -p 2222 username@server_ip
   ```

💡 **Troubleshooting**: If your keys reject the stream, ensure remote filesystem storage boundaries feature safe file and folder permission matrices: `chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys`.

---

### Task 4: Configure Firewall for SSH
**Objective**: Explicitly authorize custom network ports across internal network shields.

#### Options for UFW (Ubuntu/Debian)
1. Permit your custom port through the internal network rules tracker:
   ```bash
   sudo ufw allow 2222/tcp
   ```
2. Enable the active boundary policy ruleset map:
   ```bash
   sudo ufw enable
   ```
3. Review active packet rule maps:
   ```bash
   sudo ufw status
   ```

#### Options for firewalld (RHEL/CentOS Stream)
1. Inject the persistent port tracking declaration rule directly into active runtime layers:
   ```bash
   sudo firewall-cmd --permanent --add-port=2222/tcp
   ```
2. Command the firewall logic engine to synchronize and load backend rules:
   ```bash
   sudo firewall-cmd --reload
   ```
3. List active explicit tracking paths to confirm compliance:
   ```bash
   sudo firewall-cmd --list-ports
   ```
   *Expected Output Matrix:* `2222/tcp`

---

## 🏁 Conclusion
During this lab session, you developed crucial system engineering hardening capabilities, including:
- Deploying foundational remote daemon engines cleanly.
- Tightening system entries by disabling root access vectors and interactive text passwords.
- Structuring elliptic-curve network validation signatures.
- Re-architecting firewall rules trackers to mirror customized infrastructure modifications.

---

## 🚀 Next Steps
- Verify outside connectivity maps definitively from a completely separate machine vector.
- Consider deploying intrusion prevention wrappers like **Fail2ban** to automatically block malicious network sweeps.

---

## 🔎 Final Verification Checkout
Validate your structural compliance criteria using the targeted authentication verification sequence below:
```bash
ssh -p 2222 username@server_ip
```
*(The execution step must drop cleanly into the system shell directly without prompting for a system account password string).*
