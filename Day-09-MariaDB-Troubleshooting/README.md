## Day 9: Incident Response & MariaDB Troubleshooting

**Objective:**
Investigate and remediate a critical production outage where the backend database service (MariaDB) failed to start, causing application-wide connectivity failures.

**Scenario:**
The Nautilus production support team reported a critical application outage in the Stratos Datacenter. The root cause was isolated to the Database Server (`stdb01`), where the MariaDB daemon was in a failed state.

**Technical Implementation:**
1. Authenticated to the database server (`stdb01`) via SSH.
2. Verified the daemon state using systemd:
   ```bash
   sudo systemctl status mariadb

The process indicated a failure with status=1/FAILURE.

3. Executed log analysis. Initial checks of the system journal (sudo journalctl -u mariadb -xe) did not reveal the fatal error.
4. Shifted investigation to the application-specific logs:
   ```bash
   sudo cat /var/log/mariadb/mariadb.log

5.Identified the root cause in the logs:
[ERROR] mariadbd: Can't create/write to file '/run/mariadb/mariadb.pid' (Errcode: 13 "Permission denied")
The system directory required for Process ID tracking had its permissions improperly modified, preventing the mysql user from writing to it.

6.Remediated the issue by recursively restoring ownership of the run directory to the mysql service account:
   ```bash
   sudo chown -R mysql:mysql /run/mariadb

7. Initialized the service and restored database availability:
   ```bash
   sudo systemctl start mariadb