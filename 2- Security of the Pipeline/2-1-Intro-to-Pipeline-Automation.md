## Intro to Pipeline Automation

**Introduction**

Humans are always trying to find easier and more efficient ways to do things. When we started programming and creating software, we also looked for ways to automate some tasks. Today, automation is a big part of the Software Development Life Cycle (SDLC) and DevOps processes. Automation helps speed up development and deployment, which is great for production. However, it also brings new security risks. Before automation, an attacker would need to compromise the person’s credentials or workstation who performed a task. But with automation, attackers can target the pipeline itself.

**Learning Objectives**

In this part, you'll learn about these topics:
- What the DevOps pipeline is
- The tools and automation used in DevOps
- Basic security principles for the DevOps pipeline

This is just an introduction. You'll learn more about these topics in detail in the other parts of this module.

## DevOps Pipelines Explained

Before we dive into automation security, let's first understand what a pipeline is and where automation fits in. The diagram below shows what a typical pipeline looks like and the software that might be used at each stage.

For each part of the pipeline, we will cover:
- What it is
- The common tools used
- An introduction to its security
- A case study showing what can happen if security fails

We will go into more detail on each of these topics in the upcoming parts of this module.

## Source Code and Version Control

Let’s start with **source code** and **version control**. This is where our pipeline begins. We need a place to store our code, and we also need to keep track of different versions of it since we’re constantly improving and adding new features.

### Source Code Storage
When deciding where to store our code, we need to think about a few things:
- How can we control who has access to the code?
- How can we track changes to the code?
- Can we link the storage system to our development tools?
- Can we store and use multiple versions of the code?
- Should we host the code ourselves, or can we use an external provider?

The answers to these questions will help us pick the right storage solution for our project.

### Version Control
We need version control for two main reasons:
1. We are constantly adding new features and making updates, so we need to keep track of all these changes.
2. A team of developers works on the code, so version control helps us manage changes from multiple people.

Version control allows us to keep track of different versions of the code. This includes the specific version each developer is working on, as well as major and minor versions of the application.

### Common Tools
The two most common systems for source code storage and version control are **Git** and **SubVersion (SVN)**:
- **Git** is a distributed system, meaning each contributor has their own copy of the code.
- **SVN** is a centralized system, where the code is controlled from a central place.

**GitHub** is the most popular platform for hosting Git repositories. You can create a GitHub account and use it to manage your code. Alternatively, you could host your own Git server using software like **GitLab**. For SVN, **TortoiseSVN** and **Apache SVN** are widely used.

It’s important to note that platforms like GitLab offer more features than just version control and storage. These tools are often used for managing the entire development pipeline.

### Security Considerations
Our source code is very important, so we need to protect it. This means controlling who can access it and making sure that changes are tracked properly. If something goes wrong, we should be able to go back to an earlier version of the code.

However, we also need to be careful about what we store in the code. While developers need access to the source code, we should avoid storing sensitive information (like database credentials) in it. Even if we remove sensitive data in a newer version of the code, it could still be visible in earlier versions.

### Case Study: Git Never Forgets
Version control can cause problems if we’re not careful. Git has a saying: **"Git never forgets"**. When we commit code to a Git repository, Git creates a new version of the code based on the changes. Anyone with access to the repo can look at past commits to see what changes were made.

The problem occurs when a developer accidentally commits sensitive information, like credentials or database connection strings, to the repository. If they realize the mistake and delete the sensitive data, Git will still keep a record of both versions: the one with the secret and the one without it. If an attacker gains access to the repo, they can use a tool like **GittyLeaks** to scan through past commits and find the sensitive information, even if it has been removed in the latest version.

This shows how version control can cause problems if sensitive data is not handled carefully.

## Dependency Management

Let's talk about **dependencies**. When we develop software, it might seem like we’re writing a lot of code, but in reality, we’re only writing a small part of it. Most of the code we use has already been written for us in the form of **libraries** and **software development kits (SDKs)**. For example, even simple things like a **String** in an application come with an entire library behind them! Managing these dependencies is an important part of the development process.

### External vs Internal Dependencies
There are two types of dependencies: **external** and **internal**.

- **External dependencies** are libraries and SDKs that are publicly available. These are hosted on dependency managers like:
  - **PyPi** for Python
  - **NuGet** for .NET
  - **Gems** for Ruby libraries

