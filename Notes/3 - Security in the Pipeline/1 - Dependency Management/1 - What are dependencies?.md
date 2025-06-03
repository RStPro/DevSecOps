## The Scale of Dependencies  

While you may think that you are writing an incredible amount of code when you are developing an application, it pales in comparison to the amount of code that is actually performing actions for you in the various dependencies that you include. Let's take a look at a simple Python example.

![[Pasted image 20250603194234.png]]

In this example, we are using the NumPy library to create two arrays and then multiply them with each other. We effectively wrote about four lines of code. However, just that first line, `import numpy`, executes a `__init__.py` file in the background that contains 400 lines of code with an additional 30 imports. With a conservative estimate of 250 lines of code per import, this means that our one line of code has executed roughly 8000 lines of dependency code!

If we extrapolate this data, you are probably only responsible for 0.01% of all the code in your application, and dependencies make up the remaining 99.99% of the code! This is why dependency management is vital for the security of any pipeline or software development lifecycle (SDLC) process.

## Dependency Management

Dependency management is the process of managing your dependencies through your SDLC process and DevOps pipeline. We perform dependency management for several reasons:

- Knowing what dependencies our application uses can allow us to support it better.
- We often want to version lock dependencies to improve the stability of our application since newer versions may add new features or deprecate features that our application actively uses.
- We can build golden images that already have all our dependencies installed, meaning we can perform faster deployment cycles.
- When new developers are onboarded, we can help them set up their development machine by installing all the required dependencies.
- We can monitor the dependencies we use for security issues to ensure that dependencies are upgraded with the security fixes as needed.

Most large organisations use tools for dependency management, such as [JFrog Artifactory](https://jfrog.com/artifactory/). This allows the organisation to manage all of their dependencies from a central location and allows dependency management to be integrated into our DevOps pipeline. Build servers and agents can make requests to the dependency manager to be provided with dependencies when the application is being built or deployed.