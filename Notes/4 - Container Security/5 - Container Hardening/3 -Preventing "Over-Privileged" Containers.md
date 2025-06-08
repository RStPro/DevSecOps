First, we need to understand what privileged containers are in this context.

Privileged containers are containers that have unchecked access to the host.
The entire point of containerization is to "isolate" a container from the host. By running Docker containers in "privileged" mode, the normal security mechanisms to isolate a container from the host are bypassed.
While privileged containers can have legitimate uses, for example, running Docker-In-Docker (a container within a container) or for debugging purposes, they are extremely dangerous.

When running a Docker container in “privileged” mode, Docker will assign all possible capabilities to the container, meaning the container can do and access anything on the host (such as filesystems).

![[Pasted image 20250608175847.png]]

What are capabilities, I hear you ask?
Capabilities are a security feature of Linux that determines what processes can and cannot do on a granular level.
Traditionally, processes can either have full root privileges or no privileges at all, which can be dangerous as we may not want to allow a process to have full root privileges as it means it will have unrestricted access to the system.

Capabilities allow us to fine-tune what privileges a process has. I have placed some standard capabilities in the table below, what privileges they translate to, and where they may be used:

| **Capability**       | **Description**                                                                                                                                                                                 | **Use Case**                                                                                                                                                                              |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CAP_NET_BIND_SERVICE | This capability allows services to bind to ports, specifically those under 1024, which usually requires root privileges.                                                                        | Allowing a web server to bind on port 80 without root access.                                                                                                                             |
| CAP_SYS_ADMIN        | This capability provides a variety of administrative privileges, including being able to mount/unmount file systems, changing network settings, performing system reboots, shutdowns, and more. | You may find this capability in a process that automates administrative tasks. For example, modifying a user or starting/stopping a service.                                              |
| CAP_SYS_RESOURCE     | This capability allows a process to modify the maximum limit of resources available. For example, a process can use more memory or bandwidth.                                                   | This capability can control the number of resources a process can consume on a granular level. This can be either increasing the amount of resources or reducing the amount of resources. |

To summarize, privileged containers are containers assigned full privileges - i.e., full root access. Attackers can escape a container using this method. If you would like homework, this process has been demonstrated in the [Container Vulnerabilities](https://tryhackme.com/room/containervulnerabilitiesDG) room.

It's recommended assigning capabilities to containers individually rather than running containers with the `--privileged` flag (which will assign all capabilities). For example, you can assign the `NET_BIND_SERVICE` capability to a container running a web server on port 80 by including the `--cap-add=NET_BIND_SERVICE` when running the container.

![[Pasted image 20250608180744.png]]

Finally, the command `capsh --print` can be used to determine what capabilities are assigned to a process.

![[Pasted image 20250608180812.png]]

It is important to frequently review what capabilities are assigned to a container.

****When a container is privileged, it shares the same namespace as the host**, meaning resources on the host can be accessed by the container - breaking the "isolated" environment.