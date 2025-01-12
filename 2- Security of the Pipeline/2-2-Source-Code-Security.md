## Source Code Security

**Introduction**

In today’s fast-paced software development world, keeping your source code safe is essential to ensure your applications remain secure and reliable. A key tool for managing source code is version control, which helps teams work together, track changes, and keep a history of their code.

**Learning Outcomes**

- In this session, we’ll cover the basics of source code storage and version control, with a focus on Git, one of the most widely used version control systems. While there are other tools like Mercurial or VCS, Git is popular because it’s flexible, scalable, and packed with powerful features.
- We’ll start by understanding what version control is, why it’s important for DevSecOps (Development, Security, and Operations), and look at some examples of version control tools. Then, we’ll dive into Git, learning about its commands, workflows, and best practices for securing your code.
  
By the end of this session, you’ll have a strong understanding of source code security, how to use Git for version control, and how to manage your code safely and efficiently. Let’s get started!

## The Story of Git

**The Story of Git**

Git was created in 2005 by Linus Torvalds, the same person who created the Linux operating system. Its story began with some problems in the development of the Linux kernel, which is a big open-source project. In the early years of Linux (1991–2002), developers used patches and archived files to manage changes. Then, in 2002, the Linux project started using a system called BitKeeper to help manage its development.

But in 2005, the relationship between BitKeeper’s creator, Larry McVoy, and the Linux community became strained. This led to the Linux community losing access to BitKeeper, causing disruptions in their work. As a result, Linus Torvalds decided to create a new system that would fix these problems.

Linus designed Git to help developers work together more easily from different locations, and to make it simple to combine changes made by many contributors. He based Git on his experience with the Linux kernel and on lessons learned from other version control systems like BitKeeper, Subversion, and Monotone.

Git was released in April 2005, and since then, it has become one of the most widely used version control systems in the world, used by millions of developers.

**Why Git is Popular:**
- **Open-source:** Anyone can use and contribute to Git without paying for it.
- **Performance:** Git works faster than other systems because it focuses on the content of files rather than their names.
- **Security:** Git uses a method called hashing to protect code and keep track of changes.

Today, many companies and developers use Git as their main version control system.

## Version Control

**Version Control**

In software development, keeping source code safe is very important. Version control helps ensure that the code stays secure and is protected from unauthorized changes or mistakes. It is a tool that allows developers to track changes, work together, and keep a history of all updates made to the code.

**How does version control work?**

Version control uses a system called a repository. You can think of a repository as a database that stores all the changes made to a project. Developers also have a personal copy of the project files called a working copy (or checkout). In the working copy, developers can make changes without affecting others. Once they are happy with the changes, they can save (or "commit") those changes to the repository.

**Types of version control**

Version control systems can be centralized or distributed:

- **Centralized version control** has one central repository. When developers make changes and commit them, others can immediately see those changes.
  
- **Distributed version control** gives each developer their own repository. To share their changes, developers need to "push" their updates to a central repository, where others can then see and pull those changes.

**Popular version control systems**

The most well-known version control systems are Git, Mercurial, and Subversion. Distributed systems like Git and Mercurial are faster, more reliable, and have more advanced features than centralized systems like Subversion. However, they can be harder to learn.

In this guide, we will focus on **Git**, as it is one of the most widely used version control systems in the industry. We will go over the basics, important commands, and best practices for using Git to keep your code safe and collaborate efficiently with others.


## Cloud Based Version Control

**Introduction**

Cloud-based version control is a modern way to manage source code in software development. With this system, the code and its version history are stored in the cloud, allowing developers to work on code from anywhere. This makes it easier for distributed teams to collaborate. Cloud-based platforms offer easy access, real-time teamwork, and strong version history management. They also integrate well with other tools, providing a flexible and efficient solution for modern software development.

**GitHub**

GitHub is a cloud-based platform that lets developers store and manage their source code from anywhere. It is the oldest of the major platforms, created in 2007 by Chris Wanstrath, P.J. Hyett, Tom Preston-Werner, and Scott Chacon. GitHub was built using Ruby on Rails and became the first open-source code repository on the web, making it the dominant platform for developers. Today, developers use GitHub to host, manage, and review their code.

**CI/CD with GitHub Actions**