- **Internal dependencies** are libraries or SDKs that a company develops and maintains. For example, a company might create an authentication library used in all its applications.

Both types of dependencies come with different security concerns:

| **Internal Dependencies** | **External Dependencies** |
|---------------------------|---------------------------|
| Libraries can become outdated if they no longer receive updates or the original developer leaves the company. | We don’t have full control over external libraries, so we need to check they are secure. |
| The company is responsible for securing the internal package manager. | If an external package manager or content distribution network (CDN) is hacked, it could lead to a supply chain attack. |
| A problem in an internal library can affect multiple applications if it's used in all of them. | External libraries may have unknown vulnerabilities, which attackers could exploit. This can affect many organizations at once. |


### Common Tools
To manage dependencies, we use **dependency managers** (also called **package managers**). Some tools for managing external dependencies are:
- **PyPi** for Python
- **NuGet** for .NET
- **Gems** for Ruby

For managing internal dependencies, tools like **JFrog Artifactory** or **Azure Artifacts** are used.

### Security Considerations
The main security issue with dependencies is that they are often outside our control. With so many dependencies being used, it’s hard to track them all. If a dependency has a vulnerability, it can create security problems in our application.

### Case Study: Log4Shell
A great example of a dependency vulnerability is **Log4Shell**, which was discovered in the **Log4j** library in 2021. Log4j is a Java-based logging tool used by many software applications. The vulnerability allowed an attacker to execute remote code on any system using this tool.

What made this so dangerous was that **Log4j** was used everywhere. As this XKCD cartoon shows, it was almost impossible to count all the products that were vulnerable because they used this library. The list of affected products was so long that it had to be split alphabetically!

This example shows the huge impact a vulnerability in a single dependency can have.

## Automated Testing

Let’s take a closer look at **automated testing**. In the past, testing was a slow, manual process. Testers had to run each test case by hand and hope that all parts of the application were covered. If something went wrong, it could be hard to catch. But today, in modern development pipelines, **automated testing** handles a large part of this process, making it faster and more efficient.

### Unit Testing
The first type of automated testing most developers are familiar with is **unit testing**. A unit test checks small parts of the application to make sure each one works correctly. These tests focus on individual functions or features of the application.

In modern pipelines, unit tests are often used as **quality gates**. This means the pipeline will stop if any unit test fails, preventing problems from moving forward. However, unit tests usually focus on functionality and do not typically check for security issues.

### Integration Testing
Next is **integration testing**. While unit tests check small parts, integration tests check how different parts of the application work together. Like unit tests, integration tests can be added to the CI/CD pipeline, and a special type called **regression testing** makes sure new features don’t break old ones.

However, like unit tests, integration tests usually don’t focus on security.

### Security Testing
So, if unit and integration tests aren't for security, what types of tests are? There are two main types of **automated security testing**:

#### SAST (Static Application Security Testing)
**SAST** tools check the source code of an application to find vulnerabilities before it’s even run. These tools can scan code while it’s being written, helping developers spot potential problems early. They can also be added to the CI/CD pipeline as **security gates**, stopping the pipeline if vulnerabilities are found.

#### DAST (Dynamic Application Security Testing)
**DAST** tools work by running the application and testing it in action. They find vulnerabilities that can only be detected when the app is running, such as **Cross Site Scripting (XSS)**. DAST tools create **sources** (places where input is entered) and **sinks** (places where the input is processed), sending test data to see if vulnerabilities like XSS are present. DAST tools can also be integrated into the CI/CD pipeline as security gates.

### Penetration Testing
Even though SAST and DAST are very useful, they can't fully replace **manual testing** like **penetration testing**. Automated tools can miss some types of vulnerabilities, especially those that require understanding the context of how the application works, like business logic flaws or access control issues. Penetration tests are more effective for finding these kinds of problems. While automated tools might eventually find them, manual testing is often faster and cheaper in these cases.

### Common Tools
Several tools can help with automated testing:
- GitHub and GitLab both have built-in SAST tools.
- Popular third-party tools for SAST and DAST include **Snyk** and **SonarQube**.

