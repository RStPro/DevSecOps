## External Dependencies

An external dependency is one that has been developed and maintained outside of our organisation. Usually, these dependencies are publicly available (some are free, but some can be paid for SDKs). Some examples of popular external dependencies include:

- Any Python pip package that you install from the PyPi public repositories.
- JQuery and any other publicly available Node Package Manager (NPM) libraries, such as VueJS or NodeJS.
- Paid for SDKs such as Google's ReCaptcha SDK that can be used to integrate captchas into your application. 

External dependencies include almost any dependency that we ourselves have not created. This means that someone outside our organisation is responsible for maintaining the dependency.

## Internal Dependencies

An internal dependency is one that has been developed by someone in our organisation. These dependencies are usually only used by applications that we develop internally in our organisation. Some examples of internal dependencies include:

- An authentication library that standardizes the authentication processes of all our internally developed applications.
- A data-source connection library that provides applications with various techniques to connect to different data sources.
- A message translation library that can convert application messages from a specific format to one that a different internal application can read.

Internal dependencies are usually created to standardize an internal process and ensure that we don't have to reinvent the wheel every time we want that same feature in another application. Since we develop these dependencies ourselves, we, as an organisation, are responsible for maintaining these dependencies.

## External vs Internal

The origin of the dependency does not necessarily make it better or more secure. However, based on the origin of the dependency, the attack surface is different. Meaning we will need to take different security measures to protect each. In this room, we will talk about these security measures for both external and internal dependencies before practically exploiting one of the security concerns internal dependencies have.