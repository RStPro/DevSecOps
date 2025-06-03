Internal dependencies are any libraries or SDKs that we have developed internally in our organisation. As such, we are responsible for all aspects of the security of the dependency and its management. As mentioned before, the primary reason for creating internal dependencies is to ensure that we don't have to reinvent the wheel every time we develop an application. Internal dependencies allow us to standardize certain processes, such as authentication, registration, and communication.

## Security Concerns  

Internal dependencies have similar security concerns as external dependencies. Although internal dependencies allow us to standardize a process, if the dependency has a vulnerability, it will affect several different applications in the organisation. We, therefore, have to perform security testing of our dependencies before they are released for use.

Another issue is that internal dependencies can become legacy code incredibly fast. The developer that created and maintained a dependency has started work elsewhere, meaning the dependency no longer receives updates. If such a dependency is used in several applications, it can become an issue if a vulnerability is discovered. This problem can only be made worse if the documentation is not kept up to date, allowing someone new to take responsibility for the dependency.

A unique security concern to internal dependencies is storage. We want to ensure that a dependency can be accessed by all developers for use, but not modification. If all developers can simply modify the dependency, an attacker would simply have to compromise a single developer to compromise several applications. Hence we need to protect write-access to dependencies. In some organisations, even read access is restricted to reduce the attack surface further.

## Tools

Applications and tools must be used to manage internal dependencies effectively. These tools would differ based on our needs. If we develop code only in a single language such as Python, we could simply host an internal PyPi repository server. This would allow us to upload and install packages similar to how it is performed using pip and the internet-facing PyPi repository.

However, if we develop applications in different languages, we may opt to use a dependency manager such as [JFrog Artifactory](https://jfrog.com/artifactory/). JFrog Artifactory allows dependencies to be centrally managed and integrated into the DevOps pipeline. As developers are writing code, they can make use of the various dependencies hosted on Artifactory. Artifactory also has the ability to manage external dependencies that are used internally as well. It provides a single source for all dependencies.

While such tools are great to help us manage dependencies internally, if they are compromised, it would lead to a significant impact. One such attack that can be performed against dependency managers is Dependency Confusion, which will be discussed in more detail in the next task.