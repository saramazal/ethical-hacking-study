## The Kill Chain is a framework that describes the stages of a cyber attack, from the initial reconnaissance to the final impact. 
It's often used to understand and disrupt the attacker's activities. 
### Here’s a breakdown of the typical steps in the Kill Chain:

1. **Reconnaissance**: The attacker gathers information about the target, such as IP addresses, domain names, and vulnerabilities, using both passive and active reconnaissance techniques.

2. **Weaponization**: The attacker creates a deliverable payload, such as malware, that will exploit a vulnerability. This might involve coupling an exploit with a backdoor to create a weapon.

3. **Delivery**: The attacker sends the weapon to the target through methods like phishing emails, USB drives, or malicious websites.

4. **Exploitation**: Once the weapon is delivered, the exploit is triggered, and the attacker gains access to the target system by exploiting a vulnerability.

5. **Installation**: The attacker installs malware or backdoors on the target system to maintain persistent access.

6. **Command and Control (C2)**: The compromised system connects back to the attacker’s C2 server, allowing the attacker to control the system remotely.

7. **Actions on Objectives**: The attacker completes their mission, which could include data exfiltration, destruction of data, or further network penetration.

Understanding the Kill Chain helps defenders identify and stop an attack at various stages, ideally before the attacker can reach their objectives.