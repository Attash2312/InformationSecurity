# Chapter 1: Introduction to Information Security
## Study Guide for Exam Preparation

---

## 📚 LEARNING OBJECTIVES
Upon completion of this chapter, you should be able to:
- Define information security
- Recount the history of computer security and explain how it evolved into information security
- Define key terms and critical concepts of information security
- Explain the role of security in the systems development life cycle
- Describe the information security roles of professionals within an organization

---

## 🔍 KEY DEFINITIONS

### Core Security Terms
- **Security**: A state of being secure and free from danger or harm; the actions taken to make someone or something secure
  - Protection from adversaries (those who would do harm, intentionally or otherwise)
  - Multi-layered system like national security protecting sovereignty, assets, resources, and people
- **Information Security**: Protection of the confidentiality, integrity, and availability of information assets, whether in storage, processing, or transmission, via the application of policy, education, training and awareness, and technology
  - CNSS definition: protection of information and its critical elements, including systems and hardware that use, store, and transmit information
- **Computer Security**: Early term for securing physical location of computer technology; evolved into current concept of information security
- **Communications Security**: Protection of all communications media, technology, and content
- **Network Security**: Subset of communications security; protection of voice and data networking components, connections, and content

### The C.I.A. Triad
- **Confidentiality**: Information protected from disclosure or exposure to unauthorized individuals or systems
  - Ensures only users with rights, privileges, and need to access information can do so
  - Protected by: information classification, secure document storage, security policies, education
  - Closely related to privacy
  - Examples: personal information about employees, customers, patients
- **Integrity**: Information is whole, complete, and uncorrupted
  - Threatened by corruption, damage, destruction, or disruption of authentic state
  - Can occur during storage or transmission
  - Detected by: file integrity checks (file size changes), file hashing algorithms
  - Hash values: unique numbers computed from file bit values
- **Availability**: Information accessible and correctly formatted for use without interference or obstruction
  - Enables authorized users (people or computer systems) to access information
  - Must be in required format (e.g., book written in English)
  - Example: research library requiring identification before entrance

### Expanded Information Characteristics
- **Accuracy**: Information is free from mistakes or errors and has the value the end user expects
  - Intentionally or unintentionally modified information is no longer accurate
  - Examples: incorrect bank balance from teller error or customer mistake
- **Authenticity**: Information is genuine or original, not reproduced or fabricated
  - Information in same state as when created, placed, stored, or transferred
  - Email spoofing problem: modified sender address fools recipients
- **Utility**: Information has value for some purpose or end
  - Information must serve a purpose and be in meaningful format
  - Example: Census data overwhelming for citizens but valuable for politicians
- **Possession**: Quality or state of ownership or control of information
  - Independent of format or other characteristics
  - Breach of confidentiality always results in breach of possession
  - Breach of possession doesn't always lead to breach of confidentiality
  - Example: encrypted tape backup stolen (breach of possession) but data still confidential

---

## 📜 HISTORICAL TIMELINE

### Early Years (1940s-1960s)
- **World War II**: First mainframe computers used for code-breaking (Enigma machine)
  - Multiple levels of security implemented to protect devices and missions
  - Required new processes and tried-and-true methods for data confidentiality
  - Access controlled by badges, keys, and facial recognition by security guards
- **Physical Security Focus**: Protection of physical locations, equipment theft, espionage
- **1960s**: ARPANET development by Dr. Larry Roberts (1968)
  - Created to support military's exchange of information
  - Evolved into what we now know as the Internet
  - Figure 1-2 shows excerpt from his Program Plan
- **Early Problem**: Password file printed on every output file due to software glitch
  - Systems administrator working on MOTD (message of the day) file
  - Another administrator editing password file simultaneously
  - Software glitch mixed the two files

### Key Historical Milestones

#### 1960s-1970s
- **1967**: ARPA task force formed to study securing classified information systems
  - Assembled in October 1967, met regularly to formulate recommendations
  - Recommendations became contents of RAND Report R-609
- **1970**: RAND Report R-609 - First document defining computer security controls
  - Written by Willis H. Ware for Department of Defense
  - Classified for almost ten years, declassified in 1979
  - Identified role of management and policy issues in computer security
  - Expanded scope from physical locations to: securing data, limiting unauthorized access, involving multiple organizational levels
