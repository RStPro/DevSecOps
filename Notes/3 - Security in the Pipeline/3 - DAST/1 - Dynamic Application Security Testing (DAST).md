## What is DAST?

**Dynamic Application Security Testing (DAST)** is the process of testing a running instance of a web application for weaknesses and vulnerabilities. It focuses on a black-box testing approach where vulnerabilities are found just like a regular attacker would find them. Simply put, DAST identifies vulnerabilities by trying to exploit them, either manually or through automated tools.

By testing the application from an outside perspective, we can abstract ourselves from its inner workings and focus on identifying vulnerabilities that an attacker would likely find. This means the results obtained from DAST will often point to vulnerabilities requiring prioritised attention as they are expected to be found without prior knowledge of the application.

It is important to note that DAST doesn't replace other methods to find vulnerabilities in applications, but rather complements them. A secure development lifecycle will often mix several techniques in order to provide a good enough vulnerability coverage.

## Manual vs Automated DAST

There are two ways in which DAST can be performed:

- **Manual DAST:** A security engineer will manually perform tests against an application to check for vulnerabilities.
- **Automatic DAST:** An automated tool will scan the web application for vulnerabilities.

Both processes are complementary and can be used at different stages of the **Software Development Lifecycle (SDLC)**. Combining manual and automated tools will often yield the best results rather than relying on either separately.

Manual DAST will help us find weaknesses that an automated tool won't easily spot as they don't understand the application from a functional point of view.

The problem with doing everything by hand is that running manual tests for every commit or small change in the code during the development phases will take too much time. This is where Automated DAST excels, as it provides a quick way to run many tests against the target application without requiring human interaction.

## DAST in the SDLC

![[Pasted image 20250607161315.png]]

While every scenario is different, it is common to use automated DAST during the test phases. Automated DAST tools will often be optimized for speed so developers can obtain feedback quickly, unlike a traditional web application vulnerability scanner, which could take several hours to run. The idea here is not to provide an extensive scan of the application but to catch the low-hanging fruit early.  

Manual DAST, on the other hand, is often run periodically to avoid slowing down the development process as a whole. It is usual to run manual scans weekly while applications are being developed, but this greatly depends on each project. A more intense scanning profile can be used in these manual scans to identify even more vulnerabilities.

When the application is ready to go into production, running a full-blown web application pentest is always good practice to notice any flaws in the final product implementation.

**Note:** Most literature will often refer to automated DAST simply as DAST and will often consider manual DAST as part of web application pentesting. Manual DAST might also be referred to as "traditional DAST".

## DAST Pros and Cons

As with any other process used to find vulnerabilities in an application, DAST will have its advantages and disadvantages:

| Pros:<br><br>- Finds vulnerabilities during runtime. This will include vulnerabilities that are specific to the deployment process, which can't be seen by analysing code alone.<br>- DAST will find vulnerabilities like HTTP Request Smuggling, cache poisoning, and parameter pollution that won't be found using SAST.<br>- DAST tools don't care about the programming language in use by your application. Since DAST is black-box testing, all apps are treated in a language-agnostic way.<br>- Reduced number of false positives as compared to SAST.<br>- DAST tools might be able to find some business logic flaws. The effectivity will depend on the tool, and shouldn't be taken as a replacement for manual testing. | Cons:<br><br>- Code coverage isn't the best. DAST may not cover specific situations that will only be triggered by specific use cases in your application.<br>- Some vulnerabilities may be harder to find using DAST, as compared to static code analysis techniques.<br>- Some apps are difficult to be crawled. Modern applications heavily rely on javascript processing for the client-side. This makes it harder for DAST tools to traverse them.<br>- DAST scanners won't be able to tell you how to remediate some vulnerabilities in detail, since they have no idea of the underlying code.<br>- Some types of scans might take lots of time to finish.<br>- You need a running application to do the testing. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
## Ready to DAST?

Most of the time, you will find DAST contextualized as a series of automated tests. However, we will explore how the manual process works to understand better what most tools fundamentally do. In general terms, a DAST tool will perform at least the two following tasks against the target website:

- **Spidering/Crawling:** The tool will navigate through the web app, trying to map the application and identify a list of pages and parameters that can be attacked.
- **Vulnerability Scanning:** The tool will try to launch attack payloads against the identified pages and parameters. The user can typically customize the type of attacks to include only the ones relevant to the target application.

We will use ZAP proxy as our DAST tool for demonstration purposes in this room. Consider, however, that many DAST tools used in enterprise setups are paid and quite expensive but will use the same base principles as any other web application vulnerability scanner. The main difference among tools will be in their vulnerability detection capabilities and how many additional features they add to their product that are useful in enterprises, like dashboards, ticketing system integration and many others.