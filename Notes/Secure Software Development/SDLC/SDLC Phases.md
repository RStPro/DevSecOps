### Introduction

The first phases focus on breaking down the project or application before moving on to the development of the application.

### 1. Planning

As part of the Planning Phase, also known as the Feasibility Stage, the scope and purpose of the application are determined. Software development is planned and implemented using it. Additionally, it helps to keep the project focused on its original purpose while setting boundaries. Here, the system's problem and scope are defined, and the requirements for its upcoming design can be determined. The process of devising an effective outline for the forthcoming development cycle should enable issues to be caught before they have a detrimental effect on the process. And help them identify the resources they need to make their plan happen. The planning stage can be crucial if the goal is to have a product ready for market by a specific date.

### 2. Requirements Definition

A system's requirements stage involves defining the prototype ideas and gathering all the necessary details. This may be in the form of:  

- Making a list of all the requirements for the prototype system  
- Prototypes should be evaluated for alternatives  
- Identify the end user's needs through research and analysis  

Planning for the application involves defining the requirements to determine what it should do, and its needs. An application that uses social media, for example, will require you to connect with a friend or in some inventory programs, there is a search feature. Defining the resources needed to build the project according to the requirements is also critical. For example, software might be developed to control a custom manufacturing machine. A device is required for the process. It is common for developers to produce a document known as a software requirement specification (SRS).

### 3. Design and Prototyping

It is first necessary for developers to outline the details of the overall application, including its attributes, such as:  

- Interfaces for users  
- Interfaces between systems  
- Requirements for networks  
- Instances of databases  

SRS documents are usually converted into logical structures implemented in programming languages. Plans for operating, training, and maintaining the system will be drawn up to ensure developers know what they need to do throughout the life cycle. Here are a few examples: An architecture specifies how codes are written, industry practices, the overall design and any templates or boilerplates used within the program. Input is received and processed by the software through the user interface, which defines how the software interacts with customers. Defining a platform means choosing which media will run the software. It is not only about programming languages but also about solving problems and performing tasks in an application. A communication method specifies how an application communicates with other assets, such as a central server or other instances of the application. Application security measures may include SSL traffic encryption, password protection, and secure user credentials storage.

A document called an Architecture Design Review (ADR) is typically created by engineers and developers at this stage to ensure that all teams working in different areas are on the same page. In the case of an API endpoint, for example, front-end and back-end developers and teams handling authentication and authorisation will be involved in the ADR process.

### 4. Software Development

Code is written, and an application is developed based on specifications outlined in earlier design documents. Software developers appreciate instructions and explanations. Playbooks and guides for the application can be documented as part of the documentation process. Developers will use compilers, debuggers, and interpreters to adhere to coding guidelines established by the organisation. A very effective initiative to promote secure coding would be incorporating code hygiene, code best practices and security in playbooks.

### 5. Testing

﻿It's critical to test an application before making it available to users. During the testing stage, developers will review their software using automated tooling, like source code scanners. The project's goal is to meet the previously defined quality standards during the planning and requirement stages. Testing is an essential pillar in moving toward a more Secure Development Lifecycle. To introduce testing effectively in the SDLC, it has to go through its own "Software Testing Lifecycle" phases. Sometimes, there are dedicated teams as part of a testing function. For example, a Quality Team with Quality Analysis (QA) Engineers. The most notable phases when introducing testing are test case design and development, test environment set up and test execution.  
  
**Test case design and development**  
With the test plan in place, testers can begin writing and creating detailed test cases. In this phase, the QA team fleshes out the details of the structured tests they will run, ensuring that it meets the requirements set in the previous SDLC phases. When conceptualising test cases, the tester's goal should be to validate functionality within the allotted time and scope, especially core functionality. Test cases should be simple, well understood by any team member, and unique from other test cases. Test cases must be identifiable and repeatable, as developers will add new functionality to the product over time, requiring tests to run again. They can't change the test environment for future tests, especially when validating configurations. Test cases might also require maintenance or updates over time to validate both new and existing functionality. Once test cases are ready, a test team lead or peer can review them or check and update automated test scripts.  

  
**Test environment setup**  
The test environment provides the setting where the actual testing occurs. Testers must access bug reporting capabilities and the application architecture to support the product. Once ready, testers establish the test environment's parameters, including the hardware, software, test data, frameworks, configurations and network. For example, most of a product's users might be on an Android device, use a specific version of a Chrome browser and have a certain amount of processing power on those devices. These are parameters the test environment would include.  

  
**Test execution**  
At this stage, testers execute all test cases. For example, QA engineers and automated scripts run several functional and non-functional tests. Testers will identify and report detailed bugs from test case execution and log the system's performance compared to its requirements. Often testers retest the product, as part of regression testing, as developers make fixes to ensure new flaws don't get into production. With all of these tests piling up in the test execution phase, it's essential to use test automation to achieve the test coverage and velocity you need. Developer velocity is a metric that helps us understand and estimate how much development our team can perform in a given timeframe.  

### 6. Deployment

After testing, the overall design for the software starts to come together, and different modules or configurations are integrated into the primary source code. After this stage, the software is theoretically ready for market and provided to end-users. Many companies automate the deployment phase using tools we will later see in the DevSecOps pathway. These tools focus on what you call "Software Deployment tools" for release management; the focus is on automating software rollouts so that teams can deploy new applications on all machines or just selected ones. This is particularly important if the new package requires actions to deploy correctly (a reboot of the machine, for example). Popular Software Deployment tools are [Netlify](https://www.netlify.com/) and [Argo CD](https://argoproj.github.io/cd/). During the deployment phase, a new feature on the company's website can be released, or in the case of mobile development, download a new application version on a smartphone. Furthermore, automating the deployment processes also allows the capability to rollback a deployment, making it easier to go back if there are any unforseen circumstances with the deployment.  

### 7. Operations and Maintenance

Developers must now move into maintenance mode and begin practising any activities required to handle issues reported by end-users. Furthermore, developers are responsible for implementing changes the software might need after deployment. In this phase, users discover bugs they didn't find during testing. For example, handling residual bugs that could not be patched before launch or resolving new issues raised during user reports.﻿ Developers now focus more on stability and uptime than developer velocity, and operations teams now have a stake in developer velocity and their traditional role of maintaining uptime. When it comes to the specific part of operations in DevOps, this often means:

- They enable self-service for developers to promote developer velocity, where developers seek their solutions. Operations teams work closely with developers to provide on-demand access to secure, compliant tooling and environments.
- They standardise tooling and processes across the business. The best way to enable a sustainable self-service model and empower teams to work autonomously is by standardising tooling. Tools and techniques that are standardised and well documented enable organisational unity and greater collaboration. This reduces the friction developers and operations teams experience when sharing responsibilities.
-  They are bringing extensible automation to traditional operations tasks. DevOps teams focus on empowering other teams through self-service and collaboration. Standard operations tasks like resolving incidents, updating systems, or scaling infrastructure still need to be addressed. When development and DevOps work closely together, teams automate the repeatable tasks and drive consistency across the organisation. DevOps teams can track and monitor metrics thanks to consistency and automation of tasks. For example, by automating the creation of virtual machines in the cloud through Terraform, you can log activity for virtual machines created and accessed. You can extend this further by creating alerts for how the service accounts/roles are used to develop infrastructure from a security and compliance point of view. As operations teams shift towards greater automation, 'X' as code becomes the new normal. As example of this would be [Vagrant](https://www.vagrantup.com/) or [Ansible](https://www.ansible.com/). The code controlling operations systems must be stored, versioned, secured, and maintained.