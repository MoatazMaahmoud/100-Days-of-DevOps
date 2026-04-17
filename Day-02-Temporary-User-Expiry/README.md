## Day 2: Temporary User Setup with Expiry

**Objective:**
Provision a temporary access account for a developer on a specific Application Server, ensuring the account automatically expires on a predetermined date to maintain security compliance.

**Scenario:**
A developer requires time-limited access to the Nautilus project on App Server 3. To prevent the creation of "orphan accounts" (a major security vulnerability), the account must be configured to expire automatically on `2027-04-15`.

**Technical Implementation:**
1. Authenticated to App Server 3 (`stapp03`) via SSH.
2. Executed the user creation command utilizing the expire flag (`-e`):
   ```bash
   sudo useradd -e 2027-04-15 kareem

Verification:
Validated the expiry configuration using the chage (change age) utility to ensure the policy was successfully applied at the OS level:
```Bash

sudo chage -l kareem

Confirmed output included: Account expires : Apr 15, 2027