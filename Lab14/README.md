# Accessing and Managing Linux Filesystems

This repository contains a hands-on lab focused on storage engineering and file system layout governance. You will learn to audit physical block devices, orchestrate transient and permanent mount points via critical configuration targets (`/etc/fstab`), and construct dynamic, flexible storage layers utilizing **Logical Volume Manager (LVM)** architectures.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Inspect block devices and extract identifiers using `lsblk`, `fdisk`, and `blkid`.
- Mount and unmount file systems securely across manual system directory trees.
- Configure deterministic, persistent data mount maps inside the system configuration vault (`/etc/fstab`).
- Architect, manage, and dynamically scale storage spaces via Logical Volume Manager (LVM) pools.

## 📋 Prerequisites
- A Linux operating system (Red Hat Enterprise Linux, CentOS Stream, or Fedora recommended).
- Terminal access featuring elevated `sudo` system administration privileges.
- Basic familiarity running system command-line interface (CLI) commands.
- At least one additional unformatted, unpartitioned raw block storage disk (e.g., `/dev/sdb` or `/dev/nvme1n1`) for LVM construction segments.

---

## 🛠️ Lab Tasks

### Task 1: Inspecting Block Devices
**Objective**: Inventory your hardware topology and identify active file system types.

1. Open your terminal window and output a structured tree tracking all storage targets:
   ```bash
   lsblk
   ```
2. Run an enriched format query to expose underlying file system profiles and explicit signature hashes:
   ```bash
   lsblk -f
   ```
3. Read the complete storage disk mapping layout across every attached hard disk device:
   ```bash
   sudo fdisk -l
   ```
   *(To audit one isolated disk target independently, append its system path, for example: `sudo fdisk -l /dev/sda`)*
4. Interrogate block layers directly to sweep and gather exact globally unique UUID attributes:
   ```bash
   sudo blkid
   ```

---

### Task 2: Mounting and Unmounting Filesystems
**Objective**: Bind block devices onto local directory branches to access raw filesystems.

1. **Mount Temporarily**: Construct an anchor target mount point directory inside the volatile system tree:
   ```bash
   sudo mkdir /mnt/mydisk
   ```
2. Bind an existing operational block storage partition over onto that target folder:
   ```bash
   sudo mount /dev/sdX1 /mnt/mydisk
   ```
   *(Be sure to replace `/dev/sdX1` with your actual target partition block identity index).*
3. Verify that the partition storage dimension is tracking successfully:
   ```bash
   df -h /mnt/mydisk
   ```
4. **Unmount Storage**: Safely detach the active storage block layer out of the system directory path:
   ```bash
   sudo umount /mnt/mydisk
   ```
   Confirm clean detachment from active files arrays by running: `df -h`.

---

### Task 3: Configuring Persistent Mounts (/etc/fstab)
**Objective**: Automate file system restoration parameters so storage targets load reliably at boot.

1. Isolate the exact, permanent signature token binding hash tracking your target storage block partition:
   ```bash
   sudo blkid /dev/sdX1
   ```
2. Open the system's central storage boot mount registry inside your text editor:
   ```bash
   sudo nano /etc/fstab
   ```
3. Append a persistent mounting instructions string entry to the bottom of the ledger:
   ```text
   UUID=your-uuid-here  /mnt/mydisk  ext4  defaults  0  2
   ```
4. **Validation Test**: Instruct the operating system logic engine to evaluate and try loading all statements mapped inside the configuration file immediately:
   ```bash
   sudo mount -a
   ```
   *Expected Outcome:* Execution should return cleanly with zero error outputs. Run `df -h` to verify storage mounting states.

⚠️ **Critical Warning**: Always maintain an identical backup duplicate copy of `/etc/fstab` before manual manipulation. Bad configuration statements can cause severe boot failures.

---

### Task 4: Managing LVM Volumes
**Objective**: Abstract hard storage elements into dynamic, elastic, resizable virtual pools.

#### Subtask 4.1: Create an LVM Volume
1. Initialize a raw block storage disk device layer, marking it ready for LVM tracking management:
   ```bash
   sudo pvcreate /dev/sdX
   ```
2. Combine one or more physical paths together to create an elastic Volume Group container called `myvg`:
   ```bash
   sudo vgcreate myvg /dev/sdX
   ```
3. Carve out a distinct virtual partition space called `mylv` with a strict initial dimension layout allocation:
   ```bash
   sudo lvcreate -L 5G -n mylv myvg
   ```
4. Layer a clean file system onto the logical unit volume structure and mount it online:
   ```bash
   sudo mkfs.ext4 /dev/myvg/mylv
   sudo mkdir /mnt/lvm
   sudo mount /dev/myvg/mylv /mnt/lvm
   ```

#### Subtask 4.2: Extend an LVM Volume
1. Dynamically append supplementary allocation blocks directly onto your virtual runtime target partition:
   ```bash
   sudo lvextend -L +2G /dev/myvg/mylv
   ```
2. Force the live file system framework tracking the container block to upscale to fill the new dimension:
   ```bash
   sudo resize2fs /dev/myvg/mylv
   ```
3. Evaluate system scaling metrics immediately to confirm success:
   ```bash
   df -h /mnt/lvm
   ```
   *Expected Output:* The usable space on the target directory mount reflects an automated increase of 2GB.

---

## 💡 Troubleshooting Tips

* **Mount Request Denial**: If disk mount bindings crash, check the kernel ring buffer logs immediately to trace low-level driver alerts via `dmesg`.
* **LVM Structuring Failure**: Interrogate the component states of your abstraction modules using status diagnostics: `pvdisplay`, `vgdisplay`, and `lvdisplay`.
* **Busy Device Unmount Rejection**: If `umount` fields throw a device busy warning error, ensure your current terminal session directory path or system tools are not actively nested inside or reading from that storage path.

---

## 🏁 Conclusion
During this lab session, you developed foundational platform infrastructure and storage optimization skills, including:
- Mapping storage architectures using `lsblk` and metadata lookup registries.
- Establishing standard temporary mounting bindings and permanent boot parameters.
- Engineering virtual storage layouts through LVM setups.
- Upscaling live file storage blocks dynamically.

These storage mechanics serve as critical base criteria for configuring large database nodes, maintaining application file health, and staging local hosts to mount external storage shares inside cloud container platforms like OpenShift.

---

## 🚀 Next Steps
- Reinforce your understanding by experimenting with alternative file system layouts like XFS (using `mkfs.xfs` and its corresponding scaling agent `xfs_growfs`).
- Investigate high-utility advanced storage techniques like **LVM Snapshotting** to freeze system states for clean file backups.
