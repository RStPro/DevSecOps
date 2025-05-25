To fetch a project from GitLab, Git uses a command called clone.

The syntax looks something like this:   

```
git clone <repository_url>
```

It’s used to copy (clone) an existing repository (repo) at **another location** in a new directory (**repositories**).
Local filesystems or remote machines accessible by supported protocols can host the original repository.
Working copies of Git repositories have their history, manage their files, and are isolated from their source repositories.
The repository you create on your computer contains all the files and directories of your project.
You can think of a branch as different versions of your repository or as an independent development line.
Various versions of a repository can be contained in multiple **branches**.

```
git clone -branch
```

The _-**branch**_ argument allows you to specify a branch to clone instead of the default branch the remote is pointing to. 

```
git clone -branch name_of_branch <repository_url>
```

The above example would clone only the name_of_branch from the remote Git repository. 

Branching is a common feature in most Version Control Systems (VCS) that allows you to diverge from the main line of development and work on changes without affecting the main line. Git, a popular VCS, has a unique and powerful branching model that sets it apart. Git branches are lightweight, making branching operations fast and switching between branches quickly. Git encourages frequent branching and merging, even multiple times daily, which is critical to efficient project development. 

## Understanding Git’s Branching Model

To understand Git’s branching model, it’s essential to know how Git stores its data.
Git does not store change-sets or differences; instead, it keeps snapshots of the content.
When you make a commit in Git, it creates a commit object that includes a pointer to the snapshot of the content, along with information like author details, commit message, and parent commit(s) pointer(s).

![[Pasted image 20250525114250.png]]

**Branching:**

Git provides the git branch command to create, list, and delete branches.
As mentioned, branches in Git represent isolated lines of development.
When you create a local branch from a remote branch, tracking branches are created automatically by Git, which are local branches linked to remote branches.
You can list remote-tracking branches using the -r option with the git branch command and local and remote branches with the -a option.

In Git, local branches exist on your local machine and remote branches are stored in a remote location.
Comparing the differences between local and remote branches can be helpful. Here are the steps to do it:

- Update remote-tracking branches by running the command: `git fetch` in the terminal.
- List both local and remote branches using the command:  `git branch -a`. This will show the branches with an asterisk indicating the currently checked-out branch.
- To specifically list remote branches, use the following command: `git branch -r`

**Adding code**

- To **add** changes made to a file to the staging area, use the Git add command followed by the file name.
- This tells Git to include the changes made to the file in the next commit.

```
git add <filename>
```

- **Commit**: To save changes to the staging area.
- This creates a new commit in the Git history with the changes made.
- Use the commit message to add the description of the changes; very important to track progress.

```
git commit -m "commit message"
```

- **Push**: This will update the remote repository with the changes you made locally. It’s the final command to upload the changes from your local repository to the remote. Add the name of the branch you are working on.
- **Note**: you can pass “origin”. **“Origin” refers to the repository from which a project was initially cloned.**

```
git push <branch name>
```