- **1973**: Robert Metcalfe identified ARPANET security problems
  - Creator of Ethernet, knew individual remote sites lacked sufficient controls
  - Problems identified: vulnerable password structure, lack of safety procedures for dial-up connections, nonexistent user identification and authorizations
  - Phone numbers publicly displayed on phone booth walls gave hackers easy access
  - Network security commonly called "network insecurity"

#### 1970s-1980s
- **1978**: "Protection Analysis: Final Report" by Bisbey and Hollingworth
  - USC Information Sciences Institute researchers
  - Focused on ARPA project to understand and detect vulnerabilities in operating system security
  - Examined automated vulnerability detection techniques
- **1979**: Morris and Thompson's "Password Security: A Case History"
  - Examined design history of password security scheme on remotely accessed, time-sharing system
- **1982**: Dennis Ritchie's "On the Security of UNIX"
  - Discussed secure user IDs, secure group IDs, and inherent system problems
- **1984**: First version of Trusted Computer Security (TCSEC) documents
  - Known as the "Rainbow Series"
  - Published by U.S. Department of Defense Computer Security Evaluation Center
- **1986**: Computer Fraud and Abuse Act
- **1987**: Computer Security Act
- **1988**: CERT (Computer Emergency Response Team) created by DARPA

### Modern Era (1990s-Present)
- **1980s-1990s**: Microprocessor brought personal computers
  - Decentralization of data processing systems
  - Rise of networking - interconnecting PCs and mainframes
  - TCP/IP protocols developed for ARPANET (became Internet protocols)
  - DNS (Domain Name System) developed
  - First dial-up ISP "The World" came online
- **1990s**: Internet becomes public; networks of computers become common
  - Internet made available to general public after decades of government/academic use
  - Connectivity reached virtually all computers via phone lines or LANs
  - Commercialization brought technology to every corner of the globe
  - Early Internet deployment treated security as low priority
  - Problems plaguing email today result from early lack of security
- **1993**: First DEFCON conference in Las Vegas
  - Gathering for information security professionals, authors, lawyers, government employees, law enforcement
  - Exchange between "white hats" (law enforcement/security) and "black hats" (hackers)
- **Late 1990s-2000s**: Large corporations integrate security publicly
  - Antivirus products became extremely popular
  - Information security emerged as independent discipline
- **2000s**: Growing awareness of cyberattacks; nation-state threats
  - Internet connects millions of unsecured networks and billions of computer systems
  - Security of each computer contingent on security of every connected computer
  - Growing threat of cyberattacks on utilities and critical infrastructure
  - Nation-state information warfare concerns
  - Business and personal information systems could become casualties
- **Post-9/11**: USA PATRIOT Act and related legislation
  - USA PATRIOT Act of 2001
  - USA PATRIOT Improvement and Reauthorization Act of 2005
  - PATRIOT Sunsets Act of 2011
  - USA FREEDOM Act

---

## 🏗️ INFORMATION SYSTEM COMPONENTS

### Six Critical Components
1. **Software**: Applications, operating systems, command utilities
   - Most difficult component to secure
   - Exploitation of programming errors accounts for substantial attacks
   
2. **Hardware**: Physical technology that houses and executes software
   - Physical security policies protect from harm or theft
   - Laptop thefts in airports (pre-9/11 example)
   
3. **Data**: Information stored, processed, and transmitted
   - Most valuable asset of an organization
   - Main target of intentional attacks
   
4. **People**: Often overlooked but can be the weakest link
   - Social engineering exploits human nature
   - "Bribing the gatekeeper" example from Chinese history
   
5. **Procedures**: Written instructions for accomplishing tasks
   - Bank consultant wire fraud example ($10+ million loss)
   - Must be protected and disseminated on need-to-know basis
   
6. **Networks**: Interconnecting systems (LANs, Internet)
   - Created need for increased computer security
   - Network security essential (firewalls, intrusion detection)

---

## 🎯 KEY SECURITY CONCEPTS

### Threat Terminology
- **Threat**: Any event or circumstance that has potential to adversely affect operations and assets
  - Always present, can be purposeful or undirected
  - Examples: hackers (purposeful), severe storms (undirected)
