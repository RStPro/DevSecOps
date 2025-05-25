Maintaining good credential hygiene in CI/CD environments is crucial to protect against potential security risks.
Various systems and individuals within the engineering ecosystem use credentials, such as secrets and tokens, to deploy and access resources and other highly privileged actions.
However, securely managing credentials can be challenging due to the different contexts in which they are used and stored.
Issues such as insecurely storing credentials in code repositories, improper usage in build and deployment processes, leaving credentials in container image layers, printing credentials to console output, and neglecting to rotate credentials can all lead to security breaches.

## Risk Impact:

Attackers highly seek credentials to access valuable resources and enable malicious activities.
Engineering environments offer multiple opportunities for attackers to obtain credentials.
Human error and knowledge gaps in credential management can increase the risk of credential exposure and compromise of critical resources.

## Recommendations:

1. Ensure that credentials follow the principle of least privilege from code to deployment.
2. Avoid sharing the same credentials across multiple contexts to maintain accountability and simplify privilege management.
3. Use temporary credentials whenever possible, and establish procedures to rotate static credentials and detect stale credentials periodically.
4. Ensure credentials are only used under predefined conditions, such as limiting usage to a specific IP address or identity.  
5. Detect secrets pushed to and stored in code repositories using Integrated Development Environments (IDE) plugins, automatic scanning, and periodic repository commit scans.
6. Use built-in vendor options or third-party tools to prevent secrets from being printed to console outputs during builds and ensure existing outputs do not contain secrets.
7. Verify that secrets are removed from artifacts, such as container image layers and binaries.

Organizations should consider implementing the above best practices to mitigate the risks of insufficient credential hygiene.

## Environment Variables and Best Practices:

The use of environment variables is an excellent method of promoting credential hygiene.
As part of software development and deployment processes, environment variables are commonly used to store and manage configuration information.
They store sensitive information, such as API keys, passwords, and other credentials. You can manage environment variables securely by following these best practices:

1. Avoid hard-coding sensitive information in code; use environment variables instead.
2. Regularly review and **rotate** credentials stored in environment variables.
3. Limit access to environment variables to authorized personnel only.  
4. Environment variables should be set according to the principle of least privilege.
5. Implement monitoring and auditing mechanisms to track changes to environment variables.
6. If implementing a secrets manager solution (explained in the next task), review its encryption mechanisms and if it's a good fit for your development environments.

**Note:** Implementing environment variables does not mean you are free from compromise.
Following best practices is essential for ensuring they are appropriately implemented.