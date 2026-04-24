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
Welcome to Day 7! You are now hitting a major milestone.

Up until today, every time you connected to an App Server, you had to manually type a password (Ir0nM@n, Am3ric@, etc.). If a script needs to run a backup at 3:00 AM, there is no human awake to type that password.

This is where Password-less SSH (Key-Based Authentication) comes in. It is the absolute foundation of modern infrastructure automation. Tools like Ansible, Jenkins, and Terraform literally cannot function without it.

Here is the game plan to get this working from your jump-host.
1. The Execution (How to pass the lab)

You are currently logged into the jump-host as the user thor. You will do all of these steps directly from the jump-host terminal.

Step 1: Generate the SSH Key Pair
First, you need to create a private/public key pair for the user thor.
Bash

ssh-keygen -t rsa -b 4096

When it asks where to save the key, just press Enter to accept the default location. When it asks for a passphrase, press Enter twice to leave it empty (if you set a passphrase, the script will get stuck asking for it!).

Step 2: Copy the Public Key to the App Servers
Now, you need to distribute thor's public key to the three app servers. The ssh-copy-id tool does this safely and automatically sets the correct file permissions on the target servers.

    App Server 1:
    Bash

    ssh-copy-id tony@stapp01

    (Type yes if prompted about the host authenticity, then enter Tony's password: Ir0nM@n)

    App Server 2:
    Bash

    ssh-copy-id steve@stapp02

    (Password: Am3ric@)

    App Server 3:
    Bash

    ssh-copy-id banner@stapp03

    (Password: BigGr33n)

Step 3: Verify the Password-less Access
You must verify that the keys work. Try to log into each server. If it drops you right into the prompt without asking for a password, it worked!
Bash

ssh tony@stapp01
# (You should be logged in immediately. Type 'exit' to go back to jump-host)

Repeat the quick test for stapp02 and stapp03. Once verified, click submit!
2. The "Senior Engineer" Explanation

How does this actually work?
When you ran ssh-keygen, Linux generated two mathematically linked files in the ~/.ssh/ directory:

    id_rsa (The Private Key): This is your secret ID badge. It stays on the jump-host and should never be shared.

    id_rsa.pub (The Public Key): This is the lock.

When you ran ssh-copy-id, it took the contents of the public key and pasted it into a special file on the target server called ~/.ssh/authorized_keys. Now, when the jump-host tries to connect, the App Server checks the public key, issues a cryptographic challenge, and if the jump-host's private key solves it, access is granted instantly.
3. The Interview Angle

Recruiter Question: "We are evaluating Ansible for configuration management across our Linux fleet. How does Ansible securely connect to thousands of nodes without us hardcoding passwords into our playbooks?"

Your Answer: "Ansible is an agentless tool that relies on standard OpenSSH. To secure the connection without hardcoded passwords, we configure Public Key Infrastructure (PKI). I would generate an SSH key pair on the Ansible Control Node and distribute the public key to the authorized_keys file of the dedicated service account on all target nodes. This establishes secure, password-less authentication for all automated playbooks."
Phase 4: Your GitHub Portfolio Update

Open Git Bash on your Windows machine and run through your daily routine to document this critical DevOps skill.

    cd ~/Documents/100-Days-of-DevOps

    mkdir Day-07-Passwordless-SSH

    cd Day-07-Passwordless-SSH

    notepad README.md

Paste this professional documentation into Notepad:
Markdown

## Day 7: SSH Key-Based Authentication (Password-less SSH)

**Objective:**
Configure secure, password-less SSH access from a central jump-host to a fleet of application servers to enable automated script execution without interactive credential prompts.

**Scenario:**
The systems administration team deployed automated maintenance scripts on the Stratos Datacenter jump-host. For these scripts to execute seamlessly across the network, the executing user (`thor`) required uninterrupted, password-less SSH access to the application servers (`stapp01`, `stapp02`, `stapp03`) via their respective sudo users.

**Technical Implementation:**
1. Generated a 4096-bit RSA SSH key pair on the central jump-host for the `thor` user:
   ```bash
   ssh-keygen -t rsa -b 4096

(Note: The passphrase was intentionally left blank to allow fully automated script execution).

    Distributed the public key to the target application servers using the ssh-copy-id utility, which securely appends the key to the target's ~/.ssh/authorized_keys file and enforces proper directory permissions:
    Bash

    ssh-copy-id tony@stapp01
    ssh-copy-id steve@stapp02
    ssh-copy-id banner@stapp03

Verification:
Validated the PKI configuration by successfully initiating SSH sessions to all target nodes without being prompted for a password:
Bash

ssh tony@stapp01

**Key Takeaway:**
Establishing Public Key Infrastructure (PKI) for SSH is the prerequisite for modern infrastructure automation. Configuration management tools like Ansible, deployment pipelines, and custom bash automations rely entirely on key-based authentication to manage fleets of servers securely at scale.