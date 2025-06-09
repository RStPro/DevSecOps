## ﻿Infrastructure Before IaC  

Before defining IaC, it’s important to understand why we need it. In other words, what problems is it solving?

Let us consider what was required when infrastructure was configured and managed in the days before IaC.
Here are some tasks which would have been the responsibility of various teams (depending on companies structure), such as DevOps/DevSecOps, Platform, Infrastructure, Network and Systems Administration:

- Manually provisioning servers (physically installing servers or manually deploying virtual machines)
- Network configuration (setting up a network for the infrastructure, including setting up IP addresses, subnets, routing tables and any network components that the infra needs like routers, switches or firewalls)
- Installing an OS
- Installation, configuration and updating of software (database, web server etc.)
- Disaster recovery (DR) (this involves having a backup infrastructure on standby, making a detailed “failover” plan, and having clear procedures in place should the primary data centre go down). 

## Infrastructure as Code Explained

﻿Instead of provisioning and managing infrastructure manually, as discussed above, infrastructure as code allows the automation of these tasks through code. This code can be used to define a "desired state" for the infrastructure, acting as a blueprint for IaC tools to provision the infrastructure. For example, you may define some resources in your code, such as network components, virtual machines, and a database. An IaC tool will build this blueprint and ensure the infrastructure is always in line with it. Should you want to make an infrastructure change, like increasing the number of VMs, only a simple change needs to be made to the code, which will be reflected in your infrastructure once applied. Compare this to what was previously required to add a VM, which would involve making a manual request through a portal and waiting for that request to be actioned by a systems administrator, and it becomes easy to see the utility of IaC.

## The Many Benefits of IaC

Having infrastructure deployed from code also means it can be a collaborative process and a shared responsibility. This means knowledge of infrastructure and its configuration isn't siloed to a single team member, avoiding knowledge dependencies whilst supporting continuous integration (CI). Continuous deployment (CD) is also supported through the ability to deploy consistent infrastructure across multiple environments. As well as reducing the manual efforts and risk of error, an IaC approach can make it possible to have a reliable infrastructure that is scalable, versionable, and repeatable.

**Scalable** 

This technology begins to make even more sense when you consider the widespread adoption of cloud computing and its elastic nature, with virtual machines and resources being scaled up and down based on demand due to resources being billed per second/minute/hour. With IaC, you can do this scaling with a single command or even automate the process, whereas in the past, this would have involved weeks of work (e.g., logging tickets and manually provisioning and de-provisioning).

**Versionable** 

Infrastructure as code should be treated as any other code and versioned using a version control system. Versioning an infrastructure means it's self-documenting, allowing infrastructure changes to be tracked and recorded. This benefits the many teams that work with infrastructure with all sorts of tasks, from audits to troubleshooting infrastructure issues. Speaking of infrastructure issues, versioning also means that should your latest infrastructure start having problems, you can redeploy your infrastructure to the last known working version, an example of how IaC allows for reliable infrastructure. Versioning infrastructure can also improve testing capabilities; for example, an application can be tested using a historical infrastructure build.

**Repeatable** 

In the dev world, it is common to work between multiple environments. Developers first build their code in a dev environment before testing it in a staging environment (which mirrors production) and finally deploying the fully functional and tested code into the production environment. In the past, these three environments would require the manual provisioning and configuration of 3 respective infrastructures. With IaC, you can use the same code/configuration to set up identical infrastructures across multiple environments with the push of a button. While saving massive amounts of time, this also ensures consistency/reliability across environments, which is critical when testing software and was very hard to achieve in the days of manual provisioning.

## IaC in Practice 

IaC is a powerful technology that can streamline and improve business-critical processes if used correctly.
To demonstrate this utility, let us take one of the example responsibilities mentioned at the beginning of the task, disaster recovery, and examine how IaC can aid this process. As touched on above, disaster recovery is the process of restoring infrastructure after a catastrophic/disruptive event; for example, if you are working for a company that has a physical on-premises infrastructure located in a data center, a disaster can range from a simple power outage to extreme examples such as natural disasters like wildfires or hurricanes bringing this "primary" data center down. Failing over from this primary data center to a secondary backup data center, when done manually, is a very time-consuming, high-pressure situation which can lead to many issues. Here are a few ways in which IaC can help with disaster recovery: 

**Infrastructure Automation:** Since IaC allows the automation of the provisioning and configuration of an infrastructure, re-provisioning and re-configuring an infrastructure in a backup data center is streamlined and less time-consuming.

**Data Backup and Recovery:** Data loss or corruption is one of the most significant risks associated with disaster recovery and can be very costly to the affected company. Infrastructure as code can be used to automate the backup and recovery of data. Backup procedures can be defined in code, which will be triggered in the event of a disaster to ensure data is restored.

**Fail over Automation:** During a disaster, critical services can become unavailable as they will point to the broken infrastructure. IaC can be used to automate the fail over process so critical services use the backup infrastructure, which reduces downtime.

**Configuration Consistency:** IaC keeps infrastructure consistent and well-documented; this consistency is vital during the disaster recovery process and helps avoid misconfigurations (often caused by simple human error or lack of documentation on the current configuration) during the transition to a backup environment.

**Scaling Resources:** The recovery process can be resource intensive, and IaC can be used to scale resources to handle the increased workloads (and scale back down afterwards). 

These are just some examples of how IaC can aid and streamline processes, with a wide range of teams benefiting from infrastructure as code's versionable, scalable, and repeatable nature - saving them time and headaches.

## Summary

In conclusion, infrastructure as code is a fundamental concept in DevSecOps, with the technology supporting key concepts like continuous integration (allowing for infrastructure development to be a collaborative process with versioning in place) and continuous deployment (allowing for the automation of infrastructure deployment across multiple environments consistently). IaC also improves efficiency by facilitating infrastructure changes in code, allowing for changes to be made quickly to adapt to developing infrastructure requirements and reduce manual tasks in the process.