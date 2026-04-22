## Day 5: SELinux Installation and Configuration

**Objective:**
Install Security-Enhanced Linux (SELinux) packages on a target application server and configure the baseline state to `disabled` to prepare for a scheduled maintenance window and future policy tuning.

**Scenario:**
Following a security audit, xFusionCorp Industries mandated the rollout of SELinux for advanced Mandatory Access Control (MAC). To prevent immediate application breakage, the installation required a phased approach: installing the core packages and permanently setting the configuration to `disabled` prior to a scheduled reboot.

**Technical Implementation:**
1. Authenticated to App Server 1 (`stapp01`) via SSH.
2. Installed the core SELinux policy and utility packages using the `yum` package manager:
   ```bash
   sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils

3. Modified the SELinux configuration file securely using sed to ensure the system boots with SELinux disabled during the upcoming maintenance window:
```bash
	sudo sed -i 's/^SELINUX=.*/SELINUX=disabled/' /etc/selinux/config```