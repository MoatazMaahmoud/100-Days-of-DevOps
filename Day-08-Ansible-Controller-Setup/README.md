## Day 8: Ansible Controller Setup & Version Pinning

**Objective:**
Provision a central jump-host as an Ansible Control Node by globally installing a specific, pinned version of Ansible using the Python package manager.

**Scenario:**
The Nautilus DevOps team selected Ansible for configuration management due to its agentless, SSH-driven architecture. To standardize the testing environment, Ansible version `4.9.0` needed to be installed globally on the central jump-host so all administrative users could execute playbooks against the fleet.

**Technical Implementation:**
1. Accessed the central jump-host.
2. Utilized `pip3` with elevated privileges (`sudo`) to install the exact requested version of Ansible. Using `sudo` ensures the binaries are placed in a globally accessible `$PATH` (e.g., `/usr/local/bin/`) rather than the local user directory (`~/.local/bin/`):
   ```bash
   sudo pip3 install ansible==4.9.0