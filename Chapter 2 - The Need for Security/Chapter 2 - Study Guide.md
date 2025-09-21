# Chapter 2: The Need for Security
## Study Guide - Principles of Information Security

---

## 📚 **LEARNING OBJECTIVES**
Upon completion of this chapter, you should be able to:
- Discuss the organizational need for information security
- Explain why a successful information security program is the shared responsibility of an organization's three communities of interest
- List and describe the threats posed to information security and common attacks associated with those threats
- List the common development failures and errors that result from poor software security efforts

---

## 🎯 **KEY TERMS AND DEFINITIONS**

### **Core Information Security Concepts**
- **Data**: Items of fact collected by an organization. Data includes raw numbers, facts, and words
- **Information**: Data that has been organized, structured, and presented to provide additional insight into its context, worth, and usefulness
- **Information Asset**: The focus of information security; information that has value to the organization, and the systems that store, process, and transmit the information
- **Media**: As a subset of information assets, the systems and networks that store, process, and transmit information

### **Business and Management Terms**
- **Data Security**: Commonly used as a surrogate for information security, data security is the focus of protecting data or information in its various states—at rest (in storage), in processing, and in transmission (over networks)
- **Database**: A collection of related data stored in a structured form and usually managed by a database management system
- **Database Security**: A subset of information security that focuses on the assessment and protection of information stored in data repositories like database management systems and storage media

### **Threat and Attack Terminology**
- **Attack**: An intentional or unintentional act that can damage or otherwise compromise information and the systems that support it
- **Exploit**: A technique used to compromise a system
- **Vulnerability**: A potential weakness in an asset or its defensive control system(s)

---

## 🏢 **BUSINESS NEEDS FIRST**

### **Information Security's Four Important Functions**
1. **Protecting the Organization's Ability to Function**
   - Ensures business continuity
   - Protects against operational disruptions
   - Maintains competitive advantage

2. **Protecting the Data Organizations Collect and Use**
   - Critical for maintaining business operations
   - Essential for customer trust and compliance
   - Protects intellectual property and trade secrets

3. **Enabling the Safe Operation of Applications**
   - Safeguards infrastructure applications
   - Protects email and messaging systems
   - Ensures secure business applications

4. **Safeguarding Technology Assets**
   - Protects hardware and software investments
   - Ensures system reliability and performance
   - Maintains technology infrastructure

### **Management vs. Technology Focus**
- Information security is **more about management than technology**
- Focus on risk management, policy, and enforcement
- Requires organizational commitment and cultural change
- Success depends on people, processes, and technology working together

---

## 🚨 **THREATS AND ATTACKS**

### **The Threat Environment**
- **3.6 Billion Potential Hackers**: About 49.2% of world's population has Internet access
- Threats are always present, but attacks exist only when specific acts may cause loss
- Organizations must understand both threats and vulnerabilities to make informed decisions

### **The 12 Categories of Threats**

#### **1. Compromises to Intellectual Property**
- **Definition**: The creation, ownership, and control of original ideas as well as the representation of those ideas
- **Types**: Trade secrets, copyrights, trademarks, patents
- **Primary Threat**: Software piracy
- **Protection**: Copyright laws, licensing agreements, technical controls

**Software Piracy Statistics:**
- 39% of software installed globally in 2015 was not properly licensed
- 26% of employees admit installing unauthorized software at work
- Global commercial value of unlicensed software: $52.2 billion

**Copyright Protection Mechanisms:**
- Digital watermarks and embedded code
- Unique software registration codes
- End-user license agreements (EULAs)
- Online registration requirements

#### **2. Deviations in Quality of Service**
- **Service Level Agreement (SLA)**: Document specifying expected level of service from providers
- **Availability Disruption**: Interruption in service causing adverse events
- **Uptime/Downtime**: Percentage of time service is available/unavailable

**Types of Service Disruptions:**
- Internet service provider failures
- Power grid interruptions
- Telecommunications outages
- Data communications provider issues

**Cost of Downtime Examples:**
- 99.9% uptime (8.76 hours downtime): $10,950 average cost
- 99.5% uptime (43.92 hours downtime): $54,750 average cost

#### **3. Espionage or Trespass**
- **Competitive Intelligence**: Legal and ethical collection of competitor information
- **Industrial Espionage**: Illegal collection of competitor information for unfair advantage
- **Shoulder Surfing**: Direct observation of information or system use