- **Threat Agent**: Specific instance or component of a threat (e.g., "external professional hacker")
  - Kevin Mitnick example: convicted hacker who broke into phone systems
  - Lightning strike, hailstorm, tornado are threat agents of "acts of God/acts of nature"
- **Threat Source**: Category of objects, people, or entities representing origin of danger
  - Category of threat agents (e.g., "acts of trespass or espionage")
- **Attack**: Intentional or unintentional act that can damage or compromise information
  - Can be active or passive, intentional or unintentional, direct or indirect
  - Active: hacker attempting to break into system
  - Passive: casually reading sensitive information
  - Unintentional: lightning strike causing building fire
  - Direct: hacker using PC to break into system
  - Indirect: hacker compromising system to attack other systems (botnet)
- **Vulnerability**: Potential weakness in an asset or its defensive control system
  - Examples: flaw in software package, unprotected system port, unlocked door
  - Can be examined, documented, published, or remain latent (undiscovered)
- **Exploit**: Technique used to compromise a system
  - Can be verb (to exploit) or noun (the exploit)
  - Can use existing software tools or custom-made software components
  - Example: script from MadHackz website
- **Asset**: Organizational resource being protected (logical or physical)
  - Logical: website, software information, data
  - Physical: person, computer system, hardware, tangible object
  - Focus of what security efforts are attempting to protect

### Risk and Loss
- **Risk**: Probability of an unwanted occurrence
  - Organizations must minimize risk to match their risk appetite
  - Risk appetite: quantity and nature of risk organization is willing to accept
- **Loss**: Single instance of information asset suffering damage, destruction, or unauthorized disclosure
  - Examples: information stolen, unintended modification, denial of use
- **Exposure**: Condition when a vulnerability is known to an attacker
  - State of being exposed

### Additional Key Concepts
- **Access**: Subject or object's ability to use, manipulate, modify, or affect another subject or object
  - Authorized users have legal access, hackers gain illegal access
  - Access controls regulate this ability
- **Control/Safeguard/Countermeasure**: Security mechanisms, policies, or procedures
  - Can successfully counter attacks, reduce risk, resolve vulnerabilities
  - Improve security within organization
- **Protection Profile/Security Posture**: Entire set of controls and safeguards
  - Includes policy, education, training and awareness, and technology
  - Sometimes used interchangeably with "security program"
- **Subjects and Objects of Attack**: Computer can be either
  - Subject: agent entity used to conduct attack
  - Object: target entity of attack
  - Can be both: compromised by attack (object) then used to attack others (subject)

---

## 🔄 SYSTEMS DEVELOPMENT LIFE CYCLE (SDLC)

### Traditional SDLC Phases (Waterfall Model)
1. **Investigation**: 
   - Define problem system being developed to solve
   - Specify objectives, constraints, and scope of project
   - Preliminary cost-benefit analysis
   - Assess economic, technical, and behavioral feasibilities
2. **Analysis**: 
   - Build on information from investigation phase
   - Assess organization, current systems, capability to support proposed systems
   - Determine what new system expected to do and how it will interact with existing systems
   - Document findings and update feasibility analysis
3. **Logical Design**: 
   - Create blueprint for desired solution (implementation independent)
   - Based on business need: select applications, choose data support structures, delineate technologies
   - Generate cost and benefit estimates for comparison of options
   - Perform feasibility analysis
4. **Physical Design**: 
   - Select specific technologies to support alternatives from logical design
   - Make-or-buy decision: develop in-house or purchase from vendor
   - Final designs integrate various components and technologies
   - Feasibility analysis and management approval
5. **Implementation**: 
   - Create needed software
   - Order, receive, and test components
   - Train users and create supporting documentation
   - Install and test as complete system
   - Performance review and acceptance test
6. **Maintenance and Change**: 
   - Longest and most expensive phase
   - Support and modify system for remainder of useful life cycle
   - Periodic testing for compliance
   - Evaluate feasibility of continuance vs. discontinuance
   - Manage upgrades, updates, and patches

### Modern Development Approaches
- **JAD (Joint Application Development)**: 
  - Broader cross-section of organization in development process
  - Management team members from supported business unit
  - Future users of systems being created
