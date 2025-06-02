_The term CI/CD has changed quite a bit in recent years.
Initially, the primary focus was just on making sure that development was performed using an Agile approach while delivery of the product still occurred using the waterfall model of only deploying final releases.
During this time, it was common for CI/CD to mean Continuous Integration and Continuous Development.
However, quickly it was realized that deployment itself could also be made Agile and the acronym changed to mean Continuous Integration and Continuous Deployment, with development now becoming part of the Integration component.
Finally, they realized that it is not just the deployment, but all aspects around the delivery of the solution and how we monitor it after delivery and the acronym was again changed to now finally mean Continuous Integration and Continuous Delivery.
So you might hear these terms used interchangeably, but they all actually refer to the same thing._

## CI/CD

Since we are constantly building new features for our system or service, we need to ensure that these features will work with the current application.
Instead of waiting until the end of the development cycle when all features will be integrated, we can now continuously integrate new features and test them as they are being developed.

We can create what is called a CI/CD pipeline. These pipelines usually have the following distinct elements:

- Starting Trigger - The action that kicks off the pipeline process. For example, a push request is made to a specific branch.
- Building Actions - Actions taken to build both the project and the new feature.
- Testing Actions - Actions that will test the project to ensure that the new feature does not interfere with any of the current features of the application.
- Deployment Actions - Should a pipeline succeed, the deployment actions detail what should happen with the build. For example, it should then be pushed to the Testing Environment.
- Delivery Actions - As CI/CD processes have evolved, the focus is now no longer just on the deployment itself, but all aspects of the delivery of the solution. This includes actions such as monitoring the deployed solution.  

CI/CD pipelines require build-infrastructure to execute the actions of these elements.
We usually refer to this infrastructure as build orchestrators and agents. A build orchestrator directs the various agents to perform the actions of the CI/CD pipelines as required.  

These CI/CD pipelines are usually where the largest portion of automation can be found. As such, this is usually the largest attack surface and the biggest chance for misconfigurations to creep in.  

## Common Tools

GitHub and Gitlab provide CI/CD pipeline capabilities and are quite popular to use.
GitHub provides build agents, whereas Gitlab provides a Gitlab runner application that can be installed on a host to make it a build agent. For more complex builds, build orchestrator software such as Jenkins can be used. We will explore these tools and their common misconfigurations in later rooms.  

Case Study: A tangle between Dev and Prod

One common misconfiguration with CI/CD pipelines is using the same build agents for both Development (DEV) and Production (PROD) builds.
This creates an interesting problem since most developers will have access to the starting trigger for a DEV build but not a PROD build.

If one of these developers were compromised, an attacker could leverage their access to cause a malicious DEV build that would compromise the build agent. This would not be a big issue if the build agent was just used for DEV builds. However, since this agent is also used for PROD builds, an attacker could just persist on this build agent until a PROD build is actioned to inject their malicious code into the build, which would allow them to compromise the production build of the application.