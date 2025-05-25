Threat modelling is best integrated into the design phase of an SDLC before any code is written. Threat modelling is a structured process of identifying potential security threats and prioritizing techniques to mitigate attacks so that data or assets that have been classified as valuable or of higher risk during risk assessment, such as confidential data, are protected. When performed early, it brings a great advantage; potential issues can be found early and solved, saving fixing costs down the line. 

There are various methods to perform threat modelling. Not all the methods have the same purpose; some focus on risk or privacy concerns, while some are more customer-focused. We can combine these methods to understand potential threats better; it is essential to analyse which way aligns more with the project or business. STRIDE, DREAD, and PASTA are among the common threat modelling methodologies.  

**STRIDE**  

STRIDE stands for Spoofing, Tampering, Repudiation, Information Disclosure, Denial Of Service, and Elevation/Escalation of Privilege. STRIDE is a widely used threat model developed by Microsoft which evaluates the system's design in a more detailed view. We can use STRIDE to identify threats, including the property violated by the threat and definition. The system's data flow diagram is to be developed in this model, and each node is applied with the STRIDE model. Identifying security threats is a manual process that tools are not supported and should be carried out during the risk assessment. Using data flow diagrams and integrating STRIDE, the system entities, attack surfaces, like known boundaries and attacker events become more identifiable. STRIDE is built upon the CIA triad principle (Confidentiality, Integrity & Availability). Security professionals that perform STRIDE are looking to answer "What could go wrong with this system". Here are the components of the framework:

- **Spoofing:** Impersonation of a user by a malicious actor, violating the authentication principle. Examples include ARP, IP, and DNS spoofing.
- **Tampering:** Modification of information by an unauthorized user, violating the integrity principle.
- **Repudiation:** Lack of accountability for actions where responsibility cannot be attributed, violating non-repudiability.
- **Information Disclosure:** Violation of confidentiality, such as in data breaches.
- **Denial of Service:** Exhaustion of resources, preventing authorized users from accessing a system, violating availability.
- **Elevation of Privilege:** Gaining unauthorized access by escalating privileges, violating authorization principles.

![[Pasted image 20250519202418.png]]

**DREAD**  

The abbreviation DREAD stands for five questions about each potential threat: Damage Potential, Reproducibility, Exploitability, Affected Users, and Discoverability. DREAD ranks threats by assigning scores based on their severity and risk probability. Here are its components:

- **Damage:** The potential impact of a threat, scored on a scale of 0–10.
- **Reproducibility:** The complexity of reproducing the threat, scored 0–10.
- **Exploitability:** How easily the threat can be exploited, scored 0–10.
- **Affected Users:** The number of users impacted, scored 0–10.
- **Discoverability:** The ease of discovering the threat, scored 0–10.

**PASTA**  

PASTA stands for Process for Attack Simulation and Threat Analysis. It aligns technical requirements with business objectives and provides a strategic view of threats. PASTA's seven stages are:

- **Define Objectives:** Establish the scope and objectives.
- **Define Technical Scope:** Create architectural diagrams to map the attack surface.
- **Decomposition & Analysis:** Map trust boundaries and evaluate vulnerabilities.
- **Threat Analysis:** Identify potential threats based on intelligence.
- **Vulnerabilities & Weaknesses Analysis:** Assess and mitigate weaknesses.
- **Attack/Exploit Enumeration & Modelling:** Simulate attack paths and vulnerabilities.
- **Risk Impact Analysis:** Document risks and propose mitigation steps.

![[Pasted image 20250519202442.png]]~