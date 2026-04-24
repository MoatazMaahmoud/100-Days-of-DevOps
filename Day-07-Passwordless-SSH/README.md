## Day 7: SSH Key-Based Authentication (Password-less SSH)

**Objective:**
Configure secure, password-less SSH access from a central jump-host to a fleet of application servers to enable automated script execution without interactive credential prompts.

**Scenario:**
The systems administration team deployed automated maintenance scripts on the Stratos Datacenter jump-host. For these scripts to execute seamlessly across the network, the executing user (`thor`) required uninterrupted, password-less SSH access to the application servers (`stapp01`, `stapp02`, `stapp03`) via their respective sudo users.

**Technical Implementation:**
1. Generated a 4096-bit RSA SSH key pair on the central jump-host for the `thor` user:
   ```bash
   ssh-keygen -t rsa -b 4096
2. Distributed the public key to the target application servers using the ssh-copy-id utility, which securely appends the key to the target's ~/.ssh/authorized_keys file and enforces proper directory permissions:
   ```bash
	ssh-copy-id tony@stapp01
	ssh-copy-id steve@stapp02
	ssh-copy-id banner@stapp03

**Key Takeaway:**
Establishing Public Key Infrastructure (PKI) for SSH is the prerequisite for modern infrastructure automation. Configuration management tools like Ansible, deployment pipelines, and custom bash automations rely entirely on key-based authentication to manage fleets of servers securely at scale.