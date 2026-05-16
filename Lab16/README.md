# Monitoring System Performance and Resource Usage

This repository contains a hands-on lab focused on real-time systems diagnostics and performance engineering. You will learn to monitor system vital signs (CPU, Memory, Disk, Network) using open-source tools, isolate high-resource processes, trace performance bottlenecks, and analyze container footprints using `podman`.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Monitor and interpret global CPU, memory, storage disk, and network interface utilization metrics.
- Isolate the precise footprint and impact of individual running processes on hardware assets.
- Target, profile, and troubleshoot resource exhaustion and systemic bottleneck anomalies.
- Analyze containerized infrastructure resource workloads via runtime metrics engine components.

## 📋 Prerequisites
- A Linux operating system (Red Hat Enterprise Linux, CentOS Stream, or Fedora recommended).
- Terminal access featuring elevated `sudo` system administration privileges for package deployment.
- Basic familiarity running system command-line interface (CLI) commands.
- `podman` installed locally to execute container metrics tracking tasks.

---

## 🛠️ Lab Tasks

### Task 1: Monitor CPU Usage
**Objective**: Evaluate global processor saturation profiles and pinpoint high-usage threads.

1. Open your terminal window and access the standard dynamic real-time resource monitor:
   ```bash
   top
   ```
   *(Observe the `%CPU` ledger column to flag processes starving the hardware scheduler. Strike `q` to drop out of the interface).*
2. Deploy the advanced system statistics toolkit to gain multi-core tracking functionality:
   ```bash
   sudo dnf install sysstat -y
   ```
3. Generate a multi-report granular snapshot profile across every individual processor core:
   ```bash
   mpstat -P ALL 1 5
   ```
   *Expected Output Matrix:* Emits exactly 5 reports at 1-second increments detailing user, system, iowait, and idle values per core.

💡 **Troubleshooting**: If the system rejects your call with a missing command warning, re-verify the deployment status of the tracking package database via `rpm -q sysstat`.

---

### Task 2: Monitor Memory Usage
**Objective**: Interrogate RAM allocation maps and swap device utilization vectors.

1. Generate an instant human-readable status snapshot of physical and virtual system storage fields:
   ```bash
   free -h
   ```
   *Expected Data Metrics:* Comprehensive readout detailing absolute values tracking `total`, `used`, `free`, `shared`, `buff/cache`, and critically, `available` execution memory.
2. Launch the dynamic top table pre-configured to automatically isolate and sort allocations by memory-hungriest processes:
   ```bash
   top -o %MEM
   ```
   *(Exit the visual grid layout at any point by hitting `q`)*.

---

### Task 3: Monitor Disk Usage
**Objective**: Evaluate local file system boundary filling states and storage device I/O bottlenecks.

1. Audit usage capacities across every currently mounted directory block storage path:
   ```bash
   df -h
   ```
2. Dig into a localized directory tree layout structure to summarize individual folder space consumption (e.g., system logs tracking paths):
   ```bash
   sudo du -sh /var/log/*
   ```
3. Provision and deploy a tracking interface to view live, interactive disk read/write throughput per operational thread:
   ```bash
   sudo dnf install iotop -y
   ```
4. Launch the live disk tracker, filtering out inactive entries to focus exclusively on active I/O processes:
   ```bash
   sudo iotop -o
   ```

💡 **Privilege Notice**: Tracking deep block storage controller transfers requires explicit kernel visibility. Always prepend `iotop` executions with administrative elevation strings (`sudo`).

---

### Task 4: Monitor Network Usage
**Objective**: Inspect open system network sockets and live interface bandwidth vectors.

1. Output a detailed matrix listing active TCP/UDP ports alongside their corresponding binding process definitions:
   ```bash
   ss -tulnp
   ```
   *Expected Elements:* Lists all protocol sockets, local listener addresses, peer routing scopes, and matching system PIDs.
2. Install a dedicated interface bandwidth monitor to observe data throughput trends visually:
   ```bash
   sudo dnf install nload -y
   ```
3. Initialize the live link traffic graph dashboard interface wrapper:
   ```bash
   nload
   ```
   *(Toggle between active hardware connections using arrow keys; strike `q` to close the utility).*

---

### Task 5: Analyze Running Processes Impact
**Objective**: Audit the specific processes that are driving hardware exhaustion.

1. Use structural sorting parameters to isolate and stream the absolute top 5 CPU-intensive tracking nodes:
   ```bash
   ps aux --sort=-%cpu | head -n 5
   ```
2. Pivot the tracking sorting flags to strip out everything except the top 5 memory-intensive application paths:
   ```bash
   ps aux --sort=-%mem | head -n 5
   ```
3. Extract real-time resource performance utilization blocks across all active containerized application frames:
   ```bash
   podman stats
   ```

---

### Task 6: Detect Resource Exhaustion
**Objective**: Audit critical system anomalies and simulate heavy hardware bottlenecks.

1. Interrogate your localized logging infrastructure to extract all error-level system messages logged since the last machine boot sequence:
   ```bash
   journalctl -p err -b
   ```
2. Provision a specialized environment load execution tool designed to test stress thresholds:
   ```bash
   sudo dnf install stress-ng -y
   ```
3. Unleash a short, safe, heavily intensive execution payload to intentionally drive up hardware stress parameters:
   ```bash
   stress-ng --cpu 4 --vm 2 --timeout 30s
   ```
   *(Open a separate, concurrent ssh terminal window workspace to observe system behavior under load using `top` or `htop` metrics).*

---

## 🏁 Conclusion
During this lab session, you developed crucial system engineering diagnostics capabilities, including:
- Checking performance baselines using toolchains like `mpstat`, `free`, and `df`.
- Managing low-level tracking commands to target errant processes via `ps` and `iotop`.
- Querying hardware metrics blocks for application containers via `podman stats`.
- Running load simulation testing protocols and identifying critical logs using system logging filters.

These metrics evaluation skills serve as the fundamental diagnostic baseline for keeping systems healthy, right-sizing application server allocations, optimizing node deployments, and parsing host infrastructure performance issues within cloud orchestration layers like OpenShift.

---

## 🚀 Next Steps
- Automate basic threshold alerts by building small telemetry validation scripts tied to periodic schedule engines (`cron`).
- Advance your infrastructure monitoring strategy by researching large-scale telemetry frameworks like **Prometheus** alongside metric graphing solutions like **Grafana**.