Continuous Integration (CI) and Continuous Deployment (CD) are practices that automate parts of the software development process. CI/CD automates tasks like testing, building, and deploying code, making the whole process faster and more reliable. In 2018, GitHub introduced **Actions**, a feature that allows developers to automate their workflows. Actions let you define tasks, such as building the code, creating a release, or deploying a web service. This is all part of the CI/CD pipeline, which makes development and deployment smoother and faster.

**GitLab**

We will use **GitLab** throughout this guide. Like GitHub, GitLab is an open-source platform that provides a complete set of tools for software development. GitLab was founded in 2014 by Ukrainian developer Dmitriy Zaporozhets and Dutch developer Sytse Sijbrandij. It was the first partially Ukrainian company to reach a $1 billion valuation in 2018, making it a "unicorn." From the beginning, GitLab was designed to combine collaboration tools and a code repository in one service. Unlike GitHub, GitLab includes built-in CI/CD tools, so developers don't need to use third-party services.

**CI/CD with GitLab**

GitLab’s CI/CD features let developers automate their entire software delivery process, from building and testing code to deploying and monitoring it. GitLab uses "runners" to execute jobs in the pipeline. Developers can create custom workflows, set up different stages, and decide whether tasks should run at the same time or one after the other. This makes it easier to manage the development and deployment process.

GitLab also offers features like a built-in container registry, continuous deployment to Kubernetes, and GitLab Pages for hosting websites. It also allows developers to create multiple stable branches, which helps with version control and release management.

**Summary**

GitLab’s all-in-one approach, with built-in CI/CD features and a focus on reliability, makes it a powerful solution for software development and deployment. Whether you're using GitHub or GitLab, these platforms provide efficient tools for managing code and automating workflows.

## Insufficient Credential Hygiene

**Introduction**

In CI/CD environments, managing credentials securely is very important to avoid security risks. Developers and systems use credentials like secrets and tokens to deploy and access resources or perform other privileged actions. However, managing these credentials can be tricky because they are used in many different ways and stored in various places. Problems like storing credentials insecurely in code repositories, using them wrongly in build and deployment processes, leaving them in container images, printing them in console logs, and not updating them regularly can all lead to security breaches.

**Risk Impact**

Credentials are highly valuable targets for attackers because they can give access to sensitive resources and allow malicious activities. In engineering environments, there are many ways for attackers to get hold of these credentials. Mistakes, lack of knowledge, and poor management of credentials can increase the chances of exposing sensitive information and compromising critical resources.

**Recommendations**

1. **Follow the principle of least privilege**: Only give credentials the minimum access they need, from code to deployment.
2. **Don't share credentials across multiple areas**: Keep credentials separate to make it easier to track usage and manage privileges.
3. **Use temporary credentials when possible**: Rotate static credentials regularly and periodically check for outdated credentials.
4. **Limit where credentials can be used**: Set conditions like specific IP addresses or identities to control when and where credentials are used.
5. **Monitor for secrets in code repositories**: Use IDE plugins, automatic scanning, and periodic checks to find secrets in code repositories.
6. **Prevent secrets from appearing in console logs**: Use built-in tools or third-party options to make sure secrets are not printed during builds.
7. **Remove secrets from artifacts**: Ensure that secrets are not left in container image layers or binaries.

By following these best practices, organizations can reduce the risks related to poor credential hygiene.

**Environment Variables and Best Practices**

Environment variables are a good way to handle credentials securely. They are often used in software development and deployment to store sensitive information like API keys and passwords. To manage environment variables securely, follow these best practices:

1. **Don't hardcode sensitive information**: Always use environment variables instead of hardcoding secrets in code.
2. **Regularly review and update environment variables**: Rotate the credentials stored in environment variables to keep them secure.
3. **Limit access to environment variables**: Only authorized people should have access to environment variables.
4. **Apply the principle of least privilege**: Set environment variables to give only the necessary level of access.
5. **Monitor and audit changes**: Track changes made to environment variables to detect any unauthorized changes.
6. **Review encryption mechanisms for secrets managers**: If you're using a secrets manager, check how it encrypts data and if it's suitable for your development environment.

**Note**: Using environment variables doesn't guarantee safety. It’s important to follow best practices to make sure they are properly secured.