**Hacker Categories:**
- **Expert Hackers**: Highly skilled, master multiple programming languages and systems
- **Novice Hackers**: Limited skill, use tools created by expert hackers
- **Professional Hackers**: Conduct attacks for financial benefit or crime organizations
- **Penetration Testers**: Authorized security professionals testing systems

**Hacker Variants:**
- **Script Kiddies**: Use expertly written software to attack systems
- **Packet Monkeys**: Use automated exploits for denial-of-service attacks
- **Crackers**: Focus on removing software copyright protection
- **Phreakers**: Manipulate telephone systems

**Privilege Escalation:**
- **Jailbreaking**: Gaining administrator control over iOS devices
- **Rooting**: Gaining administrator control over Android devices
- **Back Doors**: Unauthorized access mechanisms

#### **4. Forces of Nature**
Natural events that can overwhelm control systems and cause data loss or availability issues.

**Types of Natural Disasters:**
- **Fire**: Can damage buildings and equipment, cause smoke/water damage
- **Floods**: Direct damage to systems or access disruption
- **Earthquakes**: Building damage, access disruption, infrastructure damage
- **Lightning**: Power system damage, fires, equipment destruction
- **Tornados/Windstorms**: Building damage, access disruption
- **Hurricanes/Typhoons**: Flooding, wind damage, power outages
- **Tsunamis**: Coastal area damage, power and communications disruption

**Mitigation Strategies:**
- Insurance coverage (casualty, business interruption)
- Physical protection systems (lightning rods, surge protectors)
- Geographic site selection considerations
- Backup and recovery planning

**Special Considerations:**
- **Electrostatic Discharge (ESD)**: Can damage electronic components (as little as 10 volts)
- **Dust Contamination**: Reduces cooling effectiveness, causes component failures
- **Solar Activity**: Affects satellites and power grids

#### **5. Human Error or Failure**
The greatest threat to information security - employees are closest to the information.

**Common Human Errors:**
- Accidental data disclosure
- Incorrect data entry
- Accidental deletion or modification
- Failure to follow procedures
- Poor training or inexperience

**Famous Examples:**
- 1997 Internet router table update error (45% of Internet users affected)
- 1997 corrupt database upload to root domain servers
- Metro-North railroad power loss (2014)
- Telstra communications outage (2016)

**Prevention Measures:**
- Training and awareness programs
- Dual-approval controls
- Expert systems monitoring
- Clear procedures and policies

**Humorous Acronyms:**
- PEBKAC: Problem exists between keyboard and chair
- PICNIC: Problem in chair, not in computer
- ID-10-T error: Idiot

#### **6. Information Extortion**
- **Definition**: Attackers steal or interrupt access to information and demand compensation for return or non-disclosure
- **Cyberextortion**: Using technology to extort organizations
- **Ransomware**: Malware that encrypts data and demands payment for decryption key

**Types of Ransomware:**
- **Lockscreen Ransomware**: Denies access to desktop
- **Encryption Ransomware**: Encrypts hard drive files

**Famous Cases:**
- CD Universe: Russian hacker Maxus stole credit card numbers, demanded $100,000
- Express Scripts: Hacker demonstrated access to 75 records, claimed millions more
- New York Life: Anthony Digati threatened spam attack, demanded $200,000

#### **7. Sabotage or Vandalism**
Deliberate sabotage of computer systems or business operations.

**Types of Online Activism:**
- **Hacktivism/Cyberactivism**: Using hacking to protest organizations or policies
- **Web Site Defacement**: Modifying websites to damage organization's image
- **Cyberterrorism**: Politically motivated attacks against information systems
- **Cyberwarfare**: Government-sanctioned offensive operations

**Cyberterrorism Definition:**
"Premeditated, politically motivated attacks against information, computer systems, computer programs, and data which result in violence against noncombatant targets by subnational groups or clandestine agents" - Mark Pollitt, FBI

**Examples:**
- NATO website defacement during Kosovo war
- 2002 DDoS attack on 13 root DNS servers
- 2007 DNS server attacks
- China's Cyber Blue Team (nation-sponsored cyberterrorism)

#### **8. Software Attacks**
Deliberate software designed to attack systems.

**Malware Categories:**
- **Virus**: Code attached to programs that replicates and spreads
- **Worm**: Self-replicating malware that spreads independently
- **Trojan Horse**: Malicious software disguised as legitimate programs
- **Spyware**: Software that secretly gathers user information
- **Adware**: Malware providing undesired marketing content

**Virus Types:**
- **Macro Virus**: Embedded in document macros
- **Boot Virus**: Infects boot sector or Master Boot Record
- **Memory-Resident Virus**: Installs in system memory
- **Non-Memory-Resident Virus**: Terminates after execution

