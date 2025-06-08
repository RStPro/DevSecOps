Seccomp is an important security feature of Linux that restricts the actions a program can and cannot do.
To explain, picture a security guard at the entrance of an office. The security guard is responsible for making sure that only authorized people are allowed into the building and that they do what they are supposed to do. In this scenario, Seccomp is the security guard.  

Seccomp allows you to create and enforce a list of rules of what actions (system calls) the application can make. For example, allowing the application to make a system call to read a file but not allowing it to make a system call to open a new network connection (such as a reverse shell).

These profiles are helpful because they reduce attackers' ability to execute malicious commands whilst maintaining the application's functionality.
For example, a Seccomp profile for a web server may look like the following:

```json
{
  "defaultAction": "SCMP_ACT_ALLOW",
  "architectures": [
    "SCMP_ARCH_X86_64",
    "SCMP_ARCH_X86",
    "SCMP_ARCH_X32"
  ],
  "syscalls": [
    { "names": [ "read", "write", "exit", "exit_group", "open", "close", "stat", "fstat", "lstat", "poll", "getdents", "munmap", "mprotect", "brk", "arch_prctl", "set_tid_address", "set_robust_list" ], "action": "SCMP_ACT_ALLOW" },
    { "names": [ "execve", "execveat" ], "action": "SCMP_ACT_ERRNO" }
  ]
}
```

This Seccomp profile:

- Allows files to be read and written to
- Allows a network socket to be created
- But does not allow execution (for example, `execve`)

To create a Seccomp profile, you can simply create a profile using your favorite text editor.
This room will use `nano`. An example Seccomp profile (profile.json) has been provided below.
This profile will allow reading and writing access to files but no network connections.

```json
{
  "defaultAction": "SCMP_ACT_ALLOW",
  "architectures": ["SCMP_ARCH_X86_64"],
  "syscalls": [
    {
      "name": "socket",
      "action": "SCMP_ACT_ERRNO",
      "args": []
    },
    {
      "name": "connect",
      "action": "SCMP_ACT_ERRNO",
      "args": []
    },
    {
      "name": "bind",
      "action": "SCMP_ACT_ERRNO",
      "args": []
    },
    {
      "name": "listen",
      "action": "SCMP_ACT_ERRNO",
      "args": []
    },
    {
      "name": "accept",
      "action": "SCMP_ACT_ERRNO",
      "args": []
    }
    {
      "name": "read",
      "action": "SCMP_ACT_ALLOW",
      "args": []
    },
    {
      "name": "write",
      "action": "SCMP_ACT_ALLOW",
      "args": []
    }
  ]
}
```

With our Seccomp profile now created, we can apply it to our container at runtime by using the `--security-opt seccomp` flag with the location of the Seccomp profile. For example:

![[Pasted image 20250608181507.png]]

Docker already applies a default Seccomp profile at runtime.
However, this may not be suitable for your specific use case, especially if you wish to harden the container further while maintaining functionality.
You can learn more about using Seccomp with Docker [here](https://docs.docker.com/engine/security/seccomp/#:~:text=Secure%20computing%20mode%20\(%20seccomp%20\)%20is,state%20of%20the%20calling%20process.).

## AppArmor

AppArmor is a similar security feature in Linux because it prevents applications from performing unauthorized actions.
However, it works differently from Seccomp because it is not included in the application but in the operating system.

This mechanism is a Mandatory Access Control (MAC) system that determines the actions a process can execute based on a set of rules at the operating system level.
To use AppArmor, we first need to ensure that it is installed on our system:

![[Pasted image 20250608181607.png]]

With the output "apparmor module is loaded", we can confirm that AppArmor is installed and enabled. To apply an AppArmor profile to our container, we need to do the following:

- Create an AppArmor profile
- Load the profile into AppArmor
- Run our container with the new profile

First, let's create our AppArmor profile.
You can use your favourite text editor for this. Note that there are tools out there that can help generate AppArmor profiles based on your Dockerfile. However, this is out-of-scope for this room and can be "unreliable".

Provided below is an example AppArmor profile (profile.json) for an "Apache" web server that:

- Can read files located in /var/www/, /etc/apache2/mime.types and /run/apache2. 
- Read & write to /var/log/apache2.
- Bind to a TCP socket for port 80 but not other ports or protocols such as UDP.
- Cannot read from directories such as /bin, /lib, /usr.

```
/usr/sbin/httpd {

  capability setgid,
  capability setuid,

  /var/www/** r,
  /var/log/apache2/** rw,
  /etc/apache2/mime.types r,

  /run/apache2/apache2.pid rw,
  /run/apache2/*.sock rw,

  # Network access
  network tcp,

  # System logging
  /dev/log w,

  # Allow CGI execution
  /usr/bin/perl ix,

  # Deny access to everything else
  /** ix,
  deny /bin/**,
  deny /lib/**,
  deny /usr/**,
  deny /sbin/**
}
```

Now that we have created the AppArmor profile, we will need to import this into the AppArmor program to be recognized.

![[Pasted image 20250608181720.png]]

With our AppArmor profile now imported, we can apply it to our container at runtime by using the `--security-opt apparmor` flag with the location of the AppArmor profile. For example:

![[Pasted image 20250608181749.png]]

Just like Seccomp, Docker already applies a default AppArmor profile at runtime.
However, this may not be suitable for your specific use case, especially if you wish to harden the container further while maintaining functionality.
You can learn more about using AppArmor with Docker [here](https://docs.docker.com/engine/security/apparmor/).

## What's the Difference

Well, to put it briefly:

- AppArmor determines what resources an application can access (i.e., CPU, RAM, Network interface, filesystem, etc) and what actions it can take on those resources.
- Seccomp is within the program itself, which restricts what system calls the process can make (i.e. what parts of the CPU and operating system functions).

It's important to note that it is not a "one or the other" case. Seccomp and AppArmor can be combined to create layers of security for a container.