During the process of manually creating infrastructure, deployments are blocked. There may be too many errors in the live application, indicating that the security test automation needs to be improved or is taking too much computing power and time. Understanding how and where to find improvement requires metrics to measure your resources. Here are the essential metrics gathered by engineers and the questions it aims to answer:

- Meantime to production ([MTTP](https://about.gitlab.com/handbook/engineering/infrastructure/team/delivery/metrics.html)). What is the turnaround time for newly committed source code?
- Frequency of deployment. What is the frequency of deployment of releases? The average lead time. How long does it take to develop, build, test, and deploy a new feature?
- Speed of deployment. A new release is deployed into production; how long does it take?
- Deployment Agility. You can measure deployment agility by combining deployment speed and frequency.
- Production failure rate. How often do failures occur in production?
- MTTR stands for mean time to recover. What is the recovery time after a failure?

MTTP

One critical DevOps metric to track is the mean time production. MTTP is the length of time between when a code change is committed and when it is in a deployed state. A pre-release test, for instance, is passed when all code requirements have been met. Test automation and working in small batches are good ways to improve MTTP time. Developers can receive fast feedback on the code they commit by following these practices, identifying flaws, and fixing them as quickly as possible.   

Failure Rate

When a code change goes into production, a certain percentage of code changes require hot fixes or other remediation measures. It does not measure failures caught during testing and fixes before the code is deployed. The same practices that enable shorter MTTP times correlate with reducing change failure rates. All these practices make bugs much easier to identify and remediate. Tracking and reporting failure rates are essential for ensuring new code releases meet security requirements.

Deployment frequency

Understanding how often new code is deployed into production is critical to DevOps' success. Deployment frequency defers to MTTP as it measures when it's released into a pre-production staging environment and reserves "deployment" to refer to code changes released into production. Teams can deploy changes on-demand and often many times a day. The ability to deploy on-demand requires a deployment pipeline that incorporates automated testing and feedback mechanisms, as mentioned in the previous tasks, minimising the need for human intervention. 

MTTR

When a partial or total service interruption occurs, the mean time to recovery (MTTR) is measured. Keeping track of this metric is crucial. If a failure occurs, a fix must be deployed as soon as possible, or the changes that caused the failure must be rolled back. In most cases, this involves monitoring system health continuously and alerting operations in the event of a failure. The operations team have the necessary processes, tools, and permissions to resolve incidents. 

Communicating Risk

You can demonstrate improvement over time by measuring any of these, and you'll have the evidence to support the buy-in from the business and teams. Risk means very different across teams. For DevSecOps engineers, risk means the likelihood of a vulnerability being exploited and its impact on systems. Whereas for a DevOps engineer, a significant risk would be high rates of production failure, for example. By understanding other teams' definitions of risk, a DevSecOps engineer can find common ground and better build a perception of security risk for other teams.