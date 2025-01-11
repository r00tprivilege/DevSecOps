##Introduction:

If you’re aiming to enter the world of DevOps/DevSecOps, you’ve likely come across the term infrastructure as code (IaC). IaC is a core component of DevSecOps, which is why it’s extensively discussed in various articles, blog posts, and papers. However, these resources often skim over many concepts and tools, which can leave newcomers confused about key IaC terms and uncertain about which tools to use for different purposes. This section will provide a gradual introduction to infrastructure as code, guiding you through the essential terms and providing a foundational understanding of IaC. You can build on this knowledge with the subsequent sections in this module.

### Learning Prerequisites
This section is a continuation of the DevSecOps path, so it’s crucial to have completed all previous DevSecOps modules. Task 6 covers virtualization and highlights the "Virtualization and Containers" and "Intro to Containerization" sections for additional context.

### Learning Objectives
- Understand the necessity of IaC
- Grasp the concept of IaC, the tools used, and their characteristics
- Understand the IaC lifecycle, including the distinction between provisioning and configuring, and identify tools for both
- Recognize the importance of virtualization to IaC
- Differentiate between on-premise IaC and cloud-based IaC, and understand the benefits of each

DevOps:

Since its introduction, Developer Operations (DevOps) has had a major impact on modern Software Development, Deployment, and Operations. But where did this term originate?

### The Story of DevOps
In a distant past, in a galaxy far, far away, there were waterfalls.

#### Waterfall Model
The Waterfall Model was the approach to project management back in the 1970s. This hierarchical structure assigned specific responsibilities to each team member. System administrators worked tirelessly to keep everything running smoothly. Developers built and added as many features as possible. Quality Assurance (QA) engineers tested the system's functionality to ensure it worked as expected.

If servers had issues or something needed deployment, system admins would handle it. Developers tackled code problems, and QA teams dealt with testing and feedback. But what if a bug emerged? Who would fix it? These situations often led to blame games, creating friction and backlogs. As customer expectations grew, so did the number of features and new releases. Tasks and responsibilities piled up, leading to an unmanageable mess. Bugs and security flaws accumulated, and unresolved issues piled up. The system's lack of scalability created excessive pressure, distrust, communication gaps, and team friction.

This outdated problem-solving strategy and system were the root causes of inflexibility and poor communication across teams.

#### Agile Model
In response to the challenges with the Waterfall Model, businesses began developing more flexible and adaptable approaches. In the early 2000s, the Agile Methodology was born, along with the Agile Manifesto, which emphasized four values:

- Individuals and interactions over processes and tools
- Working software over comprehensive documentation
- Customer collaboration over contract negotiation
- Responding to change over following a plan

Companies now valued team collaboration, self-organizing teams, and a focus on clients, with ample room for change and flexibility. However, something was still missing.

### DevOps: A New Hope
In 2008, a conversation between Andrew Clay and Patrick Debois led to something revolutionary. Discussing Agile's drawbacks, they gave birth to DevOps. After the "DevOpsDays" event in Belgium in 2009, DevOps became a buzzword, and its popularity soared.

DevOps differs from previous methodologies by driving "cultural change" to increase efficiency. It unites all project teams through integration and automation. This approach fosters cross-integration among QA, sysadmins, and developers.

For instance, developers can now participate in deployment, sysadmins can write scripts, and QA can address flaws instead of just testing functionality. Automation and system integration provide engineers with constant visibility and improve their interaction. We'll delve into how DevOps achieves this through pipelines, automation, Continuous Integration, and Continuous Delivery (CI/CD) later.

### Why is DevOps Important?
DevOps promotes building trust and better collaboration between developers and other teams (sysadmins, QA, etc.). This alignment of technological projects with business requirements enhances the business's impact and value. Changes are typically small, reversible, and visible to all teams, ensuring better communication and contribution, leading to increased efficiency.

### In Summary
Thanks to DevOps, today's development infrastructure is fully automated and self-service:

- Developers can provision resources to public clouds without relying on IT, avoiding delays.
- CI/CD processes automatically set up testing, staging, and production environments in the cloud or on-premises. They can be decommissioned, scaled, or re-configured as needed.
- Infrastructure-as-Code (IaC) deploys environments declaratively, using tools like Terraform and Vagrant.
- Organizations can dynamically provision containerized workloads using automated, adaptive processes.

