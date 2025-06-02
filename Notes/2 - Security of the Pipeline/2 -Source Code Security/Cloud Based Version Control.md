Cloud-based version control is a modern approach to managing source code in software development, where the codebase and version history are stored in the cloud. It allows developers to collaborate on code from anywhere, providing a flexible and scalable solution for distributed teams.

Cloud-based version control platforms offer easy access, real-time collaboration, robust version history management, and seamless integration with other development tools.
Overall, it provides a scalable, collaborative, and efficient solution for managing source code in modern software development workflows.  

﻿**Github**

﻿Github is cloud-based, and it helps developers store and manage source code from everywhere in the world.
﻿It is the oldest of the services. Chris Wanstrath, P.J. Hyett, Tom Preston-Werner, and Scott Chacon founded the company in 2007 and developed it using Ruby on Rails (see more of Git’s history [here](https://pslmodels.github.io/Git-Tutorial/content/background/GitHubHistory.html)).
﻿Since it was the first open-source code repository on the web, GitHub became the dominant platform. In the present day, developers can host their code and review it.

**CI/CD with ﻿GitHub Actions**

Continuous Integration and Continuous Deployment (CI/CD) is a method to introduce automation into the stages of app development or the Software Development Lifecycle.
It introduces ongoing automation and continuous monitoring from the integration phases to delivery and deployment.
All these together are what you would call a CI/CD pipeline.
Github launched **Actions** in 2018; it is Github’s way of evolving to give developers powerful automation and Continuous Integration & Deployment.
It comprises “Workflows”, where you can declare (via actions) how to build the code through the development pipeline.
You can create activities like push, issue creation, or a new release. For example, to build a container or to deploy a web service.

**GitLab**

Throughout the DevSecOps [path](https://tryhackme.com/path/outline/devsecops), we’ll be using GitLab.
Like GitHub, GitLab is an open-core company that provides a DevOps software package that combines the ability to develop, secure, and operate software in a single application.
Founded in 2014, GitLab was created by Ukrainian developer Dmitriy Zaporozhets and Dutch developer Sytse Sijbrandij.

Fun Fact, it was considered the first partly Ukrainian unicorn, valued at over $1 billion in 2018.
From day one, GitLab was designed to be a set of collaboration tools and a code repository service.
GitLab eliminates the need for third-party integration as it includes CI/CD tools by default, making it a convenient all-in-one solution for software development.

**CI/CD with GitLab**  

GitLab’s CI/CD functionality allows developers to automate their software delivery pipeline, from building and testing to deploying and monitoring.
GitLab uses “runners” - agents that execute jobs - to enable continuous integration and continuous deployment.
With GitLab’s CI/CD features, developers can create custom workflows, define stages, and specify jobs to be executed in parallel or sequentially.
This enables teams to achieve efficient and reliable automation of their development and deployment processes.

GitLab also emphasizes reliability by providing features such as a built-in container registry, built-in continuous deployment to Kubernetes, and GitLab Pages for hosting static websites. Additionally, GitLab allows for creating multiple stable branches beyond the main branch, providing better version control and release management.

In summary, GitLab’s built-in CI/CD capabilities, focus on reliability, and all-in-one DevOps platform makes it a robust software development and deployment solution.