- **RAD (Rapid Application Development)**: 
  - Increase speed of requirements collection and software prototyping
  - More iterations in design process
- **Spiral Method**: 
  - Each stage completed in smaller increments
  - Working software components delivered more frequently
  - Software comes closer to finished state with each pass
- **Agile/XP (Extreme Programming)**: 
  - Collective approach including Kanban and Scrum
  - Reduce time from gathering requirements to testing software
  - Faster feedback cycles to reduce time to market
- **DevOps**: 
  - Integrate development team and operations team efforts
  - Improve functionality and security of applications
  - Continuous development model with systems thinking
  - Short feedback loops and continuous experimentation
- **SecOps**: 
  - DevOps methodologies applied to security control systems
  - Integrated development and operations approach for security

### Software Assurance (SA)
- **Definition**: Methodological approach to develop software free of vulnerabilities
- **Goal**: Build security into development life cycle rather than address at later stages
- **U.S. Department of Defense Initiative (2003)**:
  - Led by Joe Jarzombek
  - Endorsed by Department of Homeland Security (2004)
  - Resulted in SwA CBK publication
- **SwA CBK (Secure Software Assurance Common Body of Knowledge)**:
  - Working group from industry, government, and academia
  - Two key questions: What engineering activities achieve secure software? What knowledge is needed?
  - Sections: Nature of Dangers, Fundamental Concepts, Ethics/Law/Governance, Requirements, Design, Construction, Verification/Validation, Tools/Methods, Processes, Project Management, Acquisition, Sustainment

### Software Design Principles (Saltzer & Schroeder, 1975)
1. **Economy of mechanism**: Keep design as simple and small as possible
2. **Fail-safe defaults**: Base access decisions on permission rather than exclusion
3. **Complete mediation**: Every access to every object must be checked for authority
4. **Open design**: Design should not be secret, depend on possession of keys/passwords
5. **Separation of privilege**: Protection mechanism should require two keys to unlock
6. **Least privilege**: Every program and user should operate with least set of privileges necessary
7. **Least common mechanism**: Minimize mechanisms common to multiple users
8. **Psychological acceptability**: Human interface designed for ease of use

### NIST SDLC Phases
1. **Initiation**: 
   - Initial delineation of business requirements (confidentiality, integrity, availability)
   - Information categorization and special handling requirements
   - Determination of privacy requirements
   - Security discussions as part of development project
2. **Development/Acquisition**: 
   - Conduct risk assessment and supplement baseline security controls
   - Analyze security requirements
   - Perform functional and security testing
   - Prepare initial documents for system certification and accreditation
   - Design security architecture
3. **Implementation/Assessment**: 
   - Integrate information system into operational environment
   - Plan and conduct system certification activities
   - Complete system accreditation activities
   - Risk Management Framework (RMF) replaces former C&A approach
4. **Operation/Maintenance**: 
   - Conduct operational readiness review
   - Manage system configuration
   - Institute processes for assured operations and continuous monitoring
   - Perform reauthorization as required
5. **Disposal**: 
   - Build and execute disposal/transition plan
   - Archive critical information
   - Sanitize media
   - Dispose of hardware and software

### Microsoft Security Development Lifecycle (SDL)
- **7 phases, 16 steps**:
  1. Training (Core security training)
  2. Requirements (Establish security requirements, create quality gates/bug bars, perform security and privacy risk assessments)
  3. Design (Establish design requirements, perform attack surface analysis/reduction, use threat modeling)
  4. Implementation (Use approved tools, deprecate unsafe functions, perform static analysis)
  5. Verification (Perform dynamic analysis, perform fuzz testing, conduct attack surface review)
  6. Release (Conduct final security review, certify release and archive)
  7. Response (Create incident response plan, execute incident response plan)

---

## 👥 ORGANIZATIONAL ROLES

### Senior Management
- **CEO**: Chief Executive Officer
- **CIO**: Chief Information Officer 
  - Advises CEO, president, or company owner on strategic planning for information management
  - Translates strategic plans into strategic information plans for information systems division
  - Works with subordinate managers to develop tactical and operational plans
  - Enables planning and management of systems supporting organization
  - Other titles: VP of information, VP of information technology, VP of systems
