In our on-prem IaC journey, we will start with [Vagrant](https://developer.hashicorp.com/vagrant). Vagrant is a software solution that can be used for building and maintaining portable virtual software development environments. In essence, Vagrant can be used to create resources from an IaC pipeline. You can think of Vagrant as the big brother of Docker. In the context of Vagrant, Docker would be seen as a provider, meaning that Vagrant could be used to not only deploy Docker instances but also the actual servers that would host them.

## Terminology

Before diving into using Vagrant, let's brush up on some terminology first.

|Term|Definition|
|---|---|
|Provider|A Vagrant provider is the virtualisation technology that will be used to provision the IaC deployment. Vagrant can use different providers such as Docker, VirtualBox, VMware, and even AWS for cloud-based deployments.|
|Provision|Provision is the term used to perform an action using Vagrant. This can be actions such as adding new files or running a script to configure the host created with Vagrant.|
|Configure|Configure is used to perform configuration changes using Vagrant. This can be changed by adding a network interface to a host or changing its hostname.|
|Variable|A variable stores some value that will be used in the Vagrant deployment script.|
|Box|The Box refers to the image that will be provisioned by Vagrant.|
|Vagrantfile|The Vagrantfile is the provisioning file that will be read and executed by Vagrant.|
## Vagrant Example

Let's take a look at a simple Vagrant provisioning script. In our example here, we have the following folder structure:

```
.
├── provision
│   ├── files.zip
│   └── script.sh
└── Vagrantfile
```

The Vagrantfile script has the following code:

![[Pasted image 20250609115841.png]]

In this example, we are going to provision two servers. Both of these servers will start with the base Ubuntu Bionic x64 image.
Like Docker, these images will be pulled from a public image repo.
We could, however, tell Vagrant where to find these images, meaning they can be pulled from a private repo of images as well. You can see that both servers are configured with a hostname and how many CPUs (1) and RAM (4GB) each host will have.

- The first server will also have two network interfaces with static IPs attached.
- The second server will have a file called `files.zip` uploaded, and a script called `script.sh` will be executed on the host.

If we want to provision the entire script, we would use the command `vagrant up`. This would provision both servers in the order specified in the Vagrantfile. We could also decide to only provision one of the servers by using the server name. For example, `testserver` could be provisioned using `vagrant up server`.

If you want to play around with VirtualBox provisioning using Vagrant, look at this [repo](https://github.com/MWR-CyberSec/tabletop-lab-creation).
Using VirtualBox and Vagrant, this repo will allow you to create your very own Active Directory (AD) network with two domain controllers, a server, and a workstation. Give the Vagrantfile a read to see what provisioning will be performed on each host.

We will create our very own IaC deployment script a bit later in this room.