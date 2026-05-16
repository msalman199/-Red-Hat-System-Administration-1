# Monitoring and Managing Processes

This repository contains a hands-on lab focused on Linux process management. You will learn to inspect system resource utilization, control application execution states, send operational signals, manage background shell tasks, and modify scheduler prioritization flags.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- View, inspect, and evaluate active system processes.
- Monitor metrics dynamically using `ps`, `top`, and interactive `htop` dashboard maps.
- Dispatch signals to processes using explicit identifiers (`kill`) and naming filters (`pkill`/`killall`).
- Control job streams using background (`bg`), foreground (`fg`), and status (`jobs`) handlers.
- Alter kernel process schedules and execution priority weights using `nice` and `renice`.

## 📋 Prerequisites
- A Linux-based operating system (e.g., Ubuntu 22.04, CentOS Stream 9, or RHEL 9).
- Terminal access featuring elevated `sudo` system administration privileges.
- Basic familiarity running system command-line interface (CLI) utilities.

---

## 🛠️ Lab Tasks

### Task 1: Viewing Processes with ps, top, and htop

#### Subtask 1.1: List Processes with ps
1. Open your terminal window.
2. Generate a comprehensive snapshot list of all running processes across the environment:
   ```bash
   ps aux
   ```
   - `a` : Show execution tracks for all active terminal users.
   - `u` : Display a user-oriented layout (showing memory, CPU, and owners).
   - `x` : Include background processes completely detached from controlling terminals.

3. Sift through massive process pools to isolate specific running binaries (e.g., Nginx):
   ```bash
   ps aux | grep nginx
   ```

#### Subtask 1.2: Monitor Processes Dynamically with top
1. Launch the default core real-time monitoring screen interface:
   ```bash
   top
   ```
2. **Interactive Controls**:
   - Press `Shift + M` to sort the list dynamically by memory usage profile maps.
   - Press `q` to quit out of the dashboard layer.

#### Subtask 1.3: Use htop for an Interactive View
1. If the tool is missing from your deployment tree, deploy the packages using your platform manager:
   ```bash
   sudo apt install htop -y     # Ubuntu / Debian
   sudo dnf install htop -y     # CentOS / RHEL
   ```
2. Launch the color-coded interactive visual engine dashboard:
   ```bash
   htop
   ```
   *(Navigate the grid using arrow keys; toggle sorting fields by striking the `F6` key)*

---

### Task 2: Sending Signals to Processes

#### Subtask 2.1: Terminate a Process with kill
1. Locate the Process ID (PID) numbers tied to an active task (e.g., Firefox):
   ```bash
   pidof firefox
   ```
2. Issue a graceful termination signal (**SIGTERM / Signal 15**), letting the utility save states and shut down properly:
   ```bash
   kill <PID>
   ```
3. If an application locks up or refuses to respond, override it by forcing immediate closure via a **SIGKILL / Signal 9** flag:
   ```bash
   kill -9 <PID>
   ```

#### Subtask 2.2: Kill Processes by Name with pkill and killall
1. Erase all executing instances matching a program target name string concurrently without looking up raw numbers:
   ```bash
   pkill firefox
   ```
   *Alternative:*
   ```bash
   killall firefox
   ```

---

### Task 3: Job Control (jobs, fg, bg)

#### Subtask 3.1: Manage Background and Foreground Jobs
1. Launch a long-running system command directly into a background shell thread by appending an ampersand:
   ```bash
   sleep 300 &
   ```
2. Check the active directory tracking index monitoring jobs assigned to your shell process pool:
   ```bash
   jobs
   ```
   *Expected Output Layout:* `[1]+ Running sleep 300 &`
3. Pull a background task back into an active, interactive foreground workspace state:
   ```bash
   fg %1
   ```
4. **Pause and Suspend**: Freeze an active foreground utility process stream by striking `Ctrl + Z`.
5. Resume a paused, suspended execution job thread securely in the background without tying up your shell inputs:
   ```bash
   bg %1
   ```

---

### Task 4: Adjusting Process Priority (nice, renice)

#### Subtask 4.1: Start a Process with Modified Priority
1. Spin up a new task with a custom execution weight balance (Nice values run from `-20` [highest priority] down to `19` [lowest priority]):
   ```bash
   nice -n 10 sleep 300 &
   ```

#### Subtask 4.2: Change Priority of a Running Process
1. Locate the active task identification mapping:
   ```bash
   pgrep sleep
   ```
2. Alter the priority value assignment vector on a live executing process track inside the scheduler engine:
   ```bash
   sudo renice -n 15 -p <PID>
   ```

---

## 💡 Troubleshooting Tips

* **Installation Faults**: If your package engine throws errors while grabbing `htop`, update local repository databases using `sudo apt update` or `sudo dnf check-update`.
* **Signal Lookups**: Review the total list of available signal integers and descriptive names by typing `kill -l`.
* **Privilege Demands**: Increasing process priorities (moving nice scores below zero) or altering other users' tasks requires administrative elevation via `sudo`.

---

## 🏁 Conclusion
During this lab session, you developed crucial production diagnostics capabilities, including:
- Monitoring operational environments using `ps`, `top`, and interactive `htop` dashboard maps.
- Controlling errant application pools using signal wrappers.
- Operating deep background automation pipelines with job control operators.
- Balancing scheduling priorities using resource tuning metrics.

These administrative skills form the baseline criteria for keeping systems healthy, managing system performance anomalies, and handling orchestration engine tasks inside cluster environments.

---

## 🚀 Next Steps
- Dig into `systemd` configuration targets to manage persistent service daemons.
- Research modern resource management techniques like Control Groups (`cgroups`) used to throttle container containers.
