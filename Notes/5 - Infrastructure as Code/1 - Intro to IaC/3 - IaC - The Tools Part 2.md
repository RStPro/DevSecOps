## Immutable vs. Mutable 

Immutable vs mutable infrastructure refers to whether or not changes can be made to an infrastructure. To define both, let’s imagine we have a simple infrastructure, a virtual machine with a web server and application. If you want to change this infrastructure, for example, deploy some application code to your web application, this code will mean your web application will go from version 1 to version 2. How might that look for each?

**Mutable**

Mutable infrastructure means you can make changes to that infrastructure in place. So, in our current example, we can upgrade the application on the server it’s currently running on. The advantage here is that no additional resources need to be provisioned for this update, with the resources already being used just needing to be changed. Where mutable infrastructure starts presenting issues is, imagine your web application update contains three changes, and whilst these updates are being made, one of the changes fails to apply. This is a common occurrence in development and can occur for several reasons, such as application misconfiguration or a network dropout. Now running on your server will be a web application version with two of the three changes required to be version 2. In other words, it’s no longer version 1 anymore but not quite version 2 either. When an application is updated in a production environment, it will have been tested first in development and staging environments. What won’t have been tested is this halfway version, leading to all kinds of potential issues. Imagine now that this update was not just rolled out on a single server, but many, maybe some updates succeeded, and some failed with errors in different changes. You can see how this can become an issue very quickly with different versions of the web application existing across many servers.

**Immutable**

Immutable infrastructure means you cannot make changes to it. Once an infrastructure has been provisioned, that’s how it will be until it’s destroyed. Now, let’s apply that to our example. When this new version 2 of the web application is deployed, an entirely new infrastructure will be deployed with this new version. Now, you have two infrastructures stood up: one with version 1 of the web application and one with version 2. However, if all of the changes are implemented successfully (and only if they ALL are; otherwise, if it fails, the infrastructure will be torn down, and the process will be retried), the version 1 infrastructure can be torn down. This approach has some drawbacks, as having multiple infrastructures stood up side by side or retrying on failed attempts is more resource-intensive than simply updating in place, but it allows for consistency across servers. You know with certainty that x server is running version 2 of the web application.

Immutable IaC tools: Terraform, AWS CloudFormation, Google Cloud Deployment Manager, Pulumi (some of these tools can be configured to be used with a mutable infrastructure but work better with an immutable approach)

In the example given, it makes more sense to use an immutable infrastructure. However, to demonstrate further that each can have its own use case, imagine the server instead is a critical database system that requires regular maintenance updates and patching. If you were to use an immutable infrastructure for this, the critical database would have to be rebuilt from scratch every time, which can be a risky process when dealing with business-critical data. So, in this instance, it might make sense to use a mutable infrastructure.

## Provisioning vs. Configuration Management 

All the characteristics discussed in this task so far are behavioural; in other words, how does this tool work? This way or that way. Considering what a tool's purpose is and when it is used in the development of infrastructure will tell us whether it is a _provisioning_ tool or a _configuration_ _management_ tool. You might see these primary functions defined differently elsewhere, for example, infrastructure as code vs. configuration as code, but to determine which tool falls into which category, you simply need to ask, "What can it do?". If we think about four key tasks: Infrastructure provisioning (the set-up of the infrastructure), infrastructure management (changes made to infrastructure), software installation (initial installation and configuration of software/applications), and software management (updates made to software or config changes).

There is no single tool that can perform all 4 of these tasks. Instead, combining two tools, a provisioning tool and a configuration management tool, is common practice to cover all these. There will be a practical example of exactly what tools can cover which tasks in the static site coming up. Some examples of each type of tool:

 - Provisioning tools: Terraform, AWS CloudFormation, Google Cloud Deployment Manager, Pulumi
 - Configuration management tools: Ansible, Chef, Puppet, Saltstack

Let’s consider a real-life industry example of how these two types of tools might be used. Say you work for a company which needs to set up a new infrastructure for a web application. A similar one has been deployed before and fell prey to some malicious activity, so this time, you will install an agent to monitor for this activity. The infrastructure would be defined and provisioned using a provisioning tool like Terraform, and then a configuration management tool like Ansible would be used to install an agent within the provisioned infrastructure to monitor for malicious behaviour.

## Put That All Together

Now, you’ve been introduced to the world of infrastructure as code tools and their various uses. Each has its characteristics which best suit different use cases and scenarios. In that way, they are no different to physical tools; you have to assess the problem and choose the best tool to address it. Here's a little summary of what we've discussed, as well as a little bit more information about some of the tools mentioned:

**Terraform**: is a declarative, agentless infrastructure provisioning tool that works with immutable infrastructure. Terraform is one of the most popular infrastructure provisioning tools out there, allowing for the management of infrastructure across multiple cloud providers like AWS, GCP and Azure.

**Ansible:** is a hybrid, typically agentless **configuration management tool** that works with mutable infrastructure. Another example of a massively popular tool in the DevSecOps space. It's slightly harder to categorize than some of the other tools, because of how this tool functions and what it does can depend on how you employ it. For example, there is much discussion over whether Ansible is an imperative or declarative tool. In reality, Ansible is sort of a hybrid in a sense.

**Pulumi:** is a declarative, agentless infrastructure provisioning tool that works with immutable infrastructure. Pulumi is similar in nature to Terraform but has become increasingly popular in recent years due to its ability to let users define their desired infrastructure using familiar general-purpose languages like Python, JavaScript, Go, Java and markup languages like YAML.

**Aws CloudFormation:** is a declarative, agentless infrastructure provisioning tool which can be used to implement an immutable infrastructure on AWS. This is an AWS-managed service and provisions AWS cloud resources using JSON / YAML templates.

**Chef:** is an imperative, agent-based configuration management tool that works with mutable infrastructure. Chef gets an infrastructure to a desired state by running a series of instructions contained in a file referred to as a 'Recipe'; a collection of these files is referred to as a 'Cookbook'.

**Puppet:** is a declarative, agent-based configuration management tool that works with mutable infrastructure. In Puppet, you define the desired configuration state using their own domain-specific language (DSL), "Puppet Code"; Puppet then automates this configuration through a Puppet primary server and agent.

![[Pasted image 20250609105124.png]]
