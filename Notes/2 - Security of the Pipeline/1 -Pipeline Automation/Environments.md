Most pipelines have several environments.
Each of these environments has a specific use case, and their security posture often differs. Let's take a look at some of the common ones:

|                **Environment**                 |                                                                                                                                                                                                                                                                          **Description**                                                                                                                                                                                                                                                                          | **Stability** | **Security Posture** | **May it contain customer data?** |
| :--------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------: | :------------------: | :-------------------------------: |
|               DEV - Development                |                              The DEV environment is the playground for developers. This environment is the most unstable as developers are continuously pushing new code and testing it. From a security standpoint, this environment has the weakest security. Access control is usually laxer, and developers often have direct access to the infrastructure itself. The likelihood of the development environment being compromised is high, but if there is adequate segregation, the impact of such a compromise should be low.                              |   Unstable    |       Weakest        |                No                 |
|         UAT - User Acceptance Testing          |                                        The UAT environment is used to test the application or select features before they are pushed to production. These include unit tests that ensure the developed feature behaves as expected. This can (and should) include security tests as well. Although this environment is more stable than DEV, it can often still be fairly unstable. Similarly, certain security hardening controls would have been introduced for UAT, but it is still not as hardened as PreProd or PROD.                                        |  Semi-Stable  |    Second Weakest    |                No                 |
|            PreProd - Pre-Production            |                                                                                                                 The PreProd environment is used to mimic production without actual customer/user data. This environment is kept stable and used to perform the final tests before the new feature is pushed to production. From a security standpoint, PreProd's security should technically mirror PROD. Although, this is not always the case.                                                                                                                  |    Stable     |   Second Strongest   |                No                 |
|               PROD - Production                | The PROD environment is the most sensitive. This is the current active environment that serves users or customers. To ensure that our users have the best experience, this environment must be kept stable. No updates should be performed here without proper change management. To enforce this, the security of this environment is the strongest. Only a select few employees or services will have the ability to make changes here. Furthermore, since we may have "malicious" users, the security has to be hardened to prevent outsider threats as well.  |    Stable     |      Strongest       |                Yes                |
| DR/HA - Disaster Recovery or High Availability | Depending on the criticality of the system, there may be a DR or HA environment. If the switchover is instantaneous, it is usually called a HA environment. This is often used for critical applications such as Online Banking, where the bank has to pay large penalties if the website goes down. In the event where some (but still small) downtime is allowed, the environment is called a DR environment, meant to be used to recover from a disaster in production. DR and HA environments should be exact mirrors of PROD in both stability and security. |    Stable     |      Strongest       |                Yes                |

## Other Notable Environments

There are some other environments that you may hear about when talking about DevOps.  

### **Green and Blue Environments**

Green and Blue environments are used for a Blue/Green deployment strategy when pushing an update to PROD. 
Instead of having a single PROD instance, there are two.

The Blue environment is running the current application version, and the Green environment is running the newer version.
Using a proxy or a router, all traffic can then be switched to the Green environment when the team is ready.
However, the Blue environment is kept for some time, meaning that if there are any unforeseen issues with the new version, traffic can just be routed to the Blue environment again.
We can think of this as High-Availability backups of PROD during a new deployment to use for a roll-back if something goes wrong, which is faster than having to perform a roll-back of the actual PROD environment.

### **Canary Environments**

Similar to Green and Blue environments, the goal of Canary environments is to smooth the PROD deployment process.
Again two environments are created, and users are gradually moved to the new environment.
For example, at the start, 10% of users can be migrated. If the new environment remains stable, another 10% can be migrated until 100% of the users are in the new environment.
Again, these are usually classified under PROD environments but are used to reduce the risk associated with a PROD upgrade to limit potential issues and downtime.

### **Common Tools**

Environments have changed significantly in modern times.
Breakthroughs such as virtualization and containerization have changed the landscape.
Instead of environments simply being computers, we can now have virtual computers created through tools such as Vagrant or Terraform.
We could also move away from hosts entirely to things like containers using Docker or pods using Kubernetes. These tools can make use of processes such as Infrastructure as Code (IaC) to even create software that can create and manage these environments.  

### **Security Considerations**

As mentioned before, the security considerations become more important the closer the environment is to PROD.
The underlying infrastructure of an application also forms part of the attack surface of the actual application.
Any vulnerabilities in this infrastructure could allow an attacker to take control of the host and the application.
As such, the infrastructure must be hardened against attacks. This hardening process usually requires things like the following:

- Removing unnecessary services
- Updating the host and applications
- Using a firewall to block unused ports

Case Study - Developer Bypasses in PROD

One of the common issues that can happen with different environments is that often things that should stay in DEV, don't.
Develop bypasses are common in DEV environments for features like the following:

- Multi-factor authentication
- CAPTCHAs
- Password resets
- Login portals

Developer bypasses allow developers to quickly test different application features by bypassing time-consuming features such as MFA prompts.
A common example is having a specific One-Time Pin (OTP) code that is always accepted, regardless of the OTP code that is sent by the application.

However, if there is inadequate sanitisation of these bypasses before the application is moved to the next environment, it could lead to a developer bypass making its way all the way into PROD.
That OTP bypass? It could now be leveraged by an attacker to bypass MFA and compromise user accounts.

This is why environments must be segregated, and similar to quality gates, security gates must be implemented to ensure a clean application is moved to the next environment.