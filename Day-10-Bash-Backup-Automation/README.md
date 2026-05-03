## Day 10: Bash Scripting & Backup Automation

**Objective:**
Develop and deploy a secure bash script to automate the compression and off-site transfer of website directories without utilizing elevated (`sudo`) privileges.

**Scenario:**
The production support team required a backup mechanism for the static e-commerce website hosted on App Server 3. The objective was to compress the `/var/www/html/ecommerce` web root into a `.zip` archive, store it locally in a temporary `/backup` directory, and securely transfer it to the Nautilus Storage Server. The script had to execute without interactive password prompts and adhere strictly to the Principle of Least Privilege (no `sudo` within the script).

**Technical Implementation:**
1. **Dependency Management:** Installed the required `zip` package manually on the target node.
2. **Directory Provisioning:** Created the `/scripts` and `/backup` directories, explicitly assigning ownership to the executing user (`banner`) to avoid permissions boundary issues:
   ```bash
   sudo chown banner:banner /scripts /backup
3. **PKI Configuration:** Established password-less SSH authentication between App Server 3 and the Storage Server (ststor01) to enable non-interactive file transfers.
4. **Script Development:**
Developed /scripts/ecommerce_backup.sh:
    ```bash
    #!/bin/bash
    zip -r /backup/xfusioncorp_ecommerce.zip /var/www/html/ecommerce
    scp /backup/xfusioncorp_ecommerce.zip natasha@ststor01:/backup/\
5. **Execution:** Granted executable permissions (chmod +x) and validated the end-to-end automation pipeline.