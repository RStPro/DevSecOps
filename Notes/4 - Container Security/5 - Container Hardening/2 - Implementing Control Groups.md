Control Groups (also known as cgroups) are a feature of the Linux kernel that facilitates restricting and prioritizing the number of system resources a process can utilize.

For example, a process such as an application can be restricted to only use a certain amount of RAM or processing power or given priority over other processes. This often improves system stability and allows administrators to track system resource use better.

In the context of Docker, implementing cgroups helps achieve isolation and stability. Because cgroups can be used to determine the number of (or priorities) resources a container uses, this helps prevent faulty or malicious containers from exhausting a system. Of course, the best mechanism is preventing this from happening, but preventing a container from bringing down a whole system is an excellent second line of defense.

This behavior is not enabled by default on Docker and must be enabled per container when starting the container. The switches used to specify the limit of resources a container can use have been provided in the table below:

| **Type of Resource** | **Argument**                                                  | **Example**                                 |
| -------------------- | ------------------------------------------------------------- | ------------------------------------------- |
| CPU                  | `--cpus` (in core count)                                      | `docker run -it --cpus="1" mycontainer`     |
| Memory               | `--memory` (in k, m, g for kilobytes, megabytes or gigabytes) | `docker run -it --memory="20m" mycontainer` |

You can also update this setting once the container is running.
To do so, use the `docker update` command, the new memory value, and the container name. For example: `docker update --memory="40m" mycontainer`.
You can use the `docker inspect containername` command to view information about a container (including the resource limits set).
If a resource limit is set to **0**, this means that no resource limits have been set.

![[Pasted image 20250608175710.png]]

Docker uses namespaces to create isolated environments.
For example, namespaces are a way of performing different actions without affecting other processes.
Think of these as rooms in an office; each room serves its own individual purpose.
What happens in a room in this office will not affect what happens in another office.
These namespaces provide security by isolating processes from one another.
