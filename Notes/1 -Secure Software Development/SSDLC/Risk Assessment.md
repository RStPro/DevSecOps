Risk refers to the likelihood of a threat being exploited, negatively impacting a resource or the target it affects.
For example, vulnerabilities being exploited after a new version of the software is published, design flaws, and poorly reviewed code can increase the risk of these scenarios.
Risk management is an important pillar to integrate into the SDLC to mitigate risk in a product or service.  

---

Risk assessment is used to determine the level of the potential threat. Risk identified in the risk assessment process can be reduced or eliminated by applying appropriate controls during the risk mitigation process. Usually, a risk assessment is followed by threat modelling, which will be explained further in the next section.  

**Performing a Risk Assessment**

1. The first step in the risk assessment process is to assume the software will be attacked and consider the factors that motivate the threat actor. List out the factors such as the data value of the program, the security level of companies who provide resources that the code depends on, the clients purchasing the software, and how big is the software distributed (single, small work group or released worldwide). Based on these factors, write down the acceptable level of risk. For instance, a data loss may cause the company to lose millions, especially if they require to pay fines nowadays with GDPR, but eliminating all potential security bugs in the code may cost $40,000. The company and some other stakeholder groups have to decide whether it is worth it; it is also crucial to communicate these trade offs. Hence, everyone has an understanding of risk and its implications. From a brand reputation perspective, if the attack causes damage to the company's image, it costs the company more in the long run than fixing the code.
2. The next step is risk evaluation. Include factors like the worst-case scenario if the attacker has successfully attacked the software. You can demonstrate the worst-case scenario to executives and senior engineers by simulating a ransomware attack. Determine the value of data to be stolen, valuable data such as the user's identity, credentials to gain control of the endpoints on the network, and data or assets that pose a lower risk. Another factor to consider is the difficulty of mounting a successful attack, in other words, its complexity. For example, if an attacker can gain access to the company's tool for giving feedback to colleagues or running retrospective meetings, it would have a lower impact than accessing a production environment's monitoring and alerts system. The high level of risk will not be acceptable, and it is best to mitigate it. For example, a vulnerability can be exploited by anyone running prewritten attack scripts or using botnets to spread the scripts to compromise computers and networks. Users affected are a vital factor.
3. Some attacks only affect one or two users, but the denial of service attack will affect thousands of users when a server is attacked. Moreover, thousands of computers may be infected by the spread of worms. The last factor is the accessibility of the target. Determine whether the target accepts requests across a network or only local access, whether authentication is needed for establishing a connection, or if anyone can send requests. It has more impact if an attacker accesses a production environment vs a sandbox environment used in local playgrounds for people to do labs or tutorials.

Types of Risk Assessments

There are several types of Risk assessments best suited for different scenarios. Below are the different types of Risk Assessments:

**Qualitative Risk Assessment**

This is the most common type of Risk Assessment that you will find in companies (hopefully). In a Qualitative Risk Assessment, the goal is to assess and classify risk into thresholds like "Low", "Medium", and "High". It systematically examines what can cause harm and what decisions should be made to define or improve adequate control measures. Like all types of Risk Assessments, each level has a priority, where "High" has the most urgency. Even though Qualitative Risk Assessments don't use numbers, a typical formula to evaluate qualitative risk is:

`Risk = Severity x Likelihood`

"Severity" is the impact of the consequence, and Likelihood is the probability of it happening. It is up to the risk assessor to judge these circumstances.

**Quantitative Risk Assessment**  

The Quantitative Risk Assessment is used to measure risk with numerical values. Instead of "Low", "Medium", and "High", you would have numbers that represent those bands. When carrying out Quantitative Risk Analysis, we can use tools to determine Severity and Likelihood or custom series of calculations based on the company's processes.

For example, suppose there are services with assigned business criticality levels. In that case, you can say that if a bug affects a business-critical service (an authentication service, a payment infrastructure etc.), you will assign 5 points. This highlights why it is vital to understand a security posture and its processes. Measuring risk and priority with an endemic equation to a company's services will have great results. An example of a Quantitative Risk Assessment Matrix can be seen below:

![[Pasted image 20250519201328.png]]

Risk assessments are better performed at the beginning of the SDLC, during the planning and requirement phases. For example, "Customer data gets exfiltrated by an attack". Once the system is developed, you can perform quantitative risk analysis: "One customer can sue us for $ 20,000 if their data gets leaked", and we have 100 customers. However, the Annual Rate of Occurrence (ARO) is 0.001. Hence Annual Loss Expectancy is = $20,000 * 100 * 0.001 = $ 2,000, meaning as long as our compensating security control is less than $ 2,000, we are not overspending on security.