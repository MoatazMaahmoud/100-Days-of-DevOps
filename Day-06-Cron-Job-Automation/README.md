## Day 6: OS-Level Task Scheduling with Cron

**Objective:**
Automate the execution of system tasks by installing the cron daemon and configuring a scheduled job across the application server fleet.

**Scenario:**
The systems administration team requires a mechanism to run automated deployment and backup scripts on a strict schedule. To validate this functionality, a sample cron job was deployed to write a test string to a temporary file every 5 minutes on all application servers.

**Technical Implementation:**
This procedure was executed across App Server 1 (`stapp01`), App Server 2 (`stapp02`), and App Server 3 (`stapp03`).

1. Authenticated to the target servers via SSH.
2. Installed the cron daemon package (`cronie`) using the `yum` package manager:
   ```bash
   sudo yum install -y cronie
3. Initialized the crond service and enabled it to persist across system reboots:
   ```bash
	sudo systemctl start crond
	sudo systemctl enable crond
4.Configured the cron schedule for the root user using crontab:
   ```bash
	sudo crontab -e
	# Appended the following schedule: 
	# */5 * * * * echo hello > /tmp/cron_text
	
