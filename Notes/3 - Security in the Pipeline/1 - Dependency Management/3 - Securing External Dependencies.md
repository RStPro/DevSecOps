## Public CVEs

The team that develops external dependencies are not robots who don't make mistakes. They are humans, just like the rest of us. This means there may be vulnerabilities in the code that they have written. The issue, however, is that these vulnerabilities will be publicly disclosed, usually as a Common Vulnerabilities and Exposures (CVE), once the developers have created a patch. While this is good practice to ensure that developers create patches, for us, it is a problem since it means that our specific version of their dependency is now vulnerable to an issue that is advertised to attackers online.

As such, we must react as soon as possible and patch our dependency. But this is easier said than done. We may have version locked a dependency for the stability of our application. So upgrading to a new version means we will first have to determine whether such an upgrade could cause instability. The problem gets even worse when you start to talk about dependencies of dependencies. It is perhaps not the SDK that you are using that is vulnerable, but a dependency of the SDK, that is. Since that dependency has to be updated, we will also now need to update our SDK.

Log4j is a prime example of how bad this can truly get. Log4j is a Java-based logging utility. It was used in almost every application that was developed in Java. This led to several products becoming vulnerable when a vulnerability was discovered in the dependency. You can look [here for the full list of impacted products](https://github.com/cisagov/log4j-affected-db). The list got so big, more than 1000 products, that they had sorted it alphabetically.

Depending on the discovered vulnerability, it will impact the risk associated with the specific dependency. Since Log4j's vulnerability allowed for remote code execution, the impact was significant. If you would like to explore this issue more, have a look at [this room](https://tryhackme.com/room/solar).  

## Supply Chain Attacks

Even if dependencies do not have any vulnerabilities and are kept up to date, they can still be leveraged to attack systems and services. As more and more organisations are becoming security conscious and making it harder for an attacker to compromise them, attackers had to become more crafty.

Instead of trying to attack the application directly, which has been hardened, an attacker instead targets one of the dependencies of the application, which may have been created by a smaller team that does not have such a large security budget. These indirect attack methods are called supply chain attacks.

One advance persistent threat (APT) group, namely the MageCart group, was notorious for performing these types of attacks. Some highlights of their actions:

- Compromising the payment portal of British Airways' online portal led to the compromise of credit cards of customers and a fine for BA of 230 million dollars.
- Compromising more than 100000 customers' credit cards by embedding skimmers in various payment portals of various applications.
- Compromising more than 10000 AWS S3 buckets and embedding malware in any JavaScript found in these buckets.

The MageCart group showed that you do not really have to target an application directly. It is far more lucrative to compromise a dependency used by the application. These supply chain attacks are even more effective since a dependency might be used by several applications. Meaning the compromise of a single dependency could lead to the compromise of several applications.

There are several ways to compromise dependencies, but by far, the most common is when dependencies are insecurely hosted, allowing an attacker to alter the dependency. This could be, for example, an S3 bucket that has world-writeable permissions configured. An attacker could abuse these permissions to overwrite the hosted dependency with malicious code.
