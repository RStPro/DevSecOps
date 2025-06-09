## The Lifecycle

Now that it has been established what IaC is and the tools we use to implement it, it’s time to define the lifecycle.
There is talk about an IaC lifecycle across forms, blog posts, and academic papers. Still, there is yet to be an agreed-upon and widely adopted lifecycle (as there is for DevOps/DevSecOps).
Because we think you, the reader, would benefit from having an IaC lifecycle to use as an educational tool, we have defined one, the infrastructure as code lifecycle (IaCLC). The actions/tasks performed by developers and IaC tools can be broken down into phases, which together make a lifecycle; this lifecycle helps us understand that infrastructure as code has continual and repeatable processes, which don't simply follow a linear sequence of provision and management tasks. This task will outline the stages of the IaC lifecycle, its phases and how they are connected.

The IaCLC is designed to give DevOps Engineers (or anyone else assigned with the task) guidance on the tasks associated with provisioning infrastructure and the continued support of that infrastructure. Key DevOps practices such as continuous integration and continuous deployment are also parts of best practices throughout the lifecycle. 

Due to IaC being a development process, some parallels can be drawn between the IaC lifecycle and the SDLC, which also covers a solution's planning/designing, implementation, testing, deployment and monitoring. While these parallels exist due to these lifecycles being created on the same foundations (providing developer guidance and improving output quality), they don't directly fit into each other. Both lifecycles break down tasks into phases. However, due to the frequently changing infrastructure needs, the IaCLC distinguishes between two different types of phases.

![IaC lifecycle](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/248f6eebfa09c336733237216b1b4b8b.svg)

**The Continual (Best Practice) Phases** 

| Version Control        | This phase involves versioning code while defining your infrastructure and making changes. This way, when it comes to the later rollback phase, there are clearly defined versions to fall back on should a new change break something.                                                                                                      |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Collaboration          | When working as part of a team on infrastructure, it is crucial to communicate and collaborate so everyone is on the same page. Otherwise, this can lead to a disconnect between modular infrastructure components or general confusion over infrastructure.                                                                                 |
| Monitoring/Maintenance | Once an infrastructure has been provisioned/configured, it must be monitored for poor performance, security events, failure events, warnings, etc. Automated maintenance tasks (e.g. disk clean-up) can help avoid some of these events. In certain events, this phase can trigger the rollback phase.                                       |
| Rollback               | In the event of a failure event post-deployment, the infrastructure will need to be rolled back to the last known working version.                                                                                                                                                                                                           |
| Review + Change        | Just because an infrastructure works doesn’t mean it’s as efficient as it could be. Perhaps a new security vulnerability has been discovered, or maybe there’s a new business requirement that would benefit from an infrastructure change. Infrastructure should routinely be reviewed to determine if this is the case, and changed if so. |

**The Repeatable (Infra Creation + Config) Phases** 

| Design    | The infrastructure needs to be designed based on needs, taking security into account throughout the whole process (for example, poor scaling policy design can lead to availability issues, which is a huge security concern). |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Define    | Use the design to define the infrastructure that needs to be provisioned in code.                                                                                                                                              |
| Test      | Using a linter, validate the code for syntax errors or logical issues. Before provisioning is done in production, test the infrastructure in a replica environment (staging).                                                  |
| Provision | Provision the infrastructure that has been defined in the production environment using a provisioning tool, e.g. Terraform.                                                                                                    |
| Configure | Configure the provisioned environment using a configuration management tool, e.g. Ansible.                                                                                                                                     |
