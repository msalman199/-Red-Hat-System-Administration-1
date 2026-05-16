# Securing the System with SELinux Basics

This repository contains a hands-on lab focused on Security-Enhanced Linux (SELinux) administration. You will learn to audit Mandatory Access Control (MAC) labels, modify resource safety contexts temporarily and persistently, deconstruct Access Vector Cache (AVC) violation events within system security ledgers, and resolve complex application privilege denials.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Comprehend the architecture of SELinux security context strings and their role in system security.
- View and evaluate existing security contexts using the `-Z` diagnostic flag across file system entities.
- Modify resource security contexts temporarily using `chcon` and permanently using `semanage`.
- Query, interpret, and troubleshoot Access Vector Cache (AVC) denials within system logs.

## 📋 Prerequisites
- A Linux operating system featuring an active SELinux enforcement engine (Red Hat Enterprise Linux, CentOS Stream, or Fedora recommended).
- Terminal access featuring elevated `sudo` system administration privileges.
- Basic familiarity running system command-line interface (CLI) commands.

---

## ⚙️ Setup Requirements
1. Launch an active terminal shell session workspace.
2. Interrogate the kernel security configuration space to verify that the MAC sub-engine is active:
   ```bash
   sestatus
   ```
   *(Expected Output: The `SELinux status` parameter must explicitly reflect an `enabled` state).*
3. Deploy the core auditing console tools, system policy utility binaries, and log analysis engines:
   ```bash
   sudo dnf install -y setroubleshoot setools-console policycoreutils-python-utils
   ```

---

## 🛠️ Lab Tasks

### Task 1: Viewing SELinux Contexts with ls -Z
**Objective**: Interrogate system objects to view and deconstruct security labels.

#### Subtask 1.1: View File and Directory Contexts
1. Spin up an unprivileged test file template inside volatile storage:
   ```bash
   touch /tmp/testfile.txt
   ```
2. Audit the security properties layer mapped onto the new resource:
   ```bash
   ls -Z /tmp/testfile.txt
   ```
   *Expected Output Trace:*
   ```text
   unconfined_u:object_r:user_tmp_t:s0 /tmp/testfile.txt
   ```
3. Read the standalone directory context mapping applied directly to the root volatile folder structure:
   ```bash
   ls -Zd /tmp
   ```

#### Subtask 1.2: Understand Context Components
The security context layout string is divided into four distinct colon-separated fields:
*   **User**: `unconfined_u` (Identifies the SELinux user account bound to the resource layer)
*   **Role**: `object_r` (Defines structural roles; objects/files are typically assigned `object_r`)
*   **Type**: `user_tmp_t` (The domain layout definition driving primary Type Enforcement logic)
*   **Level**: `s0` (Indicates Multi-Level Security / Multi-Category Security stratification annotations)

📌 **Key Concept**: The **Type** field is the critical component used by the kernel to make access control decisions. If a process type does not have an explicit rule allowing access to a target file type, the operation is blocked.

---

### Task 2: Changing Contexts with chcon
**Objective**: Manually alter the context type mapping associated with filesystem resources.

#### Subtask 2.1: Change File Context Temporarily
1. Build a custom directory block directly at the root of the file system tree:
   ```bash
   sudo mkdir /web
   ```
2. Check the default context types inherited automatically from parent templates:
   ```bash
   ls -Zd /web
   ```
3. Explicitly swap the target context type profile map over to align with web server system expectations:
   ```bash
   sudo chcon -t httpd_sys_content_t /web
   ```
4. Verify that the runtime mapping adjustment took effect immediately:
   ```bash
   ls -Zd /web
   ```
   *Expected Outcome:* The Type dimension segment now reflects `httpd_sys_content_t`.

#### Subtask 2.2: Restore Default Context
1. Instruct the system policy tracker to evaluate the path and wipe out manual modifications, resetting the directory to system defaults:
   ```bash
   sudo restorecon -v /web
   ```
2. Re-verify the directory state to confirm it returned to its original default context:
   ```bash
   ls -Zd /web
   ```

---

### Task 3: Interpreting Audit Logs and AVC Denials
**Objective**: Intentional generation, tracking, and remediation of Access Vector Cache (AVC) violations.

#### Subtask 3.1: Generate an AVC Denial
1. Build a mock web document structure tree:
   ```bash
   sudo mkdir -p /web/html
   sudo touch /web/html/index.html
   ```
2. Intentionally inject an invalid, mismatched context type (`user_home_t`) onto the index file to trigger a policy conflict:
   ```bash
   sudo chcon -t user_home_t /web/html/index.html
   ```
3. Fire up the local Apache HTTP Server daemon:
   ```bash
   sudo systemctl start httpd
   ```
4. Attempt to access the web asset via a local network loop to trigger a security block:
   ```bash
   curl http://localhost/html/index.html
   ```
   *Expected Outcome:* The request returns an HTTP `403 Forbidden` error because the web server daemon type is denied access to the home directory type label.

#### Subtask 3.2: Analyze the Denial
1. Sift through system logs to pull out the raw, low-level AVC denial tracking block events recorded recently:
   ```bash
   sudo ausearch -m avc -ts recent
   ```
2. Generate an easily readable, structured breakdown detailing the exact cause of the fault along with automated suggestions:
   ```bash
   sudo sealert -a /var/log/audit/audit.log
   ```
   *Key Information Fields to Isolate:*
   - **Source Context (scontext)**: The process domain trying to execute the action (e.g., `httpd_t`).
   - **Target Context (tcontext)**: The resource label receiving the request (e.g., `user_home_t`).
   - **Denied Permission**: The explicit action blocked by the kernel policy ruleset matrix (e.g., `read`).

#### Subtask 3.3: Resolve the Denial
1. Overwrite the mismatched label, updating it to the correct type authorized for web data delivery operations:
   ```bash
   sudo chcon -t httpd_sys_content_t /web/html/index.html
   ```
2. Re-test the local network transport connection loop to verify clean data retrieval:
   ```bash
   curl http://localhost/html/index.html
   ```

---

## 💡 Troubleshooting Tips

*   **Sealert Execution Errors**: If your diagnostic alert utility fails to parse records, ensure the supporting background daemon thread is active:
    ```bash
    sudo systemctl start setroubleshoot
    ```
*   **Persistent Configuration Overwrites**: Real-world operations should avoid `chcon` because relabeling tasks wipe out its manual definitions. Apply changes permanently using policy modification tools:
    ```bash
    sudo semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?"
    sudo restorecon -Rv /web
    ```
*   **Isolation Debugging Controls**: If an ambiguous error makes it unclear whether SELinux or basic file permissions are causing a failure, shift the engine temporarily into a log-only mode:
    ```bash
    sudo setenforce 0
    ```
    *(Note: Re-activate standard active production enforcement rules immediately after testing by running `sudo setenforce 1`).*

---

## 🏁 Conclusion
During this lab session, you developed crucial enterprise security administration capabilities, including:
- Viewing and interpreting four-part context strings using `ls -Z`.
- Modifying resource safety boundaries temporarily using `chcon` and permanently using `semanage`.
- Troubleshooting system blockages by analyzing AVC denial traces using `ausearch` and `sealert`.

These skills are vital baseline prerequisites for enforcing a strong security posture, debugging server daemon configuration access faults, and hardening enterprise platforms and container runtimes (Podman) inside managed frameworks like OpenShift.

---

## 🚀 Next Steps
- Dig into functional boolean policy variables to alter runtime software rules on-the-fly using `getsebool` and `setsebool`.
- Research the construction patterns of custom policy modules to author localized rule maps using `audit2allow`.