- **CISO**: Chief Information Security Officer
  - Primary responsibility for assessment, management, and implementation of information security
  - Other titles: manager for IT security, security administrator
  - Usually reports directly to CIO (may have layers of management in larger organizations)
  - Recommendations must be given equal or greater priority than other technology proposals
  - Common placement and accountabilities subject of current industry debate

### Information Security Project Team
- **Champion**: Senior executive who promotes project and ensures support
  - Provides financial and administrative support at highest organizational levels
  - Role cannot be overstated - moves project forward, ensures proper management
  - Pushes for acceptance throughout organization
- **Team Leader**: Project manager with technical and personnel management skills
  - May be departmental line manager or staff unit manager
  - Understands project management, personnel management, and information security technical requirements
- **Security Policy Developers**: Understand organizational culture and requirements
  - Knowledge of existing policies and requirements for developing successful policies
- **Risk Assessment Specialists**: Financial risk assessment, asset valuation
  - Understand financial risk assessment techniques
  - Know value of organizational assets and security methods to be used
- **Security Professionals**: Dedicated, trained specialists
  - Well-educated specialists in all aspects of information security (technical and non-technical)
- **Systems Administrators**: Administer systems housing organizational information
  - Primary responsibility for administering systems that house organizational information
- **End Users**: Directly affected by new system
  - Selection from various departments, levels, and degrees of technical knowledge
  - Help team focus on realistic controls that don't disrupt essential business activities
  - Most directly affected by process and outcome of project
  - Must be included in information security process
  - Key end users assigned to Joint Application Development (JAD) team

### Data Responsibilities
- **Data Owners**: Senior management responsible for security and use of information
  - Members of senior management who control particular set of information
  - Determine level of data classification and changes required by organizational change
  - Work with subordinate managers to oversee day-to-day administration of data
- **Data Custodians**: Work with data owners; responsible for storage, maintenance, protection
  - Work directly with data owners
  - Responsible for information and systems that process, transmit, and store it
  - May be dedicated position (CISO) or additional responsibility of systems administrator
  - Duties: oversee data storage and backups, implement procedures and policies from security plans
  - Report to data owner
- **Data Users**: Everyone in organization responsible for data security
  - Internal and external stakeholders (customers, suppliers, employees)
  - Interact with information in support of their organization's planning and operations
  - Everyone in organization is responsible for security of data

### Communities of Interest
1. **Information Security Management and Professionals**:
   - Aligned with goals and mission of information security community
   - Job functions focus on protecting organization's information systems and stored information from attacks
2. **Information Technology Management and Professionals**:
   - IT managers and skilled professionals in systems design, programming, networks
   - Focus on costs of system creation and operation, ease of use for users, timeliness of creation
   - Goals not always in complete alignment with information security community
   - May cause conflict depending on organizational structure
3. **Organizational Management and Professionals**:
   - General management team and rest of personnel in organization
   - Made up of subsets: executive management, production management, human resources, accounting, legal staff
   - IT community categorizes as "users of information technology systems"
   - Information security community categorizes as "security subjects"
   - Serves as reminder that IT systems and information security objectives exist to further organizational objectives
   - Most efficient and secure IT systems have no value if not useful to organization as whole

---

## 🎨 SECURITY AS ART, SCIENCE, AND SOCIAL SCIENCE

### Security as Art
- **No hard and fast rules** for security mechanism installation
- **No universally accepted complete solutions**
- **Administrators like artists** applying oils to canvas
  - Touch of color here, brush stroke there
  - Just enough to represent image without overwhelming viewer
  - Without overly restricting user access
- **Complex interactions** among users, policy, and technology controls
- **No manual** can help implement security throughout entire interconnected system
- **Security artisans**: Technologists with gift for managing and operating computers

### Security as Science
- **Specific conditions cause virtually all actions** in computer systems
- **Technology developed for rigorous performance levels** by computer scientists and engineers
- **Almost every fault, security hole, and systems malfunction** is result of interaction of specific hardware and software
- **Best practices, standards of due care, and tried-and-true methods** minimize guesswork
- **Recognized and approved security methods and techniques** provide sound technical security advice
- **Faults remain** usually due to technology malfunctioning for various reasons
- **With sufficient time**, developers could resolve and eliminate all faults

