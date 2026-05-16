# Using Red Hat Customer Portal and Cockpit

This repository contains a hands-on lab focused on modern, centralized enterprise Linux administration. You will learn to navigate official vendor knowledge spaces, administer technical service workflows via the Red Hat Customer Portal, deploy the web-based graphical management engine Cockpit, and audit system performance telemetry through a unified browser interface.

---

## 🎯 Objectives
By the end of this lab, you will be able to:
- Navigate the Red Hat Customer Portal to query enterprise software knowledgebases.
- Open, document, and manage vendor technical support cases.
- Install, configure, and secure the Cockpit web administration console.
- Analyze host resource metrics, manage containers, and filter system logs graphically.

## 📋 Prerequisites
- A RHEL 8/9 system with active terminal access and `sudo` or `root` privileges.
- An active Red Hat developer or enterprise customer account.
- Reliable internet connectivity to reach external portal networks and download mirrors.
- Basic familiarity running system command-line interface (CLI) commands.

---

## 🛠️ Lab Tasks

### Task 1: Accessing Red Hat Customer Portal
**Objective**: Authenticate against official vendor platforms to unlock diagnostic indexes and documentation.

#### Subtask 1.1: Log in to Red Hat Customer Portal
1. Open a web browser on your client machine and navigate to the portal landing page:
   ```text
   https://access.redhat.com
   ```
2. Click the **Log in** utility action button and input your Red Hat account credential strings.
3. Confirm successful authentication by verifying your account name appears in the upper right interface window.

#### Subtask 1.2: Access Knowledgebase Articles
1. Locate the centralized portal index search text field.
2. Input the following technical research string and hit enter:
   ```text
   RHEL 9 system logging
   ```
3. Evaluate the ranked results list, opening relevant documentation tracks to inspect the structural layout of solution sheets.

💡 **Troubleshooting**: If the repository restricts your query actions or blocks solution access, check your portal profile to ensure an active product subscription is linked to your user account.

---

### Task 2: Opening Support Cases
**Objective**: Build out formal technical support requests inside vendor case trackers.

#### Subtask 2.1: Create a Support Case
1. Navigate to the top navigation header on the main customer dashboard and select **Support** \(\rightarrow\) **Support Cases**.
2. Click the configuration track link to **Open a Case**.
3. Populate the diagnostic scope fields with matching values:
   - **Product**: `Red Hat Enterprise Linux`
   - **Version**: *(Select the active release matching your local system engine)*
   - **Problem Type**: `Technical`
4. Draft a descriptive evaluation issue text summary inside the context block (e.g., `"Cockpit service socket failing to initialize on custom port mappings"`).
5. Submit the ticket to push the string parameters onto the active tracking queues.

*Expected Outcome:* The system database returns a dedicated, permanent tracking case identification string and routes an confirmation summary to your registered email path.

---

### Task 3: Installing and Configuring Cockpit
**Objective**: Provision the native web management console layer and configure boundary network parameters.

#### Subtask 3.1: Install Cockpit Packages
1. Return to your RHEL system shell and deploy the base manager along with the container dashboard integration wrapper:
   ```bash
   sudo dnf install cockpit cockpit-podman -y
   ```
2. Bind the underlying connection listening engine into your persistent system startup loops and initialize it immediately:
   ```bash
   sudo systemctl enable --now cockpit.socket
   ```
3. Audit the operational health status of the network stream listening target:
   ```bash
   sudo systemctl status cockpit.socket
   ```
   *Expected Output State:* `Active: active (listening)` bound default port tracking metrics onto port `9090`.

#### Subtask 3.2: Configure Firewall
1. Authorize the web console profile layer ruleset across your permanent system packet shield:
   ```bash
   sudo firewall-cmd --add-service=cockpit --permanent
   sudo firewall-cmd --reload
   ```

💡 **Troubleshooting**: If your browser times out or fails to parse pages, verify that your local interface is listening properly on the target network port parameters using socket diagnostic calls: `sudo ss -tulnp | grep 9090`.

---

### Task 4: Exploring Cockpit Dashboard
**Objective**: Access the unified graphical console to analyze host metrics, containers, and log indexes.

#### Subtask 4.1: Access Cockpit Web Interface
1. Launch an external browser session pointing to your server node network address:
   ```text
   https://<your-server-ip>:9090
   ```
2. Overpass the self-signed certificate warning overlay screen.
3. Authenticate against the system using your standard local Linux system account username and password.

#### Subtask 4.2: Navigate Dashboard Features
Step through the left-side index panel to inspect different operational telemetry dimensions:
*   **System Overview**: Read out live hardware graphs monitoring real-time CPU threads, RAM curves, and storage metrics.
*   **Logs**: Investigate chronological system ledger outputs.
*   **Networking**: Manage interface configurations and review packet transfer graphs.
*   **Podman Containers**: Create, manage, and monitor containerized microservice execution states directly.

📌 **Key Concept**: Cockpit works as an on-demand translation layer. Actions triggered within its web layout automatically map to native terminal tools under the hood, ensuring zero overhead or performance footprint issues when closed.

#### Subtask 4.3: View System Logs
1. Click the **Logs** parameter module link inside the left application pane.
2. Adjust the interface filtering selectors to query specific logs using precise filters:
   - **Priority**: Toggle blocks to show `Error` or `Warning` exclusively.
   - **Time Range**: Limit historical read windows to isolated segments.
   - **Service Name**: Target a single operational unit entry string, such as `cockpit`.

---

## 🏁 Conclusion
During this lab session, you developed crucial enterprise system visibility capabilities, including:
- Accessing official knowledge indexes and documentation streams.
- Orchestrating ticket lifecycles inside support tracking environments.
- Deploying, configuring, and securing Cockpit web engine sockets.
- Filtering complex system logs and checking container resources graphically.

These diagnostics management skills form the foundation for modern cloud administration, allowing systems engineers to monitor hardware health, triage server errors, and manage microservices smoothly across hybrid environments.

---

## 🚀 Next Steps
- Expand your visual cluster administration capabilities by provisioning virtual machine managers using the extension package: `sudo dnf install cockpit-machines -y`.
- Integrate Cockpit's dynamic graphical metrics with automated log monitoring templates to optimize your day-to-day administrative workflow.

---

## 📚 Additional Resources
*   [Official Cockpit Project Documentation](https://cockpit-project.org)
*   [Red Hat Customer Portal Knowledgebase](https://redhat.com)
