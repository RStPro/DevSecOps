DevOps is visualized as an infinite loop, describing all the comprising phases:

![[Pasted image 20250525105428.png]]

Following the infinite loop of the DevOps diagram, let's expand on some DevOps tools & processes that we'll look at as we follow the DevSecOps pathway and how they help an organization:

1. **CI/ CD** – In the previous task, we mentioned CI/CD (Continuous Integration and Continuous Deployment); CI/CD deals with the frequent merging of code and adding testing in an automated manner to perform checks as new code is pushed and merged. We can test code as we push and merge thanks to a new dynamic and routine in deployment, which takes the form of minor code changes systematically and routinely. Thanks to this change in dynamic, CI/CD helps detect bugs early and decreases the effort of maintaining modular code massively, which introduces reliable rollbacks of versions/code.

2. **INFRASTRUCTURE AS CODE** (IaC) – a way to manage and provision infrastructure through code and automation. Thanks to this approach, we can reuse code used to deploy infrastructure (for example, cloud instances), which helps in consistent resource creation and management. Standard tools for IaC are terraform, vagrant, etc. We will use these tools further in the pathway as we experiment with IaC security. 

3. **CONFIGURATION MANAGEMENT** – This is where the state of infrastructure is managed constantly and applying changes efficiently, making it more maintainable. Thanks to this, lots of time is saved, and more visibility into how infrastructure is configured. You can use IaC for configuration management.

4. **ORCHESTRATION** – Orchestration is the automation of workflows. It helps achieve stability; for example, by automating the planning of resources, we can have fast responses whenever there is a problem (e.g., health checks failing); this can be achieved thanks to monitoring.

5. **MONITORING** – focuses on collecting data about the performance and stability of services and infrastructure. This enables faster recovery, helps with cross-team visibility, provides more data to analyze for better root-cause analysis, and also generates an automated response, as mentioned earlier.

6. **MICROSERVICES** – An architecture that breaks an application into many small services. This has several benefits, like flexibility if there is a need to scale, reduced complexity, and more options for choosing technology across microservices. We will look at these in more detail in the DevSecOps pathway.