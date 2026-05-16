# Managing Services with systemd

This repository contains a hands-on lab focused on managing system daemons, controlling application boot behaviors, inspecting unit configuration dependencies, and querying persistent system logs using the `systemd` initialization framework.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Control and monitor runtime services using the `systemctl` utility.
- Audit service execution states, initialize startups, force stops, and trigger clean reloads.
- Configure automatic initialization states at machine boot time.
- Inspect raw service configuration unit files and map internal dependencies.
- Isolate and filter structured system journal log records via `journalctl`.

## 📋 Prerequisites
- A Linux operating system initialized via `systemd` (e.g., RHEL, Fedora, CentOS Stream, or Ubuntu).
- Terminal access featuring elevated `sudo` system administration privileges.
- Basic familiarity running system command-line interface (CLI) commands.

---

## 🛠️ Lab Tasks

### Task 1: Check Service Status
**Objective**: Interrogate the system initialization controller to evaluate runtime service states.

1. Open your terminal window.
2. Generate an inventory list tracking all active, running background processes:
   ```bash
   systemctl list-units --type=service --state=running
   ```
3. Audit the operational health and historical logs of the secure shell (`sshd`) system daemon:
   ```bash
   systemctl status sshd
   ```
   *Expected Output:* A structured tracking sheet displaying process tracking trees (Cgroups), activation states, boot mapping declarations, and trailing log messages.

💡 **Troubleshooting**: If your target platform lacks the test engine service, install it using your system package manager:
```bash
sudo dnf install openssh-server -y   # For RHEL / Fedora / CentOS Stream
sudo apt install openssh-server -y   # For Ubuntu / Debian
```

---

### Task 2: Start, Stop, and Restart Services
**Objective**: Control operational execution states of running system daemons.

1. **Stop a Service**: Terminate execution threads of the target daemon process:
   ```bash
   sudo systemctl stop sshd
   ```
   Verify the successful termination using the status module:
   ```bash
   systemctl status sshd
   ```
   *Expected Output State:* `Active: inactive (dead)`

2. **Start a Service**: Initialize execution frameworks for the stopped daemon process:
   ```bash
   sudo systemctl start sshd
   ```
   Verify execution tracking states:
   ```bash
   systemctl status sshd
   ```
   *Expected Output State:* `Active: active (running)`

3. **Restart a Service**: Trigger an automated, rapid teardown and immediate reconstruction cycle:
   ```bash
   sudo systemctl restart sshd
   ```

---

### Task 3: Enable and Disable Services at Boot
**Objective**: Define persistent startup targets tracking physical machine initialization loops.

1. **Enable a Service**: Register configuration scripts to invoke the service automatically whenever the machine boots:
   ```bash
   sudo systemctl enable sshd
   ```
   *Expected Output Trace:* System creates target symbolic reference points link structures linking to `/etc/systemd/system/`.

2. **Disable a Service**: Strip out boot execution flags, keeping the application static until manual intervention calls it:
   ```bash
   sudo systemctl disable sshd
   ```
   *Expected Output Trace:* System removes relevant symbolic links matching the boot initialization chains.

---

### Task 4: Inspect Unit Files
**Objective**: Review declarative configuration parameters driving target service definitions.

1. Print out the raw, underlying unit profile configuration blueprint mapping directly onto the target program:
   ```bash
   systemctl cat sshd
   ```
2. Build an active dependency directory tree listing all supporting services demanded by the daemon target:
   ```bash
   systemctl list-dependencies sshd
   ```

---

### Task 5: View Logs with journalctl
**Objective**: Retrieve binary log entries compiled by the system logger daemon.

1. **View Service Logs**: Extract chronological logs mapped exclusively to a specific service container:
   ```bash
   sudo journalctl -u sshd
   ```
2. **Filter Logs by Time**: Constrain huge text reads to isolated temporal fields:
   ```bash
   sudo journalctl -u sshd --since "1 hour ago"
   ```
3. **Follow Logs Live**: Stream newly generated log rows dynamically onto your active shell interface:
   ```bash
   sudo journalctl -u sshd -f
   ```
   *(Terminate the live stream interface tracking loop at any point by hitting `Ctrl + C`)*

---

## 🏁 Conclusion
During this lab session, you developed crucial service orchestration capabilities, including:
- Checking, starting, stopping, and restarting services via `systemctl`.
- Altering server persistence behaviors relative to system boots.
- Deconstructing configurations via declarative unit file views.
- Extracting application debug records via `journalctl`.

These diagnostic capabilities form the baseline framework for maintaining high service availability, adjusting production configurations, and parsing errors across enterprise and cloud-native systems.

---

## 🚀 Additional Practice (Optional)
- Build a prototype custom `.service` unit text configuration file inside `/etc/systemd/system/` and govern it using `systemctl`.
- Profile your system optimization performance speeds by running `systemd-analyze`.
- Protect critical processes from rogue operations by applying administrative blocks via `systemctl mask`.
