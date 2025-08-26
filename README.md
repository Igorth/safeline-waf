# SafeLine Web Application Firewall (WAF)

<img width="1116" height="737" alt="safelinewaf" src="https://github.com/user-attachments/assets/10993dd6-a920-47c9-b413-dfa9ddf83393" />

## Introduction  
The goal of this lab is to demonstrate the use of **SafeLine Web Application Firewall (WAF)** in a controlled environment.  
For this purpose, we deployed a vulnerable application (**DVWA – Damn Vulnerable Web Application**) on an Ubuntu VM and launched attacks from a Kali Linux VM, testing SafeLine WAF capabilities against:  

- SQL Injection  
- HTTP Flood  
- Malicious authentication attempts  
- Custom rules  

## Environment  

### Virtual Machines  
- **Ubuntu** (192.168.x.x) – Hosts DVWA  
- **Kali Linux** (192.168.x.x) – Attack machine  

Both VMs were configured in **Bridge Adapter** mode in VirtualBox to share the same network.  

### DVWA Setup (Ubuntu)  
1. DVWA installation and configuration.  
2. Editing the **hosts** file on both VMs:  

   ```bash
   sudo nano /etc/hosts
   <Ubuntu I> dvwa.local
3. DVWA is now accessible via:
4. ```bash
   http://dvwa.local/dvwa

## SSL Certificate
A Self-Signed SSL Certificate was generated with openssl on Ubuntu for use in SafeLine.

## SafeLine WAF
- Installed following the official [documentation](https://docs.waf.chaitin.com/en/GetStarted/Deploy).
- Created a new application in the SafeLine dashboard:
  - Configured URL: https://dvwa.local/dvwa
  - SSL certificate added.

# Objectives
## 1. SQL Injection from Kali Linux
- Perform a SQL Injection attack against DVWA.
- Validate that SafeLine detects and blocks the attempt.
- Log and review events.

<img width="1544" height="622" alt="Screenshot 2025-08-26 124803" src="https://github.com/user-attachments/assets/1cf81e4a-cad2-420e-b6b4-d418c050ae1b" />
<img width="886" height="500" alt="Screenshot 2025-08-26 125025" src="https://github.com/user-attachments/assets/63d32d02-d760-4ce0-8201-4b862d8be1d3" />


## 2. HTTP Flood Defense
- Simulate a HTTP Flood attack using tools like ab or hydra.
- Observe how SafeLine mitigates the traffic.

<img width="1538" height="218" alt="Screenshot 2025-08-26 123919" src="https://github.com/user-attachments/assets/f6238298-5c8b-44f5-b5bb-0338e1ea6ed3" />

## 3. Authentication Protection
- Perform multiple failed login attempts.
- Verify whether SafeLine enforces rate-limiting or temporary blocking.

<img width="959" height="669" alt="Screenshot 2025-08-26 124148" src="https://github.com/user-attachments/assets/1a134861-c43e-47ed-92bd-23277784b03a" />
<img width="630" height="671" alt="Screenshot 2025-08-26 124222" src="https://github.com/user-attachments/assets/7462c346-a787-4336-a1d7-6175cf043c32" />

## 4. Custom Rules
- Create additional rules such as:
- Blocking a specific User-Agent.
- Restricting access by IP.
- Denying requests containing malicious keywords.

<img width="896" height="503" alt="Screenshot 2025-08-26 124520" src="https://github.com/user-attachments/assets/45d82649-c4b9-4ba2-af9d-04f74f94f200" />


# Results & Analysis
- **SQL Injection**: basic injection attempts were blocked and logged.
- **HTTP Flood**: abnormal traffic was detected and mitigated, reducing impact on DVWA.
- **Authentication Protection**: temporary blocks applied after repeated failures.
- **Custom Rules**: effectively denied malicious requests based on defined policies.


<img width="1765" height="790" alt="Screenshot 2025-08-26 125351" src="https://github.com/user-attachments/assets/06eea1fd-e19e-4846-94ce-aaa54ef9f03f" />


# Conclusion
This lab demonstrated that SafeLine WAF provides a strong security layer in front of vulnerable applications.
Key takeaways:
- Protection against common attacks (SQLi, XSS, brute force).
- Mitigation of volumetric HTTP layer attacks.
- Flexibility through custom rules.

# Reference
- [Youtube](https://www.youtube.com/watch?v=N0dEC1nuWCQ)
- [SafeLine WAF](https://safepoint.cloud/landing/safeline)