### Security as Social Science
- **Examines behavior of people** interacting with systems (societal systems or information systems)
- **Information security begins and ends with people** inside organization and those who interact with system
- **End users may be weakest link** in security chain
- **"It's not a bug, it's a feature!"** - systems perform as designed but not as expected
  - Users don't have skills to use system effectively
  - Attackers learn unintended ways to use systems
  - Take advantage of unintended functions or operations
- **Human side of systems** is not exact, unlike the science
- **Understanding behavioral aspects** of organizational science and change management
- **Security administrators can reduce risk** caused by end users
- **Create more acceptable and supportable security profiles**
- **Appropriate policy and training** can substantially improve end user performance
- **Result in more secure information system**

---

## 📋 CASE STUDIES & EXAMPLES

### SLS Company Incident (Opening Scenario)
- **Scenario**: Help desk employee Amy receives suspicious email attachment
  - Email from Davey Martinez with subject "Wait till you see this"
  - Message body: "Funniest joke you'll see today"
  - Amy clicked file attachment icon, nothing happened initially
  - Company systems began failing: 47 new emails, systems unresponsive, no dial tone
- **Problem**: Email worm/virus spreads through company systems
  - Bob's PC acting weird, email program not responding
  - Erin Williams reporting similar issues
  - Charlie Moody (server admin) looking frantic
  - Help desk ticket system down, no tracking system
- **Lessons**: 
  - Importance of user training about malicious email attachments
  - Need for incident response planning
  - Management confusion about containing incidents
  - Technical support staff need security awareness

### Historical Examples
- **Enigma Machine**: German encryption device broken by Allies in WWII
  - Earlier versions broken by Poles in 1930s
  - British and Americans broke later, more complex versions
  - Submarine (Unterseeboot) version caused considerable anguish
  - Information used to anticipate German armed forces actions
- **ARPANET**: Early network with security vulnerabilities
  - Developed by Dr. Larry Roberts in 1968
  - Robert Metcalfe identified fundamental security problems in 1973
  - Individual remote sites lacked sufficient controls and safeguards
  - Phone numbers widely distributed on phone booth walls
- **MULTICS**: First operating system to integrate security into core functions
  - Multiplexed Information and Computing Service
  - Mainframe, time-sharing operating system
  - Developed mid-1960s by GE, Bell Labs, and MIT consortium
  - Implemented multiple security levels and passwords
- **UNIX**: Developed from MULTICS, initially lacked security features
  - Created in 1969 by Ken Thompson, Dennis Ritchie, Rudd Canaday, Doug McIlroy
  - Primary function was text processing (didn't require same security level)
  - Password function not added until early 1970s

### Real-World Breaches
- **Georgia Secretary of State (2015)**: 
  - 6+ million voters' private information including Social Security numbers
  - Caused by employee failing to follow established policies and procedures
  - Employee fired, agency claimed to recover all copies sent to 12 organizations
- **GE Money (2008)**:
  - Data backup tape with credit card data from 650,000 customers
  - 150,000+ Social Security numbers missing from Iron Mountain storage facility
  - Approximately 230 retailers affected
- **ChoicePoint (2004)**:
  - Personal information of 145,000 people released to identity thieves
  - Criminals used stolen identities to create legitimate business entities
  - Subscribed to ChoicePoint to acquire data fraudulently
  - No network or computer-based attacks used - simple fraud
- **Eli Lilly (2001)**:
  - Email addresses of 600 patients released to each other
  - ACLU denounced breach of privacy
  - Caused by programming error when patients signed up for email service
  - Influenced public debate on privacy legislation

### Airport Laptop Theft Example
- **Pre-9/11**: Common two-person team theft in airports
  - First perpetrator enters security ahead of target
  - Second perpetrator waits behind target
  - As computer goes through scanner, first perpetrator grabs it
  - Second perpetrator slows metal detector process with keys/coins
- **Security Response**: Post-9/11 tightened security but theft still possible
- **Value**: Laptops worth few thousand dollars, but information stored worth much more
- **Risk**: Privileged access to cloud-based data stores if not quickly revoked

---

## ❓ EXAM-TYPE QUESTIONS

### Multiple Choice Questions

**Q1: What are the three components of the C.I.A. triad?**
A) Cost, Impact, Assessment
B) Confidentiality, Integrity, Availability
C) Control, Implementation, Administration
D) Compliance, Investigation, Authorization

