## Terraform Overview

Terraform is an infrastructure as code tool used for provisioning that allows the user to define both cloud and on-prem resources in a human-readable configuration file that can be versioned, reused and distributed across teams.
Terraform uses a consistent workflow to make the management of your infrastructure an easy and reliable process.
Both this configuration and the workflow Terraform follows will be covered by subsequent tasks in this room.
For now, let's define some terms which are key to understanding how Terraform provisions and manages infrastructure:

![[Pasted image 20250609172555.png]]

## Terraform's Architecture

Now we know what Terraform does. Let's examine how it is done. We will examine Terraform's architecture: 

**Terraform Core**: As the name suggests, Terraform Core is responsible for the core functionalities that allow users to provision and manage their infrastructure using Terraform.
As mentioned in the [Intro to IaC](https://tryhackme.com/room/introtoiac) room, Terraform is a declarative tool (reminder: this means that a desired state is defined, and the tool is responsible for ensuring the infrastructure meets that desired state, rather than the user declaring each step required to achieve the desired state), to ensure the user infrastructure is in the desired state, Terraform Core takes its input from two sources:

- **Terraform Config files**: The user defines the desired state of their infrastructure in these config files, in other words, what resources make up their desired infrastructure. 
- **State**: Terraform has a state file that keeps track of the current state of provisioned infrastructure. The core component checks this state file against the desired state defined in the config files, and, if there are resources that are defined but not provisioned (or the other way around), makes a plan of how to take the infrastructure from its current state to the desired state. By default, this state file is called terraform.tfstate and is stored in the same directory where Terraform runs.
![[Pasted image 20250609172802.png]]

**We can see in the graphic above that the Terraform Core takes its input from two places: the user-defined configuration files and tfstate. Should there be any difference between the desired state (configuration files) and the current state (tfstate), the required actions will be executed using a provider.**  

**Providers**: The plan mentioned above is executed using different providers depending on the resources defined. Providers are used to interact with cloud providers, SaaS providers and other APIs. For example, if an AWS resource like an EC2 instance is defined, the AWS provider would be used; if a Kubernetes cluster is defined, the Kubernetes provider would be required.

This tool and its architecture boasts many benefits of this IaC tool for DevSecOps engineers.

What probably sets Terraform apart the most from other IaC tools is the ability to use these providers to provision and manage resources across multiple cloud providers.
This means if you're working with an infrastructure that has infrastructure resources with AWS and Azure, Terraform can be used as a single solution for multi-cloud environments.
This also prevents vendor lock-in and means infrastructure can be much more flexible.

Another benefit of Terraform is the declarative configuration language, which is used to define resources in config files; it's easy to understand, and the human-readable format makes the definition process simple and streamlined.
On top of all this, the declarative nature of the tool supports versioning and change-tracking practices, allowing team members to collaborate during the declaration and development of infrastructure and roll back to previous infrastructure iterations.