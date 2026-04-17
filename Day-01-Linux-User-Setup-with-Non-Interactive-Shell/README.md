## Day 1: Provisioning a Non-Interactive Service Account

**Objective:**
Create a service user named `ammar` on a remote Application Server to facilitate a backup agent tool, ensuring the account cannot be used for interactive terminal login.

**Scenario:**
xFusionCorp Industries requires a service account for a backup tool. To adhere to the **Principle of Least Privilege** and secure the system, this user must not have access to an interactive shell.

**Technical Implementation:**
1. Accessed the target server (App Server 3) via SSH.
2. Executed the user creation command with a restricted shell:
   
   sudo useradd -s /sbin/nologin ammar