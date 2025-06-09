When using IaC, regardless of whether the deployment is on-prem or cloud-based, there are several things to consider for security. If you are looking for security best practices, cheat sheets such as [these from OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Infrastructure_as_Code_Security_Cheat_Sheet.html) are a good place to start. Even frameworks such as [NIST](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-204C.pdf) provide information on how to secure IaC.

However, in this room, we will focus more on the practical security of IaC and common mistakes that are seen in the real world. This is not a comprehensive list of things to take into consideration, but it is a great start either protecting your IaC pipeline against real-world attacks or what to look for if you are attacking an IaC pipeline on a red team engagement. In total, there are four main elements to consider.

## Dependencies

The first element of IaC pipelines where security has to be considered is the dependencies. Similar to a software pipeline, our IaC pipeline will have dependencies. In IaC pipelines, the biggest dependencies are the base images that are pulled and used to build the infrastructure. If these dependencies have any security issues, these issues will propagate through the pipeline.

A common example would be a vulnerability in the OS version of the image. If the image itself is not updated, the deployed hosts would have this vulnerability. As such, it is important to ensure adequate dependency management for resources used in the IaC pipeline. Anytime you are making use of third-party software or systems, it can introduce a dependency risk. For more information on dependency management and the potential vulnerabilities, have a look at the [Dependency Management](https://tryhackme.com/room/dependencymanagement) room.

## Defaults

A common security flaw in IaC pipelines is not altering **defaults**.

When hosts and services are initially provisioned through an IaC pipeline, it is extremely common for these systems to be provisioned using default credentials or connection strings. Ultimately, this is intended as these default credentials are used by the tools in the pipeline to provision the hosts. The security misconfiguration is therefore not the default credentials, but not removing or altering them as the final step in the IaC deployment.

An example of default credentials is the credentials used by Vagrant to provision Windows hosts.
Windows images provisioned by Vagrant often have a built-in default account of `vagrant` that has the password of `vagrant`. This is to allow the Vagrant script running on the hypervisor to connect to the host for file transfer and script execution. If, at the end of the deployment, this default user is not removed, a threat actor could use this to connect to and take full control of all hosts deployed through the IaC pipeline.

Another issue with defaults is in the services deployed on the hosts.
Let's say, for instance, that our IaC pipeline is used to deploy a CI/CD pipeline and would therefore install the Jenkins role on one of the hosts. It would be common for this role to be installed with the default credentials of Jenkins, which would be `jenkins:jenkins`. In this case, we cannot really alter these credentials in the last stages of the IaC deployment but expect the software engineers that will use the CI/CD infrastructure to alter the credentials. In some cases, this is not performed, which then leads to insecure infrastructure in the deployment. In other cases, even if the software would require the user to change their password with the first logon event, as the software is never used, the default credential remains, allowing a threat actor to compromise the service and potentially its underlying infrastructure.

As such, when building an IaC pipeline, it is important to make note of cases where defaults are used and where they may be a risk if not altered.
The alteration of these defaults should then either be embedded as the final steps in the IaC pipeline or, where required, be performed manually once the deployment is complete.

## Insufficient Hardening

The third element that commonly goes wrong in IaC pipelines is insufficient hardening.
The primary goal of IaC is to rapidly deploy infrastructure. This often means that the infrastructure that is being deployed has not yet been fully hardened. Hardening is not something that just happens automatically; it has to be planned for. As such, it is important to ensure that hardening steps are either embedded in the IaC pipeline or performed manually post-deployment.

A common example of insufficient hardening is the services used by the IaC pipeline for deployment.
For example, when Vagrant does provisioning of a Windows host, it does this via a WinRM connection.
It just so happens that WinRM is a service commonly used by threat actors for lateral movement. As such, it is important that if the service is no longer required for normal operation post-deployment, it should be disabled. When planning your IaC pipeline, it is important to include not only general hardening steps but also those that would close down the services used by the pipeline itself.

## Remote Code Execution as a Feature

The last element to consider is to remember that, ultimately, IaC pipelines are nothing more than remote code execution as a feature.
In essence, the pipeline is effectively executing code that allows for new infrastructure to be created and integrated into existing networks. While this is incredibly powerful in the right hands, it could also be extremely detrimental.

Taking this into consideration, it is important to apply security to the IaC pipeline to prevent unauthorized access. This can be done through two main security efforts, namely secret management and following the principle of least privilege.

With secret management, we can ensure that sensitive information, such as final credentials or keys, is securely stored and cannot simply be read from the IaC source code to compromise the deployment.

Following the principle of least privilege ensures that access to the IaC pipeline is only provided to users and services that require it. This includes implementing the same security controls that should be in any pipeline as taught in the [CI/CD and Build Security](https://tryhackme.com/room/cicdandbuildsecurity) room. If a threat actor can compromise the pipeline, they would often have the ability to also compromise the deployed infrastructure.

These are some of the key security considerations that are required to secure your IaC pipeline against real-world threats. Now that you know what to look for, let's use this knowledge to attack a vulnerable IaC pipeline!