**Famous Malware Examples:**
- **MyDoom (2004)**: 2 million systems infected, $38 billion damage
- **ILOVEYOU (2000)**: 10% of Internet affected, $5.5 billion damage
- **Code Red (2001)**: 400,000 servers infected, $2.6 billion damage
- **Melissa (1999)**: Macro virus, $300-600 million damage

**Attack Vectors:**
- IP scan and attack
- Web browsing exploitation
- Unprotected network shares
- Mass email distribution
- SNMP vulnerabilities

**Other Software Attacks:**
- **Denial-of-Service (DoS)**: Overwhelming target with requests
- **Distributed DoS (DDoS)**: Coordinated attack from multiple locations
- **Back Doors**: Unauthorized access mechanisms
- **Polymorphic Threats**: Malware that changes to avoid detection

#### **9. Technical Hardware Failures or Errors**
Equipment defects causing unreliable service or lack of availability.

**Famous Hardware Failures:**
- **Intel Pentium FDIV Bug**: Floating-point division error, $475 million loss
- **Intel Xeon Chip**: Hardware errors in 1998
- **Mean Time Between Failure (MTBF)**: Average time between hardware failures
- **Mean Time to Failure (MTTF)**: Average time until next failure

**Hard Drive Statistics:**
- Most commonly failing hardware component
- Average MTBF: approximately 500,000 hours

#### **10. Technical Software Failures or Errors**
Software bugs and programming errors.

**The OWASP Top 10 (2013):**
1. Injection
2. Broken authentication and session management
3. Cross-site scripting (XSS)
4. Insecure direct object references
5. Security misconfiguration
6. Sensitive data exposure
7. Missing function level access control
8. Cross-site request forgery (CSRF)
9. Using components with known vulnerabilities
10. Unvalidated redirects and forwards

**The 24 Deadly Sins in Software Security:**
1. **Buffer Overruns**: More data sent than buffer can handle
2. **Catching Exceptions**: Improper handling of unusual situations
3. **Command Injection**: Unvalidated command input
4. **Cross-Site Scripting (XSS)**: Malicious code insertion in web applications
5. **Failure to Handle Errors**: Poor error management
6. **Failure to Protect Network Traffic**: Unencrypted communications
7. **Failure to Store and Protect Data Securely**: Weak access controls
8. **Failure to Use Cryptographically Strong Random Numbers**: Predictable randomness
9. **Format String Problems**: Using untrusted data as format strings
10. **Improper File Access**: Insecure file handling
11. **Improper Use of SSL**: Misconfigured secure communications
12. **Information Leakage**: Unintentional information disclosure
13. **Integer Bugs**: Overflow/underflow/truncation errors
14. **Neglecting Change Control**: Poor version and change management
15. **Poor Usability**: Security measures that are too difficult to use
16. **Race Conditions**: Unexpected event ordering causing conflicts
17. **SQL Injection**: Unvalidated database queries
18. **Trusting Network Address Resolution**: DNS vulnerabilities
19. **Unauthenticated Key Exchange**: Insecure cryptographic key distribution
20. **Use of Magic URLs and Hidden Forms**: Sensitive data in URLs/forms
21. **Use of Weak Password-Based Systems**: Insufficient password controls
22. **Web Client-Related Vulnerabilities**: Client-side XSS
23. **Web Server-Related Vulnerabilities**: Server-side security issues
24. **Zero-Day Attacks**: Exploiting unknown vulnerabilities

#### **11. Technological Obsolescence**
Outdated infrastructure leading to unreliable systems.

**Examples:**
- Symantec antivirus software retirement
- Microsoft Windows XP end-of-support (April 2014)
- Legacy systems in critical infrastructure

**Impact:**
- Loss of vendor support
- Security vulnerabilities
- Compatibility issues
- Increased maintenance costs

#### **12. Theft**
Illegal taking of property (physical, electronic, or intellectual).

**Types of Theft:**
- **Physical Theft**: Stealing hardware or physical media
- **Electronic Theft**: Stealing digital information
- **Intellectual Property Theft**: Stealing proprietary information

**Mobile Device Risks:**
- Smartphones, tablets, laptops increase theft risk
- Stored credentials allow access to accounts
- Data often more valuable than device

---

## 🔐 **PASSWORD ATTACKS**

### **Types of Password Attacks**
1. **Brute Force**: Trying every possible password combination
2. **Dictionary**: Using common passwords and personal information
3. **Rainbow Tables**: Using precomputed hash tables
4. **Social Engineering**: Tricking users into revealing passwords

