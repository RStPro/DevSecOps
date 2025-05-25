Source Code Storage

We need to consider several things when deciding where to store our code:

- How can we perform access control for our source code?
- How can we make sure that changes made are tracked?
- Can we integrate our source code storage system with our development tools?
- Can we store and actively use multiple different versions of our source code?
- Should we host our source code internally, or can we use an external third party to host our code?  

The answers to these questions will help us choose the correct source code storage solution for our project.  

## Version Control

We need version control for two main reasons:

- We are often integrating new features in our software. Modern development approaches, such as Agile, means we are constantly updating our code. To keep all of these updates in check, we need version control.
- An entire development team is working on the code, not just one developer. To ensure that we can integrate the changes from multiple developers, version control is required.

Version control allows us to keep multiple versions of the code. This can be the specific version each developer is working on, but it can also be completely different versions of our application, including minor and major versions.

## Common Tools

The two most common source code storage and version control systems are Git and SubVersion (SVN). Git is a distributed source control tool, meaning that each contributor will have their own copy of the source code. On the other hand, SVN is a centralized source control tool, meaning the control of the repo is managed centrally.

GitHub is by far the largest provider of Internet hosting for software development and version control using Git.
You can create a GitHub account and use that to manage your source code repositories (repo). However, you could also host your own git server using software such as Gitlab. For SVN, the two most popular tools are TortoiseSVN and Apache SVN.

However, it should be noted that source code storage solutions such as Gitlab provide much more features than simple storage and version control. Today, these tools can be used for almost the entire pipeline!

## Security Considerations

Our source code is often our secret sauce. As such, we want to make sure it is not exposed. This is why authentication and access control for our source code is so important. We also want to make sure that changes and updates are adequately tracked, allowing us to always go back to a previous version if something happens.

However, we also need to be careful about what we store as part of our source code. Source code cannot be fully secret since developers need access to it. As such, we should be careful not to confuse source code storage with secret management. We need to make sure not to store secrets, such as database connection strings and credentials, in our source code. Since we keep all versions of our source code, even if we remove the secrets in a newer version, they will still be exposed in the previous versions.

Case Study: Git Never Forgets

As mentioned before, version control can end badly for us if we make a mistake. This is a common problem when using version control tools such as Git. There is a saying: _"Git never forgets"_. Code is "committed" to a Git repo. When this happens, Git determines the changes made to the files and creates a new version based on these changes. Any user with access to the repo can look at historical commits and the changes that were made.

What can often happen is a developer accidentally commits secrets such as credentials or database connection strings to a Git repo.

Realizing their mistake, they delete the secrets and create another commit. However, the repo will now have both commits.
If an attacker got access to the repo, they could use a tool such as [GittyLeaks](https://github.com/kootenpv/gittyleaks), which would scan through the commits for sensitive information.
Even if this information no longer exists in the current version, these tools can scan through all previous versions and uncover these secrets.