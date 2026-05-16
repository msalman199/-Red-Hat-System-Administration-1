# Working with Network File Systems (NFS and CIFS)

This repository contains a hands-on lab focused on network storage integration within an enterprise Linux ecosystem. You will install client-side drivers, discover and map remote network file shares, enforce secure access patterns for multi-platform data volumes, and establish persistent, networks-aware mount maps via the `/etc/fstab` storage registry.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Provision and verify client-side utility binaries for **NFS** and **CIFS/SMB** transport layers.
- Audit remote storage nodes to discover exposed export directories.
- Mount network file systems dynamically over transient directory trees.
- Store sensitive cross-platform access credentials securely using restricted profile containers.
- Configure safe, persistent boot-time network mounts inside `/etc/fstab`.

## 📋 Prerequisites
- A Linux operating system (Red Hat Enterprise Linux, CentOS Stream, or Fedora recommended).
- Terminal access featuring elevated `sudo` system administration privileges.
- Reliable network routing pathways connecting your host to active remote file shares.
- *(Optional)* An active Samba or Windows Server host within reach to fully execute live CIFS validation steps.

---

## 🛠️ Lab Tasks

### Task 1: Install Required Packages
**Objective**: Update system package registries and deploy core storage network dependencies.

1. Open your terminal window and update local metadata caches:
   ```bash
   sudo dnf update -y
   ```
2. Deploy the core utility packages driving standard Linux network storage interactions:
   ```bash
   sudo dnf install -y nfs-utils cifs-utils
   ```
3. Audit your local package management engine to verify successful package installation states:
   ```bash
   rpm -q nfs-utils cifs-utils
   ```
   *Expected Output Matrix:* Displays explicit version records (e.g., `nfs-utils-2.x.x` and `cifs-utils-6.x.x`).

💡 **Distro Variation Tip**: If configuring an environment running on Debian or Ubuntu distributions, swap your package manager binary statement out for `apt`, and double-check target naming variations.

---

### Task 2: Mount NFS Shares
**Objective**: Interrogate remote Unix-native file nodes and establish active local data connections.

1. **Discover Exposed Exports**: Scan the remote host target to inventory every directory share made public across your network segment:
   ```bash
   showmount -e SERVER_IP
   ```
   *(Be sure to replace `SERVER_IP` with the literal network IP tracking your target storage engine).*
2. **Initialize Workspace**: Establish a designated entry folder path inside the machine file system structure:
   ```bash
   sudo mkdir -p /mnt/nfs_share
   ```
3. **Execute Binding**: Attach the remote directory branch cleanly to your active operating path:
   ```bash
   sudo mount -t nfs SERVER_IP:/share /mnt/nfs_share
   ```
4. **Audit Connection States**: Confirm that the new mount registers accurately alongside standard filesystems:
   ```bash
   df -hT | grep nfs
   ls /mnt/nfs_share
   ```

💡 **Troubleshooting**: If connection threads reject your commands, check the storage node host configuration using service management status calls: `systemctl status nfs-server`.

---

### Task 3: Mount CIFS/SMB Shares
**Objective**: Access Windows-compatible storage networks using hardened permission structures.

1. **Secure Credentials**: Isolate sensitive login credentials from globally viewable terminal layers by wrapping authentication parameters inside an independent plain text file:
   ```bash
   echo "username=USERNAME" | sudo tee /etc/cifs_credentials > /dev/null
   echo "password=PASSWORD" | sudo tee -a /etc/cifs_credentials > /dev/null
   ```
2. **Restrict Access Boundaries**: Force absolute read/write lockout protection states, rendering the authentication file viewable *only* by root administrative profiles:
   ```bash
   sudo chmod 600 /etc/cifs_credentials
   ```
3. **Execute Mounting**: Initialize a directory folder target and bind the remote network asset using your protected access credentials:
   ```bash
   sudo mkdir -p /mnt/cifs_share
   sudo mount -t cifs -o credentials=/etc/cifs_credentials //SERVER_IP/SHARENAME /mnt/cifs_share
   ```
4. **Verify Active Data Volumes**: Check allocation listings and directory read structures to validate active file availability:
   ```bash
   df -hT | grep cifs
   ls /mnt/cifs_share
   ```

💡 **Troubleshooting**: If file handshakes fail during the configuration process, install supportive debug diagnostic tools by executing `sudo dnf install samba-client`.

---

### Task 4: Configure Persistent Mounts in /etc/fstab
**Objective**: Incorporate network-aware parameters into boot registries for automated volume mounting.

1. **Save Configuration Snapshots**: Back up the pristine, current state of your system storage ledger before manual injection:
   ```bash
   sudo cp /etc/fstab /etc/fstab.bak
   ```
2. **Inject NFS Persistence Rule**: Append a stable, persistent system entry rule tracking the remote NFS share block:
   ```bash
   echo "SERVER_IP:/share  /mnt/nfs_share  nfs  defaults  0 0" | sudo tee -a /etc/fstab
   ```
3. **Inject CIFS Persistence Rule**: Append your remote CIFS network storage structure rule, passing explicit user ID mappings to retain ownership context:
   ```bash
   echo "//SERVER_IP/SHARENAME  /mnt/cifs_share  cifs  credentials=/etc/cifs_credentials,uid=1000,gid=1000  0 0" | sudo tee -a /etc/fstab
   ```
4. **Validation Test**: Instruct the local service controller to parse your adjustments and mount all lines automatically:
   ```bash
   sudo mount -a
   ```

📌 **Critical Netdev Note**: If network interfaces drop temporarily during low-level startup loops, boot sequences can freeze waiting for network resources. To prevent this, consider appending the `_netdev` option string alongside standard flags inside `/etc/fstab` to instruct the kernel to delay disk mounting until network layers cycle fully online.

---

## 🔎 Comprehensive Verification Check
Confirm that your persistent mapping rules match up across all operational tables by running this diagnostic evaluation check:

- [ ] **Verify Core Mount Layout Matrices**: Ensure entries register under active system files:
  ```bash
  mount | grep -E 'nfs|cifs'
  ```
- [ ] **Audit Registry Declarations**: Read the bottom layout paths of the system ledger to guarantee clean syntax structures:
  ```bash
  cat /etc/fstab | grep -v '^#'
  ```

---

## 🏁 Conclusion
During this lab session, you developed crucial distributed storage engineering capabilities, including:
- Deploying foundational client packages (`nfs-utils` and `cifs-utils`).
- Running network discovery processes across remote servers.
- Guarding authentication boundaries with restrictive file access profiles (`chmod 600`).
- Engineering persistent, automated storage configurations using local mount parameters.

These capabilities are critical baseline requirements for building shared storage volumes, maintaining data sync points across development structures, and configuring persistent, multi-node storage states across enterprise applications and orchestration clusters like OpenShift.

---

## 🚀 Next Steps
- Automate network resource mapping on-demand via mount tracking utilities like **autofs**.
- Learn to build out distribution servers by modifying independent filesystem storage rules inside `/etc/exports`.
- Configure an interactive local environment from scratch by deploying an independent **Samba** daemon workspace.
