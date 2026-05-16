# Installing and Updating Software Packages

This repository contains a hands-on lab focused on enterprise-level Linux package management. You will master registering system streams via Red Hat Subscription Manager (RHSM), governing repository matrices, handling core lifecycles using the `dnf` utility engine, and managing advanced modular stream profiles.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Register a system subscription layout using Red Hat Subscription Manager (RHSM).
- Control package sources by enabling and disabling software repositories.
- Perform software deployments, clean removals, and system-wide upgrades via `dnf`.
- Install bundled solution clusters via package groups and optimize runtimes with application modules.

## 📋 Prerequisites
- A Red Hat Enterprise Linux (RHEL) 8/9 system (Fedora or CentOS Stream are acceptable open-source alternatives).
- Terminal access featuring elevated `sudo` system administration privileges.
- Active internet connectivity to reach upstream download mirrors.

---

## 🛠️ Lab Tasks

### Task 1: Registering a System Subscription
**Objective**: Connect your system node to Red Hat's content delivery networks to unlock official software channels.

1. Open your terminal window and verify the registration envelope status:
   ```bash
   sudo subscription-manager status
   ```
   *Expected Status Trace:* Returns an active entitlement ledger or explicitly alerts that `"This system is not yet registered."`

2. If using an authentic RHEL node, authenticate and hook available entitlement pools to your architecture:
   ```bash
   sudo subscription-manager register --username=<your_username> --password=<your_password> --auto-attach
   ```
   *(Note: Skip this command step entirely if your test environment is running on Fedora or CentOS Stream).*

💡 **Troubleshooting**: If authorization steps timeout, execute domain trace audits using network tools to verify internet mapping paths, and confirm your Red Hat Portal credential strings are correct.

---

### Task 2: Enabling and Disabling Repositories
**Objective**: Regulate software channel visibility trackers inside your package manager mapping arrays.

1. Generate a total inventory map tracing every available channel layout configuration on the system:
   ```bash
   sudo dnf repolist all
   ```
2. Activate a restricted or supplementary software repository channel matching a clear token name:
   ```bash
   sudo dnf config-manager --enable <repo_name>
   ```
   *Practical Example (Deploying and turning on Extra Packages for Enterprise Linux - EPEL):*
   ```bash
   sudo dnf install epel-release -y
   sudo dnf config-manager --enable epel
   ```
3. Remove an active tracking channel out of target evaluation pathways to freeze its updates:
   ```bash
   sudo dnf config-manager --disable <repo_name>
   ```

---

### Task 3: Installing, Removing, and Updating Packages
**Objective**: Execute explicit, non-interactive software lifecycle maintenance.

1. **Deploy Software**: Install the Apache HTTP Server daemon package, passing automatic confirmation flags:
   ```bash
   sudo dnf install -y httpd
   ```
2. **Purge Software**: Cleanly uninstall the web server asset package from your local storage system:
   ```bash
   sudo dnf remove -y httpd
   ```
3. **Upgrade Core Files**: Synchronize metadata mirrors and bring every deployed package asset up to the latest release version:
   ```bash
   sudo dnf update -y
   ```

---

### Task 4: Working with Package Groups and Modules
**Objective**: Administer monolithic developer suite environments and isolate software versions using application streams (AppStream).

1. List available composite development clusters compiled inside active repository networks:
   ```bash
   sudo dnf group list
   ```
2. Deploy an entire meta-bundle grouping (e.g., compilers, tools, system utilities) in a single execution loop:
   ```bash
   sudo dnf group install -y "Development Tools"
   ```
3. Output the grid array matrix displaying available software runtime version streams across the network:
   ```bash
   sudo dnf module list
   ```
4. Reset a version target baseline to lock onto an explicit microservice stream configuration (e.g., NodeJS 18), then execute the base deployment step:
   ```bash
   sudo dnf module enable -y nodejs:18
   sudo dnf install -y nodejs
   ```

---

## 🏁 Conclusion
During this lab session, you developed crucial system engineering provisioning capabilities, including:
- Attaching structural subscription licenses via RHSM frameworks.
- Regulating channel visibility settings maps with configuration utilities.
- Handling atomic software lifecycles using `dnf` arguments.
- Instantiating development profiles via modular version streams.

These lifecycle capabilities are essential baseline prerequisites for provisioning robust system nodes, managing platform updates, and preparing production cluster hosts driving container engines like Podman or OpenShift.

---

## 🚀 Next Steps
- Audit your package transaction history index and learn how to rollback system modifications by evaluating `dnf history`.
- Deepen your low-level software package knowledge by learning to inspect standalone binary archives with `rpm`.
