# Configuring Network Interfaces

This repository contains a hands-on lab focused on enterprise-level Linux networking. You will master the unified NetworkManager command-line interface (`nmcli`), configure deterministic static IP routing profiles, adjust link layer optimization constraints (MTU), disable unused protocols (IPv6), and handle host system identification layers.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Audit physical and virtual network devices and operational link states.
- Manage persistent interface configuration records using the `nmcli` wrapper ecosystem.
- Provision explicit static IPv4 bindings alongside custom routing gateways and DNS resolution engines.
- Adjust connection profile configurations including Maximum Transmission Unit (MTU) frames.
- Govern and cycle the central machine `NetworkManager` subsystem service.
- Implement permanent system hostname parameters and core name resolution mapping files.

## 📋 Prerequisites
- A Linux operating system featuring the `systemd` ecosystem (Red Hat Enterprise Linux, CentOS Stream, or Fedora recommended).
- Active installation of the system network orchestration engine daemon (`NetworkManager`).
- Terminal access featuring elevated `sudo` system administration privileges.
- Basic familiarity running system command-line interface (CLI) utilities.

---

## ⚙️ Lab Setup
1. Launch an active terminal shell session workspace.
2. Interrogate the runtime supervisor daemon to verify that the networking broker is fully operational:
   ```bash
   sudo systemctl status NetworkManager
   ```
3. If the unit configuration record state returns an inactive or dead status flag, initialize the tracking thread manually:
   ```bash
   sudo systemctl start NetworkManager
   ```

---

## 🛠️ Lab Tasks

### Task 1: Listing Network Devices with nmcli
**Objective**: Interrogate the hardware and virtual interface tables mapping network data streams.

1. Generate a brief tabular inventory tracking all active physical and virtual attachment structures:
   ```bash
   nmcli device status
   ```
   *Expected Output Matrix:* A grid identifying interface designations (e.g., `eth0`, `ens192`), layer types, connection tracking strings, and real-time operational states.
2. Extract exhaustive, low-level details (such as current IP assignments, hardware MAC layers, route metrics, and active upstream DNS engines) across all interface lines:
   ```bash
   nmcli device show
   ```

---

### Task 2: Configuring a Static IP Address
**Objective**: Transition an unmanaged or dynamic connection profile over to a permanent, explicit network definition.

1. Query your system configuration databases to isolate the exact, literal string name of your network profile mapping:
   ```bash
   nmcli connection show
   ```
   *💡 Troubleshooting:* If the connection registration list displays empty values, audit physical device states or virtualization layer connections by verifying physical link visibility maps using `ip link`.

2. Bind a hardcoded static address string, gateway router interface, and upstream Google DNS resolvers, while converting the runtime method away from dynamic DHCP rules:
   ```bash
   sudo nmcli connection modify "Wired connection 1" \
     ipv4.addresses 192.168.1.100/24 \
     ipv4.gateway 192.168.1.1 \
     ipv4.dns "8.8.8.8,8.8.4.4" \
     ipv4.method manual
   ```
3. Commit and push the structural runtime adjustment layout map online to recalculate active kernel link dimensions:
   ```bash
   sudo nmcli connection up "Wired connection 1"
   ```

---

### Task 3: Modifying a Connection Profile
**Objective**: Fine-tune transport boundaries and reduce security exposures across existing profiles.

1. View the full, comprehensive parameter directory binding attributes targeting your active profile configuration track:
   ```bash
   nmcli connection show "Wired connection 1"
   ```
2. Modify the link layer Maximum Transmission Unit (MTU) sizing frame constraint parameter to coordinate with upstream fabrics:
   ```bash
   sudo nmcli connection modify "Wired connection 1" 802-3-ethernet.mtu 1500
   ```
3. Mitigate network mapping exposures by disabling the unused IPv6 configuration method track:
   ```bash
   sudo nmcli connection modify "Wired connection 1" ipv6.method disabled
   ```

---

### Task 4: Restarting NetworkManager
**Objective**: Flush environment tracking parameters and prompt a complete internal subsystem configuration reconciliation.

1. Cycle the network coordination tracking daemon:
   ```bash
   sudo systemctl restart NetworkManager
   ```
2. Verify the structural recovery health state of the interface initialization tracking ledger:
   ```bash
   systemctl status NetworkManager
   ```
   *Expected Output State:* `Active: active (running)` lacking error messages or terminal system panic states.

---

### Task 5: Hostname and DNS Configuration
**Objective**: Establish explicit node identifiers and operational name resolution structures.

1. Update the operating kernel persistent server identity naming map:
   ```bash
   sudo hostnamectl set-hostname mylabhost
   ```
   Confirm your permanent mapping changes took effect immediately across tracking profiles:
   ```bash
   hostnamectl
   ```
2. Bind alternative network name lookup addresses explicitly into your configuration records:
   ```bash
   sudo nmcli connection modify "Wired connection 1" ipv4.dns "1.1.1.1 1.0.0.1"
   ```
3. Forbid upstream dynamic DHCP assignments from overriding or polluting your explicit name resolution files permanently:
   ```bash
   sudo nmcli connection modify "Wired connection 1" ipv4.ignore-auto-dns yes
   ```

---

## 🔎 Verification Steps
Validate system convergence states across networking boundaries by executing the following diagnostic checklist:

- [ ] **Audit Active Address Tables**: Confirm interface structures reflect static alignments accurately:
  ```bash
  ip addr show
  ```
- [ ] **Verify Packet Routing Paths**: Confirm layer 3 routing out across external endpoints maps cleanly:
  ```bash
  ping -c 4 8.8.8.8
  ```
- [ ] **Test Domain Name Translation**: Verify domain queries map to downstream addresses successfully:
  ```bash
  nslookup google.com
  ```

---

## 💡 Troubleshooting Tips

* **Modifications Fail to Propagate**: Force the core controller interface to tear down and reconstruct the underlying hardware links to reload variables:
  ```bash
  sudo nmcli device disconnect eth0 && sudo nmcli device connect eth0
  ```
* **DNS Resolution Failure**: Inspect the actual active lookup file tracking your system via `cat /etc/resolv.conf`. Run comprehensive network query tracking tests via `dig example.com`.
* **Missing Profiles/Devices**: Force the network engine daemon to run an interface scan and sync live mappings immediately:
  ```bash
  sudo nmcli device reapply eth0
  ```

---

## 🏁 Conclusion
During this lab session, you developed crucial enterprise network infrastructure capability profiles, including:
- Coordinating system interface structures via high-utility `nmcli` statements.
- Designing independent static IPv4 matrix definitions and profile boundaries.
- Optimization tracking across transport parameters (MTU, IPv6 dropouts).
- Governing local hostname states and DNS verification trees.

These baseline skills are essential to manage container networking parameters cleanly within complex environments like OpenShift, especially when adjusting underlying physical host servers driving isolated Podman microservice blocks.