### Case Study: "She Can’t Take Any More, Captain! She's Gonna Blow!"
One issue with automated tools like SAST and DAST is that they can slow things down if not properly set up. Here are some important things to consider:
- **Performance cost**: Scanning large amounts of code can be slow, especially when done frequently.
- **Integration points**: How the tools integrate into your pipeline is crucial for smooth operation.
- **Calibrating results**: The tools need to be properly tuned to avoid false positives or missing real issues.
- **Quality and security gates**: Deciding when and how to use security checks is important for maintaining speed.

If these factors are ignored, introducing security testing tools can cause performance problems. For example, running a security scan right before a big release can slow down the pipeline, preventing developers from pushing their changes. Also, as more teams work with **agile development**, repositories may get hundreds of commits each day. Adding security scans for each merge request can greatly affect performance and slow down development.

When adding automated testing tools, it's important to carefully plan out the **Proof-of-Concept (PoC)** phase. This helps ensure the tools are effective without disrupting the development process. The goal is to find a balance between running the tests effectively and keeping the pipeline fast and efficient.

## Continuous Integration and Delivery

In modern development pipelines, software isn’t manually moved between environments. Instead, an **automated process** is used to handle tasks like compiling, building, integrating, and deploying new software features. This process is known as **CI/CD**.

### What is CI/CD?
The term **CI/CD** has changed over time. Initially, it focused mainly on using **Agile** methods for development while delivery still followed the traditional **waterfall** model, where the product was only deployed at the end of the process. Back then, CI/CD meant **Continuous Integration** and **Continuous Development**.

Soon, it became clear that even **deployment** could follow an Agile approach. So, the term changed to **Continuous Integration** and **Continuous Deployment**—now, deployment was part of the integration process. Finally, the term evolved again to **Continuous Integration** and **Continuous Delivery**, as teams began focusing not just on deployment but on the whole delivery process, including monitoring the software after it’s released.

Today, **CI/CD** refers to the entire process of building, testing, deploying, and delivering software features, and you may hear these terms used interchangeably.

### How CI/CD Works
Since software is constantly being updated with new features, it’s important to make sure these features work with the current version of the application. Instead of waiting until the end of the development cycle to integrate everything, we can use CI/CD to **continuously integrate** new features and test them as they’re developed.

A **CI/CD pipeline** is a series of automated steps that manage this process. It usually includes the following stages:

1. **Starting Trigger** – This is the action that starts the pipeline. For example, it could be a developer pushing code to a specific branch.
   
2. **Building Actions** – These actions compile the code and build the project with the new feature.
   
3. **Testing Actions** – These actions test the project to make sure the new feature doesn’t break anything that’s already working.
   
4. **Deployment Actions** – If the tests pass, the build moves to the next environment, like a **Testing Environment**, where it can be further reviewed.
   
5. **Delivery Actions** – This focuses on the entire delivery process. It includes things like monitoring the deployed solution to ensure everything works after release.

### The Infrastructure Behind CI/CD
For CI/CD pipelines to run, they need **build infrastructure**. This is typically made up of **build orchestrators** and **build agents**. The orchestrator coordinates the agents to carry out the actions in the pipeline.

CI/CD pipelines are where a lot of **automation** happens, and because of that, they are also the biggest place where **security risks** can occur. Misconfigurations in these pipelines can lead to serious issues.

### Common Tools
Many tools are available to help with CI/CD processes:
- **GitHub** and **GitLab** are popular platforms that offer CI/CD capabilities. GitHub provides **build agents**, while GitLab uses a **GitLab runner** that can be installed on a host to turn it into a build agent.
- For more complex builds, **Jenkins** is often used as a build orchestrator.

We’ll explore these tools and their common misconfigurations in later lessons.

### Case Study: A Tangle Between Dev and Prod
A common mistake in CI/CD pipelines is using the same build agent for both **Development (DEV)** and **Production (PROD)** builds. This can cause serious problems.

- Developers typically have access to triggers for **DEV builds** but not for **PROD builds**.
- If an attacker compromises a developer’s account, they might be able to make a malicious change in the DEV build.
- The danger comes from the fact that the same **build agent** is used for both DEV and PROD environments. If the agent is compromised during a DEV build, the attacker could wait for the next **PROD build** to trigger. When this happens, the attacker could inject malicious code into the production version of the application.

This highlights the importance of **separating** DEV and PROD environments and using different build agents for each to prevent attackers from affecting the production system.