The declarative approach specifies the end state of the infrastructure, automating configuration choices throughout the workflow. The software builds and releases it without human interaction. The imperative/procedural approach configures systems through a series of steps, with a "gate" to apply changes, such as a "deploy changes" button after automated checks and configurations pass.

In such workflows, even minor issues can create chaos. As new releases increase, unresolved issues and scheduled features can lead to disaster.


## The Infinite Loop

We've explored various software development styles over the years and how they've significantly influenced the inception of DevOps. In this task, you'll be introduced to key concepts and tools, and how they all work together.

### How Does DevOps Work?
DevOps is visualized as an infinite loop, encompassing all its phases:

Following this loop, let's delve into some DevOps tools and processes we'll explore as we follow the DevSecOps pathway and see how they benefit an organization:

1. **CI/CD** – Previously, we mentioned CI/CD (Continuous Integration and Continuous Deployment). CI/CD involves the frequent merging of code and automated testing to check new code as it's pushed and merged. This dynamic and systematic approach to deployment with minor code changes helps detect bugs early and significantly reduces the effort needed to maintain modular code. It also enables reliable version/code rollbacks.

2. **Infrastructure as Code (IaC)** – IaC allows for managing and provisioning infrastructure through code and automation. By reusing code to deploy infrastructure (e.g., cloud instances), we achieve consistent resource creation and management. Standard IaC tools include Terraform and Vagrant. We'll use these tools further along the pathway to experiment with IaC security.

3. **Configuration Management** – This involves continually managing the state of infrastructure and applying changes efficiently, making it more maintainable. This approach saves a lot of time and provides greater visibility into how the infrastructure is configured. IaC can also be used for configuration management.

4. **Orchestration** – Orchestration automates workflows, helping to achieve stability. For example, automating resource planning allows for quick responses to problems (e.g., health check failures) through monitoring.

5. **Monitoring** – Monitoring focuses on collecting data about the performance and stability of services and infrastructure. This enables faster recovery, enhances cross-team visibility, provides more data for root-cause analysis, and generates automated responses.

6. **Microservices** – This architecture breaks applications into many small services, offering benefits such as flexibility in scaling, reduced complexity, and more options for technology choices across microservices. We'll delve deeper into these in the DevSecOps pathway.


## Shifting Left 

### Introduction
DevOps has greatly increased visibility and flexibility in development, making it easier to integrate security from the beginning. You may have heard of the concept "Shifting Left." This means that DevOps teams emphasize embedding security from the earliest stages of the development lifecycle, fostering a more collaborative culture between development and security. 

By introducing security early on, risks are significantly reduced. In the past, security flaws and bugs were often discovered late in the development process, even in production, leading to stress, rollbacks, and economic losses. Now, with the integration of code analysis tools and automated tests early in the process, these security flaws can be identified during the early development stages.

### Shifting Left
Historically, security testing was conducted at the end of the development cycle. As the industry evolved, security teams began performing various analyses and security testing in the final stages of the lifecycle. Depending on the results, the application would either be approved for production deployment or sent back to developers for remediation, resulting in long delays and team friction.

Implementing security measures throughout all stages of the development lifecycle (shifting left) ensures that software is designed with security best practices from the start. Early detection of security flaws lowers remediation costs and eliminates the need for rolling back changes, reducing costs, building trust, and improving the security and quality of the product.

### Why Shift Left?
Before agile methodologies, developers requested infrastructure from IT and received servers weeks or months later. Nowadays, this infrastructure provisioning in the cloud is automated, improving development productivity and speed. However, this increased velocity can also raise security concerns and allow flaws to go unnoticed.

The Shift-Left approach ensures that these flaws are caught early by integrating processes from the start. In today's fast-paced environment, post-development security reviews and analysis of cloud infrastructure configurations can create bottlenecks. Even when problems are discovered, there often isn't enough time to address them before the next version or feature is released. To keep up with customer demands and ensure security isn't left behind, adapting security testing to fit the development lifecycle is crucial.

