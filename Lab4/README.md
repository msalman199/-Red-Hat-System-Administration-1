# Accessing Local Help and Documentation

This repository contains a hands-on lab focused on navigating built-in Linux documentation tools, discovering command functionalities, and extracting package metadata directly from the command-line interface (CLI).

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Utilize local help systems to troubleshoot and learn Linux tools without external internet access.
- Navigate hierarchical manual pages (`man`) and info nodes (`info`).
- Extract immediate syntax hints using command-line help flags (`--help`).
- Explore supplementary documentation resources stored inside `/usr/share/doc`.
- Discover unfamiliar tools using keyword matching with `whatis` and `apropos`.
- Examine installed package details using `dnf` or `yum` metadata inquiries.

## 📋 Prerequisites
- A Linux operating system (Red Hat Enterprise Linux, Fedora, or CentOS recommended).
- Terminal access with standard user privileges.
- Basic familiarity with CLI execution patterns.
- `podman` installed locally on the system (required for container task steps).

---

## 🛠️ Lab Tasks

### Task 1: Using Manual Pages (man)
**Objective**: Access and search exhaustive core system command reference documents.

1. Open your terminal and display the utility documentation for directory listings:
   ```bash
   man ls
   ```
2. **Navigation Basics**:
   - Press `Spacebar` to page down.
   - Press `b` to page up.
   - Press `/` followed by a keyword (e.g., `/color`) to search forward.
   - Press `q` to exit the viewer.
3. Access specific documentation sections (e.g., system configuration files format rather than the executable command):
   ```bash
   man 5 passwd
   ```

💡 **Troubleshooting**: If your system returns a missing tool error, populate your manual databases by executing `sudo dnf install man-db -y`.

---

### Task 2: Using Info Pages (info)
**Objective**: Read complex, hyperlinked, GNU-style structured documentation.

1. Launch the documentation interface for core utility structures:
   ```bash
   info coreutils
   ```
2. **Navigation Basics**:
   - Press `Enter` while pointing at a menu item to follow its link.
   - Press `n` to jump to the **Next** structural node.
   - Press `p` to return to the **Previous** structural node.
   - Press `u` to move **Up** exactly one layout level hierarchy.
   - Press `q` to quit out of the application.

---

### Task 3: Using the --help Flag
**Objective**: Quickly inspect contextual options and summary usage syntax.

1. Fetch quick, non-interactive help pages for standard utilities:
   ```bash
   ls --help
   ```
2. Inspect help screens for structural subcommands like container runtime managers:
   ```bash
   podman --help
   podman run --help
   ```

---

### Task 4: Exploring /usr/share/doc
**Objective**: Find supplementary vendor readmes, samples, and text guides.

1. List the available package documentation catalogs compiled on your system disk:
   ```bash
   ls /usr/share/doc
   ```
2. Examine deep textual breakdowns for specific shells (such as Bash) using a file pager:
   ```bash
   less /usr/share/doc/bash/README
   ```

---

### Task 5: Using whatis and apropos
**Objective**: Identify commands based on keyword definitions and functional targets.

1. Query short, single-line summaries of tool capabilities:
   ```bash
   whatis ls
   whatis podman
   ```
2. Locate unknown binaries by querying related functional strings:
   ```bash
   apropos "list directory"
   apropos container
   ```

---

### Task 6: Examining Package Information
**Objective**: Investigate packages, dependencies, and change flags through your package manager.

1. Confirm whether a specific program package is currently deployed on the system filesystem:
   ```bash
   dnf list installed podman
   ```
2. Retrieve version metadata, release streams, architectures, and descriptions:
   ```bash
   dnf info podman
   ```
3. Read historical maintenance adjustments tracking system modifications:
   ```bash
   dnf changelog podman
   ```

---

## 🏁 Conclusion
During this lab session, you developed systematic information retrieval skills, including:
- Accessing comprehensive references via `man` and `info`.
- Utilizing structural flags for localized usage summaries.
- Exploring raw system documentation files within vendor folders.
- Using targeted lookup indexing utilities like `whatis` and `apropos`.
- Querying application properties using native `dnf` functions.

---

## 🚀 Next Steps
- Incorporate these discovery commands into your daily workflow to build muscle memory.
- Pipe massive documentation output blocks into searching patterns to pinpoint terms quickly (e.g., `man ls | grep -i hidden`).
- Explore the organizational structures of manual divisions by typing `man man`.

---

## 📊 Final Validation Checklist
Test your newly acquired troubleshooting capabilities by answering these questions:
- [ ] Can you find all commands on your system matching the keyword **"network"**?
- [ ] Can you identify the exact function of the `-a` flag for the `ls` command using a manual lookup?
- [ ] Can you view the installation timestamp of `podman` on your machine using package metadata tools?
