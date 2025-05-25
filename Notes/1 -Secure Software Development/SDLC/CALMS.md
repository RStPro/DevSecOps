Introduction

[CALMS](https://www.atlassian.com/devops/frameworks/calms-framework), as explained in the Atlassian post, is a framework that assesses a company's ability to adopt DevOps processes. The acronym was coined by Jez Humble, co-author of "The DevOps Handbook," which stands for Culture, Automation, Lean, Measurement, and Sharing.

### Culture  

As highlighted in the [Intro To DevSecOps](https://tryhackme.com/jr/introductiontodevsecops) room, DevOps isn't simply a process or a different approach to development; it's a culture change. For any DevOps adoption to be successful, an organisation will have to make a culture shift. Rather than the slower, full-release approach of the waterfall model, teams will have to adopt new strategies to break projects into smaller tasks that can be completed and then presented in a series of sprints. This culture shift is required for all employees, including not only the development teams but also QA, product management, and operations.  

### Automation﻿

A large part of DevOps is the focus on automation. Since we are breaking projects into smaller components, it would be inefficient to then manually integrate these components into the final solution. Thus, it is better to spend some time creating automated processes that can ensure that new feature integrations can occur in a reliable and repeatable manner. This is usually started on the continuous delivery side of things for new teams. But as teams mature, it will also move to continuous integration.

Mature teams can also look to automate the configuration itself through tools such as configuration as code. This means that the configuration of the application itself is defined in code, which would alter build instructions depending on the environment that the application is being built for. This streamlines the process of building production-ready code, and configuration parameters could be used to reduce the verbosity of errors and remove developer bypasses before the code is built for the production environment.

### Lean  

By implementing DevOps, we want to make sure that tasks are broken as small as possible. This allows teams to create initial versions of applications sooner. The common principle is that we are constantly improving our software, but it is more valuable to get a version of our application in the hands of users earlier rather than having to wait years until the product is fully perfected. Thus, we start with a lean first version that is constantly improved with time. This method also allows our user base to provide feedback and a wishlist of features for the application.

### Measurement

When implementing DevOps, it is important to have some sort of measure of effectiveness. These metrics are important since they will help us make small changes to our processes and ensure that we are constantly improving. In the next task, we will elaborate on how DevOps handles measurement and essential metrics to seek constant improvement and monitoring.

### Sharing  

In an effective DevOps pipeline, there is a shared responsibility for the overall application between all teams, including development and operations. Understanding that all team members are required to deliver the final solution and share in the responsibility to do so will result in a better product for users.