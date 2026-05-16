# Analyzing and Storing Logs

This repository contains a hands-on lab focused on Linux log management. You will learn to navigate the system log directory, leverage powerful `journalctl` filtering rules, construct automated log maintenance policies using `logrotate`, and parse complex text data pools via `grep` and `awk`.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Locate, view, and accurately interpret system logs to troubleshoot anomalies.
- Explore and audit the historical text structures inside the `/var/log` directory.
- Apply advanced systemd journal queries using time, service, and diagnostic filters.
- Understand, design, and validate `logrotate` blueprints for structural log management.
- Isolate and filter targeted log streams using analytical string scripts (`grep` / `awk`).

## 📋 Prerequisites
- A Linux operating system (Red Hat Enterprise Linux, CentOS Stream, or Fedora recommended).
- Terminal access featuring elevated `sudo` system administration privileges.
- Basic familiarity running foundational command-line interface (CLI) commands.
- `podman` installed locally on the system (required for container log testing scenarios).

---

## 🛠️ Lab Tasks

### Task 1: Exploring /var/log Files
**Objective**: Learn standard system log directory layouts and data structures.

1. Open your terminal window and inspect the root logging repository folder:
   ```bash
   ls -l /var/log
   ```
   *Expected Items:* Directory tracking targets like `messages`, `secure`, `cron`, or subfolders tracking web servers.
2. View global, non-authentication system-wide processing messages:
   ```bash
   sudo cat /var/log/messages
   ```
3. Audit security events, privilege elevations, and remote access authentication trials:
   ```bash
   sudo cat /var/log/secure
   ```

💡 **Troubleshooting**: File names differ across distributions. If your system throws a missing file path error, consult platform variations (e.g., Ubuntu uses `/var/log/syslog` instead of `messages`, and `/var/log/auth.log` instead of `secure`).

---

### Task 2: Using journalctl Filters
**Objective**: Query binary, indexed, and structured systemd runtime journals.

1. Output the total, unified active system log book file:
   ```bash
   sudo journalctl
   ```
2. Constrain structural query lookups to clear temporal boundaries using timestamp fields:
   ```bash
   sudo journalctl --since "2023-01-01" --until "2023-01-02"
   ```
3. Isolate log captures exclusively tracking a particular service entity (e.g., SSH daemon):
   ```bash
   sudo journalctl -u sshd
   ```
4. Stream incoming log notifications live directly onto your active terminal shell:
   ```bash
   sudo journalctl -f
   ```
   *(Terminate the live execution view tracker at any point by striking `Ctrl + C`)*

---

### Task 3: Understanding logrotate
**Objective**: Build automated system data storage cleanup and rotation jobs.

1. Inspect the global operating configuration file and system module drop-in directories:
   ```bash
   cat /etc/logrotate.conf
   ls /etc/logrotate.d/
   ```
2. Design a prototype localized log rotation policy profile script:
   ```bash
   sudo nano /etc/logrotate.d/mylogs
   ```
3. Insert the following block parameter logic rule map into your text workspace:
   ```text
   /var/log/mylog.log {
       daily
       rotate 7
       compress
       missingok
       notifempty
   }
   ```
4. **Dry-Run Validation**: Test the text translation sequence inside the utility engine without making real alterations:
   ```bash
   sudo logrotate -d /etc/logrotate.d/mylogs
   ```

💡 **Troubleshooting**: The debug flag `-d` skips real executions. To instantly compel the rotation of your data files on disk for live troubleshooting, pass the force flag: `sudo logrotate -f /etc/logrotate.d/mylogs`.

---

### Task 4: Searching Logs with grep and awk
**Objective**: Extract targeted, granular context strings from unstructured text logs.

1. Search raw system logs to pinpoint instances containing explicit errors:
   ```bash
   sudo grep "error" /var/log/messages
   ```
2. Execute a case-insensitive lookup tracking failure strings within secure logs:
   ```bash
   sudo grep -i "fail" /var/log/secure
   ```
3. Generate a pure metric numerical count calculating occurrences of targeted strings:
   ```bash
   sudo grep -c "authentication failure" /var/log/secure
   ```
4. Construct an advanced positional pattern matching routine to extract custom metadata (e.g., tracking failed login times and IP points):
   ```bash
   sudo awk '/Failed password/ {print \$1, \$2, \$3, \$9, \$11}' /var/log/secure
   ```
5. Interrogate and inspect active application log pools inside isolated container engines (Podman):
   ```bash
   podman logs <container_id> | grep -i error
   ```

---

## 🏁 Conclusion
During this lab session, you developed crucial production system monitoring and analytics skills, including:
- Mapping file path arrays across system logging directories.
- Applying rich index filters across structural `systemd` storage databases.
- Automating operational file lifecycles to protect server disks from filled partitions.
- Parsing text formats via advanced token filters (`grep` / `awk`).

These analytical skills are mandatory primitives for tracking server environments, tracing root causes, auditing compliance parameters, and managing performance data across cloud-native application stacks like OpenShift.

---

## 🚀 Next Steps
- Profile your persistent local tracking data constraints by auditing current disk usage parameters:
  ```bash
  sudo journalctl --disk-usage
  ```
- Explore alternative structured schema formats from your system journal tracker by outputting raw JSON objects: `sudo journalctl -o json`.
- Advance your script capabilities by experimenting with arithmetic evaluation statements using native `awk`.

---

## 🧹 Cleanup
Maintain a clean server environment by discarding your evaluation prototype configuration file:
```bash
sudo rm -f /etc/logrotate.d/mylogs
```
