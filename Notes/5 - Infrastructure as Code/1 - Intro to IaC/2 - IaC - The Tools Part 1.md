## Get to Know Your Toolkit 

Now that we’ve established _what_ IaC is, we can start thinking about some of the tools used for infrastructure as code. Many tools fall under the IaC umbrella, including Terraform, AWS CloudFormation, Google Cloud Deployment Manager, Ansible, Puppet, Chef, SaltStack and Pulumi.

It’s important to understand that some of these tools have different use cases, each with its own benefits. Due to the varied use cases of these IaC tools, having infrastructure provisioned, configured and deployed end-to-end will require using a combination of IaC tools rather than a single solution. To better understand these tools, this task will cover some of the key characteristics which distinguish these tools from each other so you know _what_ tool to use and _when_. Bear in mind that the behavior of these tools can often depend on exactly how they are used, often leading to debate over some of their characteristics; with this in mind, we will define those characteristics in question and how each tool is _generally_ used.

## Declarative vs. Imperative 

First off, let’s establish the difference between declarative and imperative (also known as functional and procedural) IaC tools:

**Declarative**

This involves declaring an explicit desired state for your infrastructure, min/max resources, x components, etc.; the IaC tool will perform actions based on what is defined. A state file is kept to ensure your infrastructure’s current state matches the desired state.

In other words, it focuses on the **what** rather than the **how**. A declarative IaC tool is usually idempotent, meaning the same result will be achieved when run repeatedly. This is because that check is done against the state file, and if the infrastructure is already provisioned, it will make no changes if rerun.
Examples of declarative IaC tools are Terraform, AWS CloudFormation, Pulumi and Puppet (Ansible also supports declarative).

**Imperative**

This approach involves defining specific commands to be run to achieve the desired state; these commands need to be executed in a particular order. Imperative IaC is usually not idempotent in that if you run these tools multiple times, the same result won’t be replicated, or the tool may run into some configuration issues. This is because these commands will be run regardless of the state of your infrastructure, so running these commands on an already provisioned infrastructure may cause additional unwanted infrastructure to be added or may break the configuration of some existing components (depending on the set-up of the infrastructure and the commands being run).
Examples of imperative IaC tools: Chef is the best example of an imperative tool; however, SaltStack and Ansible both support imperative programming as well.

Imagine it like directions to an X on a map, where imperative will give you a list of directions which will bring you to X if you are at the known start point (e.g., an unconfigured server). However, if you are not at this known start point (e.g., a partially configured server), you will not arrive at X but somewhere slightly different.

Declarative takes into account where you are on the map and works out which directions need to be taken to get to X from that point. Deciding which to use can depend on what your infrastructure needs are. Declarative is considered a more straightforward approach that is easier to manage, especially for long-term infrastructure.

In contrast, imperative IaC is more flexible, giving the user more control and allowing them to specify exactly how the infrastructure is provisioned/managed rather than the tool itself taking care of it.

## Agent-based vs. Agentless

Agent-based vs Agentless is a term that extends beyond infrastructure as code and is also used in the context of monitoring and security tools. In the context of IaC:

**Agent-based**

An “agent” will need to be installed on the server that is to be managed. It runs in the background and acts as a communication channel between the IaC tool and the resources that need managing. This agent is responsible for executing and reporting on the state of the infrastructure/managed resources. Note that this agent must be installed on every target system/node that needs to be managed. An agent-based IaC tool can perform tasks even when the system has limited connectivity or is offline, making it a robust choice for automation; however, you need to take care with maintenance when using these tools, monitoring the agent software closely so it can be restarted in the event of a crash.

Another thing to consider with agent-based IaC tools is that some of these tools will require opening ports on the server for inbound and outbound traffic so that the agent can push/pull configuration information; from a security perspective, more open ports are negative. Despite this, they offer a level of granular control over managed resources and can collect more detailed monitoring data. Because of this, they might be ideal if control is an important factor in your setup. Some agent-based IaC tools: Puppet, Chef, and Saltstack.

**Agentless** 

Agentless IaC tools, as you may have guessed, do not require agents to be installed on target systems. Instead, these tools leverage existing communication protocols like SSH, WinRM or Cloud APIs to interact with and provision resources on the target system.
Agentless IaC tools benefit from being easier to use; their simplicity during set-up can mean faster deployment time, and their agentless nature can also mean the tool can be deployed across multiple environments without custom agent changes needing to be made based on each environment’s needs, making it a flexible choice.
Also, compared to agent-based IaC tools, there is less maintenance and no risks surrounding the securing of an agent. However, agentless IaC tools generally have less control over target systems than agent-based tools. Agentless tools are useful in environments which have to adapt to fluctuating workloads, with resources being created/destroyed to meet these workloads. These newly created resources can be managed without having to rely on pre-installed agents. Agentless IaC tools: Terraform, AWS CloudFormation, Pulumi and Ansible.

Once again, both options have their advantages and disadvantages.
Infrastructure provisioning and configuration can present developers with a very particular set of problems, and choosing the correct tool for the job, depending on what needs to be done, involves taking these into account.