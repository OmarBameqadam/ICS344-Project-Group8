# Phase 3: Defensive Strategy Proposal

## Status Before

Before applying any defensive measures, the Metasploitable3 machine had an open and unprotected SSH service on port 22. Using brute-force tools like Hydra and Metasploit from the Kali Linux attacker machine, we successfully discovered valid credentials (`vagrant:vagrant`) and gained full SSH access. The system did not have any mechanism to detect or block repeated failed login attempts. Splunk analysis confirmed the attack pattern, showing multiple failed logins followed by successful access.

![Status Before 1](images/phase3/image1.png)  
![Status Before 2](images/phase3/image2.png)

---

## Implementing the Defensive Mechanism

To secure the Metasploitable3 system against brute-force SSH attacks, we implemented **Fail2Ban**, a log-parsing intrusion prevention tool. We installed Fail2Ban, enabled the `sshd` jail, and configured it to ban IP addresses after 3 failed login attempts for 10 minutes. This setup reduces the risk of unauthorized access by blocking repeated login attempts automatically, strengthening the system’s security.

### Installing Fail2Ban:

![Install Fail2Ban 1](images/phase3/image3.png)  
![Install Fail2Ban 2](images/phase3/image4.png)

Now, we are configuring Fail2Ban to protect the SSH service by editing the `jail.local` file. We enabled the SSH jail and set rules to monitor failed login attempts in `/var/log/auth.log`. If a user fails to log in three times within five minutes, their IP address is automatically banned for 10 minutes. This setup helps prevent brute-force SSH attacks.

![Configure Jail](images/phase3/image5.png)

### Starting the Fail2Ban Service:

![Start Service](images/phase3/image6.png)

Now Fail2Ban is running and protecting the SSH service.

![Fail2Ban Running](images/phase3/image7.png)

We installed and configured Fail2Ban to monitor SSH logins, and confirmed it’s running. This setup helps block IPs after repeated failed attempts, protecting the system from brute-force attacks.

---

## Rerun the Attack (Testing)

### Rerunning the Brute Force Attack Using Metasploit:

![Attack Re-run](images/phase3/image8.png)

Unlike Phase 1, the attack was blocked. Metasploit failed to find valid credentials and showed no successful logins. This confirms that Fail2Ban detected the repeated failed attempts and automatically banned the attacker's IP, effectively preventing unauthorized SSH access.

To confirm that our defense mechanism is working, we attempted to reconnect to the Metasploitable3 machine via SSH after the brute-force attack was executed and blocked by Fail2Ban.

![Connection Refused](images/phase3/image9.png)

As expected, the connection was refused, indicating that Fail2Ban successfully detected and banned the attacker's IP address after multiple failed login attempts, effectively protecting the system.

---

## Before-and-After Comparison

Initially, we launched a brute-force SSH attack using Hydra and Metasploit on Metasploitable3. The attack completed successfully and attempted multiple password guesses without any restriction, confirming that no blocking mechanism was in place.

![Before 1](images/phase3/image10.png)  
![Before 2](images/phase3/image11.png)  
![Before 3](images/phase3/image12.png)  
![Before 4](images/phase3/image13.png)

### Remote Access:

![Remote Access](images/phase3/image14.png)

Next, we configured and activated Fail2Ban to monitor `/var/log/auth.log` for repeated SSH login failures. We edited the jail settings, restarted the service, and verified that the `sshd` jail was enabled and actively protecting the system.

After re-running the same brute-force attack, the attacker IP was successfully detected and blocked by Fail2Ban. The attack was interrupted, and all SSH attempts were denied.

This comparison confirms that Fail2Ban effectively mitigated brute-force attacks by dynamically banning suspicious IPs and reducing attack surface on the SSH service.