**Q2: Which document is considered the foundation of computer security studies?**
A) NIST SP 800-12
B) RAND Report R-609
C) RFC 2828
D) FIPS 140-2

**Q3: What was the first operating system to integrate security into its core functions?**
A) UNIX
B) MULTICS
C) Windows NT
D) Linux

**Q4: In the SDLC, which phase is typically the longest and most expensive?**
A) Investigation
B) Analysis
C) Implementation
D) Maintenance and Change

**Q5: Who is ultimately responsible for the security and use of information in an organization?**
A) Data Custodians
B) Data Users
C) Data Owners
D) Systems Administrators

### Short Answer Questions

**Q1: Explain the difference between a threat and a threat agent.**

**Q2: List and briefly describe the six components of an information system.**

**Q3: Why is the top-down approach to information security implementation superior to the bottom-up approach?**

**Q4: What is the McCumber Cube and what does it represent?**

**Q5: Describe the relationship between MULTICS and the early development of computer security.**

### Essay Questions

**Q1: Compare and contrast the traditional SDLC with modern development approaches like Agile and DevOps. What are the security implications of each approach?**

**Q2: Analyze the SLS case study. What went wrong, and what security measures should have been in place to prevent or mitigate the incident?**

**Q3: Explain how information security can be viewed as both an art and a science. Provide examples to support your argument.**

**Q4: Discuss the evolution of information security from its origins in computer security to the modern concept. What factors drove this evolution?**

---

## 🔑 KEY TAKEAWAYS FOR EXAM

1. **Information security evolved from computer security** 
   - Started with physical protection of mainframe computers during WWII
   - Expanded from physical locations to include data, networks, and people
   - RAND Report R-609 was pivotal document expanding scope

2. **C.I.A. triad is fundamental but incomplete**
   - Confidentiality, Integrity, Availability are core principles
   - Expanded model includes Accuracy, Authenticity, Utility, Possession
   - Each characteristic affects information's value

3. **Information systems have six components**
   - Software (most difficult to secure), Hardware, Data (most valuable asset)
   - People (often weakest link), Procedures, Networks (created security challenges)

4. **Top-down approach is superior to bottom-up**
   - Management support and champion are crucial for success
   - Higher probability of success with upper-level management initiation
   - Bottom-up approach lacks participant support and organizational staying power

5. **SDLC integration is critical**
   - Security must be built into systems from beginning, not added later
   - Traditional waterfall model vs. modern approaches (Agile, DevOps, SecOps)
   - Software Assurance (SA) builds security into development life cycle

6. **People are often the weakest link**
   - Social engineering exploits human nature
   - Training and awareness are essential
   - "Bribing the gatekeeper" example from Chinese history

7. **Historical context matters**
   - Understanding evolution helps understand current challenges
   - Key milestones: ARPANET, MULTICS, UNIX, Internet commercialization
   - Modern threats: nation-state attacks, critical infrastructure concerns

8. **Multiple perspectives needed**
   - Security as art (no hard rules), science (specific conditions), and social science (human behavior)
   - Balance between protection and usability is key

9. **Organizational roles are clearly defined**
   - Data Owners (senior management), Data Custodians (technical implementation), Data Users (everyone)
   - CIO, CISO roles and responsibilities
   - Three communities of interest with different priorities

10. **Perfect security is impossible**
    - Information security is a process, not a goal
    - Balance between security and access is essential
    - "An ounce of prevention is worth a pound of cure"

## 🔄 BALANCING INFORMATION SECURITY AND ACCESS

### The Security-Access Dilemma
- **Perfect security impossible**: Cannot obtain absolute information security
- **Information security is a process, not a goal**
- **Complete access vs. complete security**:
  - Make system available to anyone, anywhere, anytime = poses danger to security
  - Completely secure system = wouldn't allow anyone access
- **Microsoft TCSEC C-2 example**: Had to remove all networking components and operate only from console in secured room

