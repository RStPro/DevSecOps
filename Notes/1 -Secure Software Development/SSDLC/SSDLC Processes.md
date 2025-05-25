After understanding your security posture, now is the time to prioritise and instil security in your SDLC.
Generally speaking, a secure SDLC involves integrating processes like security testing and other activities into an existing development process.
Examples include writing security requirements alongside functional requirements and performing an architecture risk analysis during the design phase of the SDLC.

These processes are the following:

- **Risk Assessment** - during the early stages of SDLC, it is essential to identify security considerations that promote a security by design approach when functional requirements are gathered in the planning and requirements stages. For example, if a user requests a blog entry from a site, the user should not be able to edit the blog or remove unnecessary input fields.  
- **Threat Modelling** - is the process of identifying potential threats when there is a lack of appropriate safeguards. It is very effective when following a risk assessment and during the design stage of the SDLC, as Threat Modelling focuses on what should not happen. In contrast, design requirements state how the software will behave and interact. For example, ensure there is verification when a user requests account information.
- **Code Scanning / Review** -  Code reviews can be either manual or automated. Code Scanning or automated code reviews can leverage Static and Dynamic Security testing technologies. These are crucial in the Development stages as code is being written.
- **Security Assessments - Like Penetration Testing & Vulnerability Assessments** are a form of automated testing that can identify critical paths of an application that may lead to exploitation of a vulnerability. However, these are hypothetical as the assessment doesn't carry simulations of those attacks. Pentesting, on the other hand, identifies these flaws and attempts to exploit them to demonstrate validity. Pentests and Vulnerability Assessments are carried out during the Operations & Maintenance phase of the SDLC after a prototype of the application.

![[Pasted image 20250519200102.png]]