## Environments

Let's take a closer look at the different **environments** in a typical pipeline. Each environment serves a specific purpose, and they all have different levels of **stability** and **security**. Here are the most common ones:

### Common Environments




| Environment | Description | Stability | Security Posture | May It Contain Customer Data? |
|-------------|-------------|-----------|------------------|-------------------------------|
| **DEV (Development)** | This is where developers build and test new features. It’s the most unstable environment since developers are constantly pushing new code. The security here is the weakest because access controls are usually relaxed, and developers often have direct access to the infrastructure. If compromised, the impact is usually low, but the risk is higher. | Unstable | Weakest | No |
| **UAT (User Acceptance Testing)** | UAT is used to test the app or specific features before they go live. This environment is more stable than DEV but still less stable than others. Security controls are in place but not as strict as in later environments. UAT should include security tests, but it’s not as hardened as PreProd or PROD. | Semi-Stable | Second Weakest | No |
| **PreProd (Pre-Production)** | PreProd mimics the production environment but without real customer data. It’s kept stable for final testing before new features are deployed. Its security should mirror that of PROD, but sometimes it may not. | Stable | Second Strongest | No |
| **PROD (Production)** | PROD is the live environment that users interact with. It must be stable and secure because it holds customer data. Updates should only happen with proper change management. The security here is the strongest because it protects both the system and user data from threats. | Stable | Strongest | Yes |
| **DR/HA (Disaster Recovery / High Availability)** | These environments are used for recovery if something goes wrong in PROD. If downtime is minimal, it’s called High Availability (HA); if some downtime is allowed, it’s called Disaster Recovery (DR). These environments must match PROD in stability and security to ensure a quick recovery. | Stable | Strongest | Yes |

### Other Notable Environments

- **Green and Blue Environments:** These environments are part of a **Blue/Green deployment** strategy. In this setup, two production environments (Blue and Green) exist. One (Blue) runs the current version of the application, and the other (Green) runs the new version. Traffic can be switched between them, so if issues arise in the Green environment, traffic can be routed back to Blue, allowing for faster rollbacks.

- **Canary Environments:** Similar to Green and Blue, **Canary environments** gradually move users to a new version of the application. For example, 10% of users might be moved to the new version at first. If everything works well, another 10% is moved, and so on, until all users are switched. This helps reduce risks during deployment and minimizes downtime.

### Tools for Managing Environments

With modern technology, managing environments has become more flexible. Tools like **Vagrant** and **Terraform** allow the creation of virtual environments. In addition, **containers** (using Docker) and **pods** (using Kubernetes) are widely used to run applications in isolated environments. These technologies can also be used with **Infrastructure as Code (IaC)** to automate the setup and management of environments.

### Security Considerations

As environments get closer to **PROD**, security becomes more critical. The underlying infrastructure of the application, including the servers and containers, forms part of the **attack surface**. If an attacker compromises the infrastructure, they could take control of the application as well. Therefore, it’s important to **harden** the infrastructure with measures like:

- **Removing unnecessary services**
- **Updating software regularly**
- **Using firewalls** to block unused ports

### Case Study: Developer Bypasses in PROD

One common issue between different environments is that sometimes, features meant for DEV environments accidentally make their way into PROD. In DEV, developers often use **bypass mechanisms** to speed up testing. For example, they might use a fixed **OTP code** to skip Multi-Factor Authentication (MFA) prompts or disable CAPTCHA checks to test features quickly. 

However, if these bypasses aren’t properly removed before moving to the next environment, they could end up in **PROD**. For instance, the fixed OTP code used in DEV could allow attackers to bypass MFA in PROD and gain unauthorized access to user accounts.

To prevent this, **environment segregation** is critical. Just like quality gates ensure only working code moves through the pipeline, **security gates** should be set up to make sure no insecure code or bypasses make it into higher environments like UAT, PreProd, or PROD.

## Conclusion
Automation in the pipeline has greatly improved how quickly developers can create and deploy updates to applications. However, it also opens up new security risks. Since the pipeline automates many tasks, attackers might try to target it instead of directly attacking the application. This means that the pipeline itself becomes a potential entry point for attacks. To protect against this, it’s important to secure the automation process, ensuring that the pipeline doesn’t become a weak spot that could lead to the application being compromised.
