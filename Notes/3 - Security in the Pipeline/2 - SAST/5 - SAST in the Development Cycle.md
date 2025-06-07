SAST is one of the first tools to appear during the development lifecycle. It is often implemented during the coding stage, as there's no need to have a functional application to use it.

![[Pasted image 20250607155618.png]]

Depending on each case, SAST can be implemented in one of the following ways:  

- **CI/CD integration:** Each time a pull request or a merge is made, SAST tools will check the code for vulnerabilities. Checking pull requests ensures that the code that makes it to merges has undergone at least a basic security check. On some occasions, instead of checking every single pull request, executing SAST scans only at merges may help prevent slowdowns in the development pipeline, as it avoids making all developers wait for full SAST scans.
- **IDE integration:** SAST tools can be integrated into the developers' favourite IDEs instead of waiting for a pull request or merge to occur. This way, the code can be fixed as early as possible, saving time further ahead in the project.

Note that you may want SAST running on both the developers' IDEs and your CI/CD pipeline, which would be valid. For example, IDE tools may run basic structural checks and enforce secure coding guidelines, while CI/CD integrations may run more time-consuming dataflow/taint analysis. Remember that your specific setup will depend on the requirements of each project and should be evaluated by the team carefully.

If you want to learn how security tools can be integrated into a CI/CD pipeline, check the [DAST room](https://tryhackme.com/room/dastzap) for an example of integrating a DAST tool into a Jenkins pipeline. The process with SAST tools is pretty similar, so we won't repeat it here.  

## Integrating SAST in IDEs

Your virtual machine has the VS Code editor installed and already configured to use a couple of SAST tools:

- **Psalm:** The tool we've been using supports IDE integration by installing the Psalm plugin into VS Code directly from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=getpsalm.psalm-vscode-plugin). This plugin will check anything you type in real-time and show you the same alerts as the console version directly into your code. Taint analysis won't be available, so you'll only see the structural problems reported on a basic Psalm analysis.

- **Semgrep:** Yet another SAST tool that can be installed into VS Code directly from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=Semgrep.semgrep). Just as with Psalm, it will show inline alerts directly in your code. Semgrep even allows us to build custom rules if needed. You can check the rules that are loaded for this project on the `semgrep-rules` directory inside the project's directory. The specifics on how to build Semgrep rules will be left for a future room, so don't worry about them now. You can check the rules in the directory, but this won't be required for this room.

Both tools will work similarly by showing any problems detected directly inline in your code. The only notable difference is that Semgrep will run when you start VS Code and will show you the problems it detects on all of the files, while Psalm will only show you issues related to the file you are currently editing. The plugins will add the following information to your IDE screen:

![[Pasted image 20250607155848.png]]

For each line where issues are detected, you can get additional information by hovering the mouse pointer over it. Here's what you would get by hovering over line 46 of `login.php`:

![[Pasted image 20250607155915.png]]

You can also check the complete list of issues by clicking the Errors indicator at the bottom of VS Code's screen:

![[Pasted image 20250607155930.png]]

Having your IDE check for problems allows you to produce cleaner code as a developer, contributing significantly to the overall security of your final application.