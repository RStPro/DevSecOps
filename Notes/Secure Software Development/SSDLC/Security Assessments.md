A security assessment plays a primary role in achieving security in SDLC and should be implemented in all phases where possible.
Security testing assesses a system, software or web application for vulnerabilities and other attack vectors. Because they test from a holistic point of view of the application, they are usually carried out at the end of the SDLC, in the Operations and Maintenance phase, once the version has included all the working components and updates. There are two types of assessments: Penetration Testing and Vulnerability Assessment. 

**Usually, a company employs and authorizes external security testers to attempt to break into a company’s network and systems legally*****

## Vulnerability Assessment

Vulnerability Assessments focus on Finding Vulnerabilities, but do not validate them or simulate the findings to prove they are exploitable in reality. Typically, automated tools run against an organisation's network and systems. Examples of tools: are OpenVAS, Nessus (Tenable), and ISS Scanner. These scanners probe ports and services on systems across various systems and IP Addresses. Other activities include checking service versions against a database of vulnerabilities affecting said version. The result is a report with a list of vulnerabilities usually found, with an automated threat level severity classification, e.g., High/Medium/Low or an assigned CVSS score.  

## Penetration Testing

It Includes Vulnerability Testing but goes more in-depth. It is extended by testing/validating of vulnerabilities, quantifying risks and attempting to penetrate systems. For example, trying to escalate privileges after a vulnerability is found, some vulnerabilities can be a lower risk but can be used as leverage to cause more damage. The tester can provide a thorough report with suggested countermeasures to mitigate the vulnerabilities. This makes it easier to understand the threats by demonstrating the actual risk, for example, recovering an employee password by exploiting the mentioned vulnerability.  

# Pros and Cons

**Vulnerability Assessment**  

|                             Pros                             |                                                                       Cons                                                                        |
| :----------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------: |
| - Suitable for quickly identifying potential vulnerabilities |                                                      - Can produce a large number of reports                                                      |
|                - Part of the Penetration Test                |                                                        - Quality depends on the tool used                                                         |
|     - Better for Budget, they are cheaper than Pentests      | - Real-life scenarios for vulnerabilities are not considered (it could be behind a proxy or only exploitable with social engineering/credentials) |
|                                                              |                                    - The low-risk vulnerability may be used as part of a more powerful attack.                                    |

**Penetration testing**

|                                     Pros                                      |                            Cons                             |
| :---------------------------------------------------------------------------: | :---------------------------------------------------------: |
|             Tester shows organisations what an attacker could do.             |                       Very Expensive                        |
| How any vulnerabilities could be used against it by attackers – the real risk | Requires extensive planning and time to carry out the tests |
|                         Can be shown to the customer                          |                                                             |