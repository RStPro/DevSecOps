Although we might think that we are writing a large amount of code when we develop, the truth is that it is only the tip of the iceberg.

Unless you are coding in binary, chances are you are actually only writing a fraction of the actual code. This is because a lot of the code has already been written for us in the form of libraries and software development kits (SDKs).

Even variables like String in an application have an entire library behind them! The management of these dependencies is a vital part of the pipeline.  

## External vs Internal Dependencies

External dependencies are publicly available libraries and SDKs. These are hosted on external dependency managers such as PyPi for Python, NuGet for .NET, and Gems for Ruby libraries.

Internal dependencies are libraries and SDKs that an organisation develops and maintains internally. For example, an organisation might develop an authentication library. This library could then be used for all applications developed by the organisation.

There are different security concerns for internal and external dependencies:

|                                                            Internal                                                             |                                                                                             External                                                                                             |
| :-----------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Libraries can often become legacy software since they no longer receive updates or the original developer has left the company. |                                    Since we do not have full control over the dependency, we must perform due diligence to ensure that the library is secure.                                    |
|                        The security of the package manager is our responsibility for internal libraries.                        |                                        If a package manager or content distribution network (CDN) is compromised, it could lead to a supply chain attack.                                        |
|        A vulnerability in an internal library could affect several of our applications since it is used in all of them.         | External libraries can be researched by attackers to discover 0day vulnerabilities. If such a vulnerability is found, it could lead to the compromise of several organisations at the same time. |

## Common Tools

A dependency manager, also called a package manager, is required to manage libraries and SDKs.

As mentioned before, tools such as PyPi, NuGet, and Gems are used for external dependencies. The management of internal dependencies is a bit more tricky. For these, we can use tools such as JFrog Artifactory or Azure Artifacts to manage these dependencies.

### Security Considerations

Some of the security considerations have been mentioned before.
However, the primary security concern is that dependencies are code outside our control. Especially in modern times, where so many different dependencies are used, it is incredibly hard to track dependencies.
If there are any vulnerabilities in these dependencies, it could lead to vulnerabilities in our application.

### Case Study: Log4Shell

A 0day vulnerability was discovered in Log4j dependency in 2021 called Log4Shell.

Log4j is a Java-based logging utility. It is part of the Apache Logging Services, a project of the Apache Software Foundation.
The vulnerability could allow an unauthenticated attacker to gain remote code execution on a system that makes use of the logger. The true issue? This small little dependency was used almost literally everywhere, as shown by this [XKCD](https://xkcd.com/2347/) cartoon:

![[Pasted image 20250525103556.png]]

This is not an over-exaggeration. Have a look [here](https://github.com/cisagov/log4j-affected-db/tree/develop/software_lists) to see how many different products were vulnerable since they used this dependency. The list got so big that they had to split it alphabetically. This shows the impact of what can happen when a vulnerability is discovered in a dependency.