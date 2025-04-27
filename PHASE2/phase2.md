# Phase 2: SIEM Dashboard Analysis

## SIEM Setup: Integrate Logs from Both Victim and Attacker Environments into Splunk

- **Splunk Server:** Hosted on a Windows machine.  
- **Attacker Machine:** Kali Linux  
- **Victim Machine:** Metasploitable 3  

To integrate the logs:
- Ensure the forward server connection is **active**.
- Use the `add monitor` command to start forwarding logs to Splunk.

### Attacker VM:
![Attacker VM Log Setup](images(phase2)/Attacker_Setup.png)

---

### Victim VM:
![Victim VM Log Setup 1](images(phase2)/Victim_Setup1.png)
![Victim VM Log Setup 2](images(phase2)/Victim_Setup2.png)
![Victim VM Log Setup 3](images(phase2)/Victim_Setup3.png)

---

## Log Visualization: Visualize and Analyze Attack Logs to Understand Attack Patterns and Behaviors

### Raw Log Data:
Some of the attack logs presented in a raw tabulated form:
![Raw Logs](images(phase2)/Attack_Logs.png)

---

### Username Targeting - Column Chart:
![Username Attempts](images(phase2)/col_chart.png)

- The attacker mainly targeted two users, **vagrant** and **uucp**, with **5 attempts** each.
- **15 attempts** were made with completely invalid usernames, showing a mix of **targeted** and **random guessing** behavior.

---

### Attack Timing - Time Chart:
![Login Attempts Over Time](images(phase2)/time_chart.png)

- There were **29 login attempts** within just **4 minutes**, indicating a **high-speed automated brute-force attack** rather than manual login attempts.

---

### Success vs Failure - Pie Chart:
![Login Success and Failures](images(phase2)/Pie_Chart.png)

- Out of all login attempts, only **2 were successful** while **23 failed**.
- This reflects a typical brute-force pattern where **many failures** eventually lead to a **successful breach**, highlighting the critical risk posed by **weak credentials**.

---

## Attack Comparison: Compare Data from the Victim and Attacker Environments

When comparing the victim’s and attacker’s systems:
- The victim machine recorded **many failed SSH login attempts** and a few **successful ones**.
- These events matched the **timing** and **IP address** of the attacks launched from the Kali Linux attacker machine.
- This clearly demonstrates a **direct link** between the **brute-force attacks** and the activity recorded on the victim's system.