### **Password Strength Analysis**
**Case-Insensitive Passwords (26 characters):**
- 8 characters: 1.01 seconds to crack
- 12 characters: 5.3 days to crack
- 16 characters: 6,672.9 years to crack

**Case-Sensitive with Numbers and Special Characters (72 characters):**
- 8 characters: 2.7 hours to crack
- 12 characters: 14,141.9 years to crack
- 16 characters: 639,384,942,170.1 years to crack

### **The 10.4 Password Rule**
- At least 10 characters long
- At least one uppercase letter
- At least one lowercase letter
- At least one number
- At least one special character

---

## 📧 **EMAIL AND COMMUNICATION ATTACKS**

### **Email Attack Types**
- **Spam**: Unsolicited commercial email
- **Mail Bomb**: Overwhelming target with excessive email
- **Phishing**: Fraudulent emails to obtain sensitive information
- **Spear Phishing**: Targeted phishing attacks
- **Whaling**: Phishing targeting senior executives

### **Communications Interception Attacks**
- **Packet Sniffer**: Monitoring network traffic
- **Spoofing**: Forging source addresses
- **Pharming**: Redirecting legitimate traffic to fake sites
- **Man-in-the-Middle**: Intercepting and modifying communications
- **TCP Hijacking**: Taking over established sessions

---

## 🛡️ **PROTECTION STRATEGIES**

### **General Protection Approaches**
1. **Layered Security**: Multiple security controls
2. **Defense in Depth**: Multiple layers of protection
3. **Risk Management**: Identifying and mitigating threats
4. **Incident Response**: Prepared response to security incidents
5. **Business Continuity**: Maintaining operations during disruptions

### **Specific Control Types**
- **Technical Controls**: Hardware and software security measures
- **Administrative Controls**: Policies, procedures, and training
- **Physical Controls**: Physical security measures
- **Managerial Controls**: Oversight and governance

---

## 📊 **THREAT STATISTICS AND TRENDS**

### **2015 SEC/CISE Survey Results**
**Top Internal Threats:**
1. Inability/unwillingness to follow established policy (66%)
2. Disclosure due to insufficient training (63%)
3. Unauthorized access or escalation of privileges (63%)

**Top External Threats:**
1. Unauthorized information collection/data sniffing (71%)
2. Unauthorized access or escalation of privileges (69%)
3. Web site defacement (64%)

**General Threats to Information Assets:**
1. Electronic phishing/spoofing attacks (79%)
2. Malware attacks (73%)
3. Unintentional employee/insider mistakes (70%)

---

## 🔍 **CASE STUDIES AND EXAMPLES**

### **The SLS Case Study**
- **Scenario**: Fred Chin (CEO), Gladys Williams (CIO), Charlie Moody (new CISO)
- **Problem**: Recurring malware outbreaks affecting company operations
- **Solution**: Formal information security program with risk management
- **Key Points**: Management commitment, cost-benefit analysis, organizational change

### **Famous Security Incidents**
- **Kevin Mitnick**: Social engineering attacks, phone system hacking
- **Edward Snowden**: Classified document leaks, NSA contractor
- **Mafiaboy (Michael Calce)**: DDoS attacks on major websites
- **Robert Morris**: Internet worm (1988), first major worm incident

---

## 💡 **KEY INSIGHTS AND PRINCIPLES**

### **Management Principles**
- Information security is primarily a management issue, not just technical
- Requires organizational commitment and cultural change
- Success depends on people, processes, and technology integration
- Cost-benefit analysis essential for security investments

### **Threat Management**
- Threats are always present; attacks occur when vulnerabilities are exploited
- Human error is the greatest security threat
- Multiple threat categories often overlap in real attacks
- Regular threat assessment and monitoring essential

### **Security Implementation**
- Security must be balanced with business needs and usability
- Layered approach provides better protection than single controls
- Regular updates and patches critical for software security
- Training and awareness programs essential for human factor management

---

## 📝 **STUDY TIPS**

1. **Understand the Big Picture**: Information security protects business operations, not just technology
2. **Learn the Categories**: Memorize the 12 threat categories and their characteristics
3. **Study Real Examples**: Understand how threats manifest in real-world scenarios
4. **Focus on Management**: Remember that security is primarily a management challenge
5. **Practice Application**: Be able to identify threats in given scenarios
6. **Know the Statistics**: Understand the scope and impact of different threats

---

*This study guide covers all major concepts from Chapter 2. Focus on understanding how threats impact business operations and why management involvement is crucial for effective information security programs.*
