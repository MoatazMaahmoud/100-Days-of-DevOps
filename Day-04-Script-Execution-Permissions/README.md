## Day 4: Script Execution Permissions

**Objective:**
Modify file permissions on a target application server to grant executable rights to a backup automation script for all users.

**Scenario:**
The xFusionCorp sysadmin team distributed a new bash script (`xfusioncorp.sh`) to automate backup processes across the fleet. However, the script lacked the necessary execution permissions on App Server 1, which would cause automated triggers to fail. 

**Technical Implementation:**
1. Authenticated to App Server 1 (`stapp01`) via SSH.
2. The initial file permissions were absolutely restricted (`----------`). 
3. Utilized the `chmod` utility to append both read (`r`) and execute (`x`) bits for all (`a`) users on the target script. 
   *(Note: Bash scripts require read permissions in addition to execute permissions because the interpreter must be able to read the file's text contents to run the commands).*
   ```bash
   sudo chmod a+rx /tmp/xfusioncorp.sh```