### Achieving Balance
- **Reasonable access with protection against threats**
- **Security level must allow reasonable access yet protect against threats**
- **End users and security professionals must recognize shared goals**:
  - Ensure data is available when, where, and how needed
  - With minimal delays or obstacles
  - After addressing concerns about loss, damage, interception, or destruction

### Competing Voices
- **CISO**: "Encryption is needed to protect secrets of the organization"
- **User 1**: "Encrypting email is a hassle"
- **User 2**: "Encrypting email slows me down"

---

## 🎲 MCCUMBER CUBE MODEL

### CNSS Security Model
- **Based on**: CNSS document "National Training Standard for Information Systems Security Professionals, NSTISSI No. 4011 (1994)"
- **Organization**: Committee on National Security Systems (CNSS)
- **Original name**: National Security Telecommunications and Information Systems Security Committee (NSTISSC)
- **Established**: 1990 by National Security Directive (NSD) 42
- **Expected replacement**: NIST SP 800-16 Rev. 1 (2014)

### McCumber Cube Details
- **Created by**: John McCumber in 1991
- **Also known as**: McCumber Cube
- **Structure**: 3 × 3 × 3 cube with 27 cells
- **Three dimensions**:
  1. **Information Characteristics**: Confidentiality, Integrity, Availability
  2. **Information States**: Storage, Processing, Transmission
  3. **Security Measures**: Policy, Education, Technology

### Cube Components
- **Each of 27 areas must be properly addressed** during security process
- **Example intersection**: Technology, Integrity, and Storage
  - Requires controls addressing need to use technology to protect integrity of information while in storage
  - Example control: system for detecting host intrusion that protects integrity by alerting administrators to potential file modification
- **Common omission**: Need for guidelines and policies providing direction for practices and implementations

---

## 📖 ADDITIONAL RESOURCES

### Important Documents
- **RAND Report R-609**: "Security Controls for Computer Systems" - foundation document
- **NIST SP 800-64**: "Security Considerations in the System Development Life Cycle"
- **Microsoft Security Development Lifecycle (SDL)**: 7-phase, 16-step methodology
- **NIST SP 800-12**: "An Introduction to Computer Security: The NIST Handbook"

### Key Figures
- **Dr. Larry Roberts**: ARPANET founder, became known as Internet founder
- **Robert Metcalfe**: Ethernet creator, identified ARPANET security issues, received National Medal of Technology
- **Willis Ware**: Author of RAND Report R-609 for Department of Defense
- **John McCumber**: Creator of McCumber Cube model
- **Ken Thompson, Dennis Ritchie**: UNIX developers from MULTICS project
- **Kevin Mitnick**: Convicted hacker who broke into phone systems

### Organizations
- **CNSS**: Committee on National Security Systems (formerly NSTISSC)
- **NIST**: National Institute of Standards and Technology
- **CERT**: Computer Emergency Response Team (created by DARPA)
- **ARPA/DARPA**: Advanced Research Projects Agency
- **CERT**: Computer Emergency Response Team

### Important Websites and References
- www.packet.cc (Dr. Roberts' website)
- web.mit.edu/multics-history (MULTICS project)
- www.rand.org/pubs/reports/R609-1.html (RAND Report)
- www.microsoft.com/en-us/sdl (Microsoft SDL)
- http://csrc.nist.gov/publications/nistpubs/800-64Rev2/ (NIST SP 800-64)

### Timeline References (Table 1-1 from textbook)
- **1968**: Maurice Wilkes discusses password security
- **1970**: Willis H. Ware authors RAND Report R-609
- **1973**: Schell, Downey, and Popek examine military system security needs
- **1975**: Federal Information Processing Standards examines DES
- **1978**: Bisbey and Hollingworth publish "Protection Analysis: Final Report"
- **1979**: Morris and Thompson author "Password Security: A Case History"
- **1982**: Dennis Ritchie publishes "On the Security of UNIX"
- **1984**: First version of TCSEC documents (Rainbow Series)
- **1992**: Researchers develop Simple Internet Protocol Plus (SIPP) Security protocols (IPSEC)

---

*Remember: Information security is a process, not a goal. Perfect security is impossible, but reasonable security that balances protection with usability is achievable.*