### DevSecOps: Security from the Start
This development approach, referred to as DevSecOps, integrates security early in the development cycle, significantly minimizing risks. By incorporating code analysis tools and automated tests earlier in the process, security loopholes are better identified and eliminated. As a result, when the software reaches the deployment stage, it functions smoothly as expected. Security is not an add-on; it's a must-have design feature.

Integrating security in DevOps not only enhances the impact of DevOps but also eliminates many bottlenecks that could otherwise arise. With the rise in cyber threats and stricter regulations, adding security to DevOps is not a choice but an obligation.


## DevSecOps: Security Strikes Back

DevSecOps is an approach that leverages automation and platform design to make security a shared responsibility. It promotes a culture where security is a daily operation integrated into development processes.

### What is the value?
DevSecOps helps reduce vulnerabilities, maximizes test coverage, and enhances the automation of security frameworks. This approach significantly lowers risks, helps organizations prevent brand reputation damage and economic losses due to security incidents, and simplifies auditing and monitoring.

### How to implement this efficiently?
Culture is key. Open communication and trust are essential. DevSecOps requires collective effort to bridge security knowledge gaps between teams. To ensure everyone is accountable for security, they need the tools and knowledge to drive autonomy effectively and confidently.

### DevSecOps Challenges
**Security Silos:** 
Many security teams are often excluded from DevOps processes, treating security as a separate entity managed by specialists. This creates a silo effect, preventing engineers from understanding or applying security measures from the start. Security should be a supportive function that helps other teams scale and build secure solutions without becoming a bottleneck. Responsibilities should be shared across all team members, rather than relying on specialized security engineers.

**Lack of Visibility & Prioritization:**
Creating a culture where security is treated as a regular aspect of application development is crucial. This allows developers to focus on development with confidence in security, avoiding the blame game and fostering trust between teams. Security should promote autonomy by establishing processes that instill security within the teams.

**Stringent Processes:**
New experiments or software should not be bogged down by complicated security compliance processes. Procedures should be flexible, treating lower-risk tasks differently from higher-risk ones. Developers need environments to test new software without common security limitations, such as "SandBox" environments—temporarily isolated environments with no connection to internal networks and no customer data.


### DevSecOps Culture

#### Promote Autonomy of Teams
In large organizations or fast-growing startups, maintaining security can be challenging. Promoting team autonomy is essential. Automate processes that integrate seamlessly with the development pipeline until security tests become as routine as unit testing or smoke tests.

Lead by example and promote education by creating playbooks or runbooks. These resources help spot and fix flaws, understand risks, and build confidence in engineers to make secure decisions independently. Since there won't always be a balanced ratio of developers, platform, and infrastructure engineers to security engineers, it's crucial to understand that security engineers can't be part of every conversation. Instead, security should act as a supporting function that builds trust and promotes knowledge sharing among teams.

#### Visibility and Transparency
Introduce tools with supporting processes that provide visibility and promote transparency across teams. To build team autonomy, they need visibility into the security state of their services. For example, a dashboard that visualizes the number of security flaws by the criticality of the service helps prioritize tasks, ensuring they don't get lost in the backlog.

Transparency means making tools and practices accessible to teams. For instance, if a code check fails with a message about a possible code injection flaw, the developer should access the tool that flagged it. These analysis tools often specify the affected code line and provide definitions and remediation steps. Creating developer roles with access to this information promotes education and autonomy, extending transparency traditionally limited to security teams.

#### Account for Flexibility with Understanding and Empathy
Integrating security into DevOps processes with visibility and transparency is challenging and requires understanding and empathy. The definition of risk varies between security teams and other teams, affecting priorities, work processes, and decisions.

There's no one-size-fits-all tool or process. Understanding how developers and engineers work, their perception of risk, and their priorities helps build processes that find common ground and are more likely to succeed. This understanding fosters empathy for how other teams work and builds flexible processes, accounting for varying situations, deadlines, and bandwidth.

As a DevSecOps engineer, understanding how a team manages a service with a security scanner added to its development process makes it easier to gain their buy-in and demonstrate value. For example, if a platform team owns a critical internal service, a risk might be a bug that disrupts the service rather than a potential injection behind a proxy. Tuning scanners or adding a triaging process that addresses their concerns builds trust and prevents security processes from being questioned.