## The Git, The Branch and The Ugly

**Introduction: Git**

In this section, we'll go over the basic Git commands you need to interact with projects on GitLab.

To get a project from GitLab, you use the `git clone` command. This command copies an existing repository to your local computer. The syntax looks like this:

```
git clone <repository_url>
```

This command copies the repository (repo) into a new folder on your computer. The original repository can be hosted either on your local machine or a remote server that Git can access. Once you clone a repo, you have a local version of it that includes all the files and their history. Your local copy is separate from the original repo.

You can think of a **branch** as a version of the project or an independent development line. Git allows you to create different branches for different versions of the project. A repository can have multiple branches.

**Cloning a Specific Branch**

Sometimes, you might want to clone a specific branch from a repository, not the default one. To do this, you can use the `-b` flag followed by the branch name:

```
git clone -b <branch_name> <repository_url>
```

This command clones only the specified branch, not the default one, from the remote repository.

**Understanding Git’s Branching Model**

Git stores data differently from other version control systems. Instead of keeping track of the changes made to files, Git stores snapshots of the entire project at different points in time. When you make a commit, Git creates a commit object that points to the snapshot and includes other details like the author's name, commit message, and the previous commit(s).

**Branching in Git**

Branches in Git allow you to work on different versions of the project independently. You can create, list, and delete branches using the `git branch` command.

When you create a branch locally from a remote branch, Git automatically creates a "tracking branch." This is a local branch that is linked to the remote one. You can see a list of remote branches by using the `-r` option with the `git branch` command. To see both local and remote branches, use the `-a` option.

Here’s how you can manage branches:

1. **To update remote branches**, use the command:
   ```
   git fetch
   ```

2. **To list all branches (local and remote)**, use:
   ```
   git branch -a
   ```

3. **To list only remote branches**, use:
   ```
   git branch -r
   ```

**Adding Code**

After making changes to files, you need to add them to Git's "staging area" before committing. Use the `git add` command:

```
git add <filename>
```

This tells Git to include the changes in the next commit.

**Committing Changes**

Once your changes are staged, you need to commit them to save them in the Git history. Use the `git commit` command with a message that describes the changes:

```
git commit -m "Your commit message here"
```

**Pushing Changes**

Once you've committed your changes locally, you need to upload them to the remote repository. Use the `git push` command, followed by the branch name you're working on. For example:

```
git push <branch_name>
```

The `git push` command sends your changes from your local machine to the remote repository. You can use "origin" to refer to the repository where you originally cloned the project from.

By using these basic Git commands, you can manage and update projects on GitLab effectively.

## Secret Management

**Introduction**  
Environment variables are important for securing sensitive information like passwords, keys, APIs, and tokens used in apps and services. These credentials help protect different parts of your IT system, such as accounts and data. However, to keep these environment variables safe, you need to have a good secret management process. Without proper management, security risks can appear, and it will be hard to track them. In this guide, we will learn how to manage secrets securely using GitLab.

**Managing Secrets in GitLab**  
After adding environment variables to your GitLab project, you can use GitLab’s secret management features to keep these variables safe. Here’s how to do it:

1. Open your GitLab project and go to the "Settings" page.
2. Click the "CI/CD" tab, then click on "Variables."
3. Click "Add variable" and enter the name and value of your environment variable. Be sure to check the "Protected" box.
4. Click "Add variable" to save it.
5. In your `nstr.go` file, you can now use the command `os.Getenv("var_name")` to get the value of the environment variable.

For example, if you add variables called `GIT_USERNAME` and `GIT_PASSWORD`, you can use them like this in `nstr.go`:

```go
func init() {
    apiURL = "https://samplesite.com"
    username = os.Getenv("GIT_USERNAME")
    password = os.Getenv("GIT_PASSWORD")
}
```

Now, your credentials are safely stored in environment variables, and you can access them when needed.

**Bonus**  
Have you noticed the `.gitlab-ci.yml` file? But there are no pipelines, workflows, or "status checks"? To learn more about what that file is used for, check out this link: [GitLab CI YAML](https://docs.gitlab.com/ee/ci/yaml/gitlab_ci_yaml.html). Although this isn't covered here, be on the lookout for the next topic: "Build System Security."