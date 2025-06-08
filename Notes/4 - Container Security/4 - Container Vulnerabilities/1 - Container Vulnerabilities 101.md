What Sort of Vulnerabilities Can We Expect To Find in Docker Containers

While Docker containers are designed to isolate applications from one another, they can still be vulnerable. For example, hard-coded passwords for an application can still be present. If an attacker is able to gain access through a vulnerable web application, for example, they will be able to find these credentials.

You can see an example of a web application containing hard-coded credentials to a database server in the code snippet below:

```php
/** Database hostname */
define( 'DB_HOST', 'localhost' );

/** Database name */
define( 'DB_NAME', 'sales' );

/** Database username */
define( 'DB_USER', 'production' );

/** Database password */
define( 'DB_PASSWORD', 'SuperstrongPassword321!' );
```

This, of course, isn't the only vulnerability that can be exploited in containers. The other potential attack vectors have been listed in the table below.

| **Vulnerability**        | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Misconfigured Containers | Misconfigured containers will have privileges that are not necessary for the operation of the container. For example, a container running in "privileged" mode will have access to the host operating system - removing the layers of isolation.                                                                                                                                                                                                     |
| Vulnerable Images        | There have been numerous incidents of popular Docker images being backdoored to perform malicious actions such as crypto mining.                                                                                                                                                                                                                                                                                                                     |
| Network Connectivity     | A container that is not correctly networked can be exposed to the internet. For example, a database container for a web application should only be accessible to the web application container - not the internet.<br><br>Additionally, containers can serve to become a method of lateral movement. Once an attacker has access to a container, they may be able to interact with other containers on the host that are not exposed to the network. |
