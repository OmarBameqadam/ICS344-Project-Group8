# Phase 1: Brute-Force Attack Documentation

---

## Task 1.1: Use Metasploit to Compromise the Service

- **Chosen Vulnerability:** SSH on Ubuntu  
- **Attacker:** Kali Linux  
- **Victim:** Metasploit3 VM running on Ubuntu Linux  
- **Victim’s IP:** `10.0.2.15`

---

### Step 1: Scanning the Victim Ports

As shown in the image below, the SSH service is open on the victim machine.

![SSH Port Scan](images(phase1)/Scanning_Ports.png)

---

### Step 2: Using Metasploit Tools

We start by launching Metasploit with the `msfconsole` command. Then, we use the `ssh_login` scanner module to brute-force credentials using a wordlist.

![Using msfconsole](images(phase1)/Using_Metasploit.png)

---

### Step 3: Result and Exploit Execution

After executing the scanner, the correct credentials are discovered:

- **Username:** `vagrant`
- **Password:** `vagrant`

![Brute-force result](images(phase1)/Results1.1.png)  

This allows remote command execution via SSH.

![Remote access through SSH](images(phase1)/Remote_access.png)

---

## Task 1.2: Compromising the Service Using a Custom Script

---

### Step 1: Scanning the Victim Ports

As with Task 1.1, we begin by scanning for open ports on the victim machine.

---

### Step 2: Using a Custom Script

A Python-based custom brute-force script was used, leveraging **Hydra** for fast execution.

![Python script using Hydra](images(phase1)/Custom_Script.png)

The script is made executable and run via the terminal:

![chmod-image](images(phase1)/chmod.png)

that will brute force the SSH login as shown below  
![Brute-forcing in action](images(phase1)/SSH_Bruteforce.png)

---

### Step 3: Result and Exploit Execution

After running the custom script, the correct SSH login credentials were discovered:

- **Username:** `vagrant`  
- **Password:** `vagrant`

This result is shown below:  
![Script output - success](images(phase1)/Results1.2.png)

Similar to Task 1.1 Step 3, these credentials can now be used to SSH into the victim machine and execute remote commands.

---

