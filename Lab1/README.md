# Introduction to Red Hat Enterprise Linux (RHEL) 

This repository contains a hands-on lab designed to introduce the fundamentals of open-source software, Linux distributions, and the core characteristics and subscription models of Red Hat Enterprise Linux (RHEL).

---

## 🎯 Objectives
By the end of this lab, you will:
- Understand the fundamentals of open-source software.
- Learn about Linux distributions and their significance.
- Explore Red Hat Enterprise Linux (RHEL) characteristics and its subscription model.

## 📋 Prerequisites
- A system with internet access.
- A terminal or command-line interface (CLI).
- Basic familiarity with command-line operations.

---

## 🛠️ Lab Guide

### Task 1: Understanding Open Source and Linux

#### Subtask 1.1: Define Open Source
**Objective**: Learn what open-source software is and its key principles.

1. Open your terminal.
2. Run the following command to fetch the Open Source Initiative (OSI) definition:
   ```bash
   curl -s https://opensource.org | grep -A5 "Open Source Definition"
   ```

* **Expected Output**: Displays the Open Source Definition summary.
* **Key Concepts**:
  - **Free Redistribution**: No restrictions on selling or giving away software.
  - **Source Code Availability**: Must include source code.
  - **Derived Works**: Modifications and derived works must be allowed.
* **Troubleshooting**: If `curl` is not installed, install it using:
  ```bash
  sudo dnf install curl -y  # For RHEL-based systems
  ```

#### Subtask 1.2: Introduction to Linux
**Objective**: Understand Linux as an open-source operating system.

1. Check the kernel version (core of Linux) using:
   ```bash
   uname -r
   ```

* **Expected Output**: Displays the Linux kernel version (e.g., `5.14.0-70.el9.x86_64`).
* **Key Concepts**:
  - **Kernel**: Manages hardware resources.
  - **GNU Tools**: Provides essential utilities (`ls`, `grep`, `bash`).

---

### Task 2: Exploring Linux Distributions

#### Subtask 2.1: List Popular Linux Distributions
**Objective**: Identify major Linux distributions and their use cases.

1. Research common distributions:
   - **Debian**: Community-driven, stable.
   - **Ubuntu**: User-friendly, based on Debian.
   - **RHEL**: Enterprise-focused, subscription-based.
2. Check your distribution (if using Linux):
   ```bash
   cat /etc/os-release
   ```

* **Expected Output**: Displays OS name, version, and ID (e.g., RHEL 9.0).

#### Subtask 2.2: Compare Distributions
**Objective**: Understand differences between RHEL and others.


| Feature | RHEL | Ubuntu |
| :--- | :--- | :--- |
| **Support** | Paid | Community/Paid |
| **Package Manager** | `dnf` | `apt` |
| **Release Cycle** | 5-10 years | 6 months (LTS versions longer) |

---

### Task 3: RHEL Characteristics and Subscription

#### Subtask 3.1: RHEL Features
**Objective**: Learn key RHEL features.

1. **Security**: SELinux (Security-Enhanced Linux) is enabled by default. Check status:
   ```bash
   sestatus
   ```
   - **Expected Output**: Shows SELinux status (e.g., `enforcing`).
2. **Stability**: Long-term support (10+ years).

#### Subtask 3.2: RHEL Subscription Model
**Objective**: Understand how RHEL subscriptions work.

1. Register a system (requires Red Hat account):
   ```bash
   sudo subscription-manager register --username <your_username> --password <your_password>
   ```
2. Attach a subscription:
   ```bash
   sudo subscription-manager attach --auto
   ```
3. Verify the registration:
   ```bash
   sudo subscription-manager list --consumed
   ```

* **Expected Output**: Lists active subscriptions.
* **Troubleshooting**: If `subscription-manager` is missing, install it:
  ```bash
  sudo dnf install subscription-manager -y
  ```

---

## 🏁 Conclusion
In this lab, you:
- Defined open-source principles and Linux.
- Explored major Linux distributions and compared them.
- Learned RHEL’s security features and subscription model.

## 🚀 Next Steps
- Practice commands on a live RHEL system.
- Explore the Red Hat Developer Program for free resources.

---

> ⚠️ **Note**: All commands are tested on RHEL 9. Replace `<your_username>` and `<your_password>` with actual Red Hat credentials. For educational purposes, use the [Red Hat Developer Subscription](https://redhat.com) for free access.
