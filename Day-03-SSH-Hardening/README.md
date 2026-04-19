## Day 3: SSH System Hardening (Disabling Root Login)

**Objective:**
Enhance the security posture of the Stratos Datacenter by disabling direct SSH root login across all application servers, mitigating the risk of brute-force attacks.

**Scenario:**
Following a security audit at xFusionCorp Industries, a new protocol requires locking down the SSH daemon. Administrators must log in using their personal, unprivileged accounts and escalate privileges via `sudo` to ensure strict auditing and accountability.

**Technical Implementation:**
This procedure was executed across App Server 1 (`stapp01`), App Server 2 (`stapp02`), and App Server 3 (`stapp03`).

1. Authenticated to the target server via SSH.
2. Modified the SSH Daemon configuration file using stream editing (`sed`) to enforce the policy:
   ```bash
   sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/g' /etc/ssh/sshd_config
3. Restarted the SSH service to apply the configuration changes:
   ```bash
  	sudo systemctl restart sshd
