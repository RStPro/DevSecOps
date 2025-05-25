## Unit Testing

When talking about automated testing in a pipeline, this will be the first type of testing that most developers and software engineers are familiar with.
A unit test is a test case for a small part of the application or service. The idea is to test the application in smaller parts to ensure that all the functionality works as it should.

In modern pipelines, unit testing can be used as quality gates.
Test cases can be integrated into the Continuous Integration and Continuous Deployment (CI/CD) part of the pipeline, where the build will be stopped from progressing if these test cases fail. However, unit testing is usually focused on functionality and not security.

## Integration Testing

Another common testing method is integration testing.
Where unit tests focus on small parts of the application, integration testing focuses on how these small parts work together.
Similar to unit tests, testing will be performed for each of the integrations and can also be integrated into the CI/CD part of the pipeline.
A subset of integration testing is regression testing, which aims to ensure that new features do not adversely impact existing features and functionality. However, similar to unit testing, integration testing, including regression testing, is not usually performed for security purposes.  

## Security Testing

So if the first two types of automated testing are not for security testing, which are? There are two primary types of automated security testing.

### SAST  

Static Application Security Testing (SAST) works by reviewing the source code of the application or service to identify sources of vulnerabilities.
SAST tools can be used to scan the source code for vulnerabilities. This can be integrated into the development process to already highlight potential issues to developers as they are writing code.

We can also integrate this into the CI/CD process. Not as quality gates, but as security gates, preventing the pipeline from continuing if the SAST tool still detects vulnerabilities that have not been flagged as false positives.  

### DAST

Dynamic Application Security Testing (DAST) is similar to SAST but performs dynamic testing by executing the code.
This allows DAST tools to detect additional vulnerabilities that would not be possible with just a source code review.
One method that DAST tools use to find additional vulnerabilities, such as Cross Site Scripting (XSS), is by creating sources and sinks.
When a DAST tool provides input to a field in the application, it marks it as a source.
When data is returned by the application, it looks for this specific parameter again and, if it finds it, will mark it as a sink. It can then send potentially malicious data to the source and, depending on what is displayed at the sink, determine if there is a vulnerability such as XSS.

Similar to SAST, DAST tools can be integrated into the CI/CD pipeline as security gates.

### Penetration Testing

Sadly, SAST and DAST tools cannot fully replace manual testing, such as penetration tests.
There have been significant advancements in automated testing and even in some cases, these techniques were combined with more modern approaches to create new testing techniques such as  Interactive Application Security Testing (IAST) and Runtime Application Self-Protection (RASP). However, the main issue remains that these tools, including these modern testing techniques, do not perform well against contextual vulnerabilities. Take the process flow of a payment, for example.

A common vulnerability is when part of the process can be bypassed, for example, the credit card validation step. This is an easy test case to perform manually, but since it requires context, even DAST tooling will find it hard to discover the bypass. Similarly, business logic and access control flaws are hard to discover using automated tools, whereas manual testing can discover them fairly quickly. It is not that automated tooling will never be able to find these flaws, it is simply more cost-effective to use manual testing.  

### Common Tools

There are several common tools that can be used for automated testing.
Both [GitHub](https://github.com/features/security/code) and [Gitlab](https://docs.gitlab.com/ee/user/application_security/sast/) have built-in SAST tooling.
Tools such as [Snyk](https://snyk.io/) and [Sonarqube](https://www.sonarqube.org/) are also popular for SAST and DAST.  

Case Study: She can't take any more captain, She's gonna blow!  
A common issue with SAST and DAST tooling is that the tool is simply deployed into the pipeline, even simply for a Proof-of-Concept (PoC).
However, you need to take several things into consideration:

- Performance cost
- Integration points
- Calibration of results
- Quality and security gate implementation

The first and last point is very important and can be costly if ignored.
The initial PoC of the tool should probably occur after hours since it will have to scan through all code.

This process can impact the performance of your source code control tool significantly.
Imagine this happening just before a big release, and developers cannot stage and push their latest commits.

Furthermore, as more organisations move to a more agile approach to software development, most repos receive several hundred commits daily. If you introduce a new security gate, even just for a PoC, that scans each merge request for vulnerabilities before approval, this can have a drastic performance cost on your infrastructure and the speed at which developers can perform merge requests.

When introducing new automated testing tooling, careful consideration should be given to how a PoC should be performed to ensure that no disruptions are caused but also to ensure that the PoC is representative of how the tooling will interact when it is finally integrated.
A fine balance to try and achieve!