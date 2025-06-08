Compliance and benchmarking play vital roles in securing assets - let alone containers. Let us begin by explaining compliance.
Compliance is the process of following regulations and standards such as the NIST SP 800-190, a set of standards from the National Institute of Standards and Technology that gives guidance and best practices on container security:

| **Compliance Framework** | **Description**                                                                                                                                                              | **URL**                                                                                                                  |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| NIST SP 800-190          | This framework outlines the potential security concerns associated with containers and provides recommendations for addressing these concerns.                               | [https://csrc.nist.gov/publications/detail/sp/800-190/final](https://csrc.nist.gov/publications/detail/sp/800-190/final) |
| ISO 27001                | This framework is an international standard for information security. The standard guides implementing, maintaining and improving an information security management system. | [https://www.iso.org/standard/27001](https://www.iso.org/standard/27001)                                                 |

Please note that you may have to adhere to additional frameworks relevant to your Industry. For example, financial or medical. Regulations exist in all industries. For example, in the medical field, the HIPPA for handling medical data.

Benchmarking, on the other hand, is a process used to see how well an organisation is adhering to best practices. Benchmarking allows an organisation to see where they are following best practices well and where further improvements are needed:

| **Benchmarking Tool** | **Description**                                                                                                                                                                                           | **URL**                                                                                    |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| CIS Docker Benchmark  | This tool can assess a container's compliance with the CIS Docker Benchmark framework.                                                                                                                    | [https://www.cisecurity.org/benchmark/docker](https://www.cisecurity.org/benchmark/docker) |
| OpenSCAP              | This tool can assess a container's compliance with multiple frameworks, including CIS Docker Benchmark, NIST SP-800-190 and more.                                                                         | [https://www.open-scap.org/](https://www.open-scap.org/)                                   |
| Docker Scout          | This tool is a cloud-based service provided by Docker itself that scans Docker images and libraries for vulnerabilities. This tool lists the vulnerabilities present and provides steps to resolve these. | [https://docs.docker.com/scout/](https://docs.docker.com/scout/)                           |
| Anchore               | This tool can assess a container's compliance with multiple frameworks, including CIS Docker Benchmark, NIST SP-800-190 and more.                                                                         | [https://github.com/anchore/anchore-engine](https://github.com/anchore/anchore-engine)     |
| Grype                 | This tool is a modern and fast vulnerability scanner for Docker images                                                                                                                                    | [https://github.com/anchore/grype](https://github.com/anchore/grype)                       |

An example of using the Docker Scout tool to analyse a Docker image has been provided in the terminal below. Please note this will need to be [installed](https://github.com/docker/scout-cli) beforehand. You can read the [Docker Scout](https://docs.docker.com/scout/) documentation to learn more.

![[Pasted image 20250608182449.png]]

