The next IaC tool to learn about is [Ansible](https://www.ansible.com/).
Like Vagrant, Ansible is another suite of software tools that allows you to perform IaC. Ansible is also open-source, making it a popular choice for IaC pipelines and deployments.
One main difference between Ansible and Vagrant is that Ansible performs version control on the steps executed. This means that Ansible is similar to Docker, in that it will only perform updates on steps that require updates, instead of requiring a full reprovision.

## Terminology

Before diving into using Ansible, let's brush up on some terminology first.

| Term     | Definition                                                                                                                                                                                                                                                                                                                                                                                                                               |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Playbook | An Ansible playbook is a YAML file with a series of steps that will be executed.                                                                                                                                                                                                                                                                                                                                                         |
| Template | Ansible allows for the creation of template files. These act as your base files, like a configuration file, with placeholders for Ansible variables, which will then be injected into at runtime to create a final file that can be deployed to the host. Using Ansible variables means that you can change the value of the variable in a single location and it will then propagate through to all placeholders in your configuration. |
| Role     | Ansible allows for the creation of a collection of templates and instructions that are then called roles. A host that will be provisioned can then be assigned one or more of these roles, executing the entire template for the host. This allows you to reuse the role definition with a single line of configuration where you specify that the role must be provisioned on a host.                                                   |
| Variable | A variable stores some value that will be used in the Ansible deployment script. Ansible can take this a step further by having variable files where each file has different values for the same variables, and the decision is then made at runtime for which variable file will be used.                                                                                                                                               |

## Ansible Example

Ansible makes use of a specific folder and file structure. The most important part of the structure is the playbook, a YAML file that ultimately dictates what commands will be executed for provisioning. Let's take a look at the typical folder structure:

![[Pasted image 20250609120424.png]]

The folder structure was only expanded for the `common` role. However, this same structure would apply for roles 2 to 3.

Let's dive a little bit into what each of these files would do. Let's start with the playbook.yml file:

![[Pasted image 20250609120458.png]]

As we can see, the playbook specifies that the `common` and `role3` roles should be applied for all hosts where this Ansible playbook will be executed. It will also use the `var.yml` file to overwrite any default variables within the roles. This allows us to only change the default variables where needed, as the defaults will then still be applied to all other variables.

To execute the `common` role, Ansible will load variables from the `defaults/main.yml` file and overwrite these variables with any new values found in the `var.yml` file. It will then read and execute the `tasks/main.yml` file. This file would look something like this:

![[Pasted image 20250609120559.png]]

The first section of the Ansible file will determine the OS distribution of the host. It will then use this information to include OS-specific provisioning steps. As you can see from our folder structure, we have specific provisioning steps based on whether the distribution is Debian or RedHat. The second section of the playbook will set the root user's password. In the third section, we update the host and install some packages. However, we only execute the installing step matching the OS distribution. If the host is Debian, we will execute the commands specified in the `apt.yml` file. If the host is RedHat, we will execute the commands specified in the `yum.yml` file. This allows our Ansible role to be OS distribution agnostic. Lastly, we will execute the commands contained within the `task1.yml` and `task2.yml` files. These can be any commands, such as adding files to the host or making configuration changes.

This is quite a lot of information to take in, but as you start using these tools and follow along with what scripts get executed when, it makes a lot more sense.

## Combining Vagrant and Ansible

While you could stick to one IaC tool for your entire pipeline, it can often be beneficial to combine toolings. For example, Vagrant could be used for the main deployment of hosts, and Ansible can then be used for host-specific configuration. This way, you only use Vagrant when you want to recreate the entire network from scratch but can still use Ansible to make host-specific configuration changes until a full rebuild is required. Ansible would then run locally on each host to perform these configuration changes, while Vagrant will be executed from the hypervisor itself. In order to do this, you could add the following to your Vagrantfile to tell Vagrant to provision an Ansible playbook:

![[Pasted image 20250609121002.png]]

It is also worth noting some of the differences between Vagrant and Ansible, if you are looking to only stick to a single IaC solution:

| **Feature/Aspect**               | **Vagrant**                                                         | **Ansible**                                                               |
| -------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **Configuration Language**       | Ruby (for Vagrantfiles).                                            | YAML (for Playbooks).                                                     |
| **Integration with Other Tools** | Often used with provisioning tools like Chef, Puppet, or Ansible.   | Can be used standalone or integrated with other CI/CD tools.              |
| **Complexity**                   | Relatively straightforward for setting up development environments. | Higher complexity for larger infrastructures and advanced configurations. |
| **Scalability**                  | More suited for smaller-scale, individual development environments. | Highly scalable, suitable for managing complex, multi-tier applications.  |
| **Execution Model**              | Procedural style with sequential execution steps.                   | Declarative model, describing the desired state of the system.            |
