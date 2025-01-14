# SDLC

**Introduction**  
This section explains the Software Development Lifecycle (SDLC) framework, its stages, and its key parts.
![image](https://github.com/user-attachments/assets/6d6a2558-a734-4b4b-8ec1-a42d5be4b3c5)

**Learning Objectives**  
By the end of this section, you will:  
- Understand what the SDLC framework is and why it’s important  
- Learn about the different phases of the SDLC  
- Discover how to add security to the SDLC  
- Understand the security-related phases and processes of the SDLC

## SDLC
![image](https://github.com/user-attachments/assets/6e788d8d-bb89-4e34-89c4-d8df450ffe23)

**What is the Software Development Lifecycle (SDLC)?**

The Software Development Lifecycle (SDLC) is a set of steps or practices used to build software applications in a structured way. It helps standardize the process by defining tasks that need to be completed at each stage of development. The goal of SDLC is to improve software quality, ensure the development process meets customer needs, and stay on schedule and within budget. For example, as customer demands grow, the need for more computing power also increases, which can drive up costs and reliance on developers. SDLC helps manage this by measuring and analyzing each stage, improving efficiency, and reducing costs.

**How does SDLC work?**

SDLC breaks down the software development process into different phases. Each phase has specific tasks that need to be done, and this helps make the process more efficient and organized. By standardizing these tasks, it becomes easier to track progress, measure success, and ensure that projects stay on track. The goal is to create repeatable processes that lead to predictable outcomes, so future projects can benefit from past experiences.

There are typically 6 to 8 phases in the SDLC. These phases are:

1. **Planning**: This phase involves organizing the project. It includes things like allocating resources, scheduling tasks, and estimating costs.

2. **Requirements Definition**: This is part of planning, where you figure out what the software should do. For example, a social media app needs to have features that allow users to connect with friends.

3. **Design & Prototyping**: This phase is about deciding how the software will work. It includes choosing the programming language, designing the architecture, and figuring out how different parts of the software will communicate with each other.

4. **Software Development**: This is the phase where the actual coding happens. Developers write the software and create documentation.

5. **Testing**: In this phase, the software is tested to make sure it works properly. This includes checking that all parts of the application work together smoothly and there are no performance issues, like slow loading times.

6. **Deployment**: Once the software is ready, it’s made available for users to use.

7. **Operations & Maintenance**: After the software is launched, engineers work to fix any bugs or issues reported by users. They may also add new features in future updates.

## SDLC Phases
![image](https://github.com/user-attachments/assets/35ee28c7-4405-4a19-b797-6418341ee786)

**Introduction**  
The first phases of the Software Development Lifecycle (SDLC) focus on breaking down the project or application before actual development begins.

**1. Planning**  
The Planning Phase, also called the Feasibility Stage, helps define the purpose and scope of the application. This phase outlines how the software will be developed, ensuring that the project stays focused on its main goals and limits. In this stage, the problem the system will solve is identified, and its scope is defined. It also helps identify the resources needed and potential risks, allowing problems to be caught early before affecting the process. Planning is especially important if the project needs to be completed by a specific deadline.

**2. Requirements Definition**  
In the Requirements Definition stage, the details of what the system needs to do are gathered. This includes:  
- Listing all the requirements for the system  
- Evaluating prototypes and considering alternatives  
- Researching and analyzing the needs of the end-users

This phase helps define the resources and features needed for the application. For example, a social media app might need features to connect with friends, while an inventory app might need a search function. Developers often create a document called a Software Requirement Specification (SRS) to capture all these details.

**3. Design and Prototyping**  
In this phase, developers create detailed plans for the software, including:  
- User interfaces  
- Communication between systems  
- Network requirements  
- Database needs

The design from the Requirements Definition phase is turned into a logical structure using programming languages. Plans for system operation, user training, and ongoing maintenance are also created. For example, the software’s architecture defines how the code is written and what practices are followed. A document called an Architecture Design Review (ARD) is often created during this phase to ensure all teams, like developers working on different parts of the system, are aligned.

**4. Software Development**  
The development phase involves writing the code for the application based on the earlier design. Developers follow instructions, use compilers, and debugging tools to ensure the software is built correctly. Security guidelines and best practices are also followed to ensure the software is secure. The application is also documented, including playbooks and guides for developers.

**The Final Phases: Testing, Deployment, and Maintenance**

The final phases of the Software Development Lifecycle (SDLC) focus on testing the application before it is released and ensuring it runs smoothly after it’s deployed.

### **5. Testing**  
Before making the software available to users, it's important to test it thoroughly. During the testing phase, developers check the software using automated tools, such as code scanners, to make sure it meets the quality standards set earlier in the planning and requirement stages. Testing is a key part of making the software more secure. It goes through its own "Software Testing Lifecycle," which may involve a dedicated testing team, like Quality Assurance (QA) Engineers. The main tasks in testing are designing test cases, setting up the test environment, and running the tests.

- **Test Case Design and Development**  
  After creating a test plan, the testing team writes detailed test cases. These tests are designed to make sure the software works as expected, especially the most important features. Test cases must be clear, simple, and repeatable, so they can be used again in the future as the software evolves. Once written, these test cases are reviewed by the team to ensure they are correct and complete.

- **Test Environment Setup**  
  The test environment is where the software will be tested. This includes setting up the necessary hardware, software, network, and configurations. For example, if most users will be using the app on Android phones with a certain browser, the test environment needs to simulate that setup.

- **Test Execution**  
  During this stage, testers run all the test cases. This includes both functional tests (to check if everything works as it should) and non-functional tests (like checking performance). Testers identify any bugs, record how the software performs, and report any issues. Developers then fix these issues, and the software is retested, which is called regression testing. Automated testing tools are often used to speed up this process.

### **6. Deployment**  
Once the software passes testing, it is ready for deployment. In this phase, the software’s design is finalized, and different parts of the application are integrated. After this, the software is released to end-users. Many companies use automation tools for deployment, which makes the process easier and faster. For example, deployment tools like Netlify or Argo CD help manage the release of the software and can even roll back the deployment if something goes wrong. Automated deployment also helps if the software requires special actions, like restarting machines or updating versions. 

### **7. Operations and Maintenance**  
After the software is deployed, developers enter the maintenance phase. This involves fixing any bugs that users report and making necessary updates to keep the software running smoothly. Maintenance also includes handling new issues that weren't found during testing. During this phase, the focus shifts from fast development to maintaining stability and uptime.

In DevOps, the operations team works closely with developers to ensure the software continues to run smoothly. Some key activities during this phase include:

- **Enabling Self-Service for Developers**  
  Developers are given tools and environments they can access on their own to help them solve problems quickly, which speeds up development.

- **Standardizing Tools and Processes**  
  To help teams collaborate better, the operations and development teams use standardized tools and methods. This reduces confusion and helps teams work more efficiently.

- **Automating Operations Tasks**  
  Many routine tasks, such as fixing issues, updating systems, or scaling infrastructure, are automated. This helps ensure consistency across the organization. For example, using tools like Terraform to automatically create virtual machines in the cloud can help track and manage system activity more easily.

As operations teams focus on automation, they also make sure that all systems are secure and compliant. Tools like Vagrant or Ansible help manage operations as code, meaning the system configurations are stored, versioned, and maintained securely.


## Keep CALMS
![image](https://github.com/user-attachments/assets/1573c2bc-e17e-4bf7-bf27-0e6aa5e3ee6c)

**CALMS Framework for DevOps Adoption**

CALMS is a framework that helps assess how well a company can adopt DevOps processes. The acronym stands for **Culture**, **Automation**, **Lean**, **Measurement**, and **Sharing**, and it was introduced by Jez Humble, co-author of *The DevOps Handbook*. Here’s a breakdown of each part:

### **Culture**  
DevOps isn't just a process or method; it's a change in culture. For DevOps to succeed, a company needs to shift its mindset. Instead of the slow, all-at-once approach of the waterfall model, teams need to break projects into smaller, manageable tasks that can be completed in short, focused sprints. This cultural change applies not just to development teams but also to QA, product management, and operations teams. Everyone in the company needs to embrace this new way of working.

### **Automation**  
Automation is a key element of DevOps. Since projects are broken down into smaller tasks, manually putting all the pieces together would be inefficient. Instead, automated processes are set up to reliably and repeatedly integrate new features. For new teams, this often starts with continuous delivery, but as teams mature, they can move to continuous integration. Advanced teams also automate the configuration process using tools like **configuration as code**, which defines how an application is set up based on its environment. This makes it easier to build production-ready code and helps prevent errors before code is deployed.

### **Lean**  
DevOps focuses on making tasks as small as possible so that teams can release early versions of software faster. The idea is to deliver a basic version of the application quickly and then improve it over time. This approach is more valuable than waiting years for a perfect product. By releasing early, teams can gather feedback from users and add new features based on their needs, making continuous improvement a core part of the process.

### **Measurement**  
To ensure that DevOps is working effectively, it’s important to measure progress. Metrics help track performance and allow teams to make small improvements. These metrics are used to monitor processes and ensure that teams are always improving. In later tasks, we will explore specific metrics to help with constant monitoring and improvement in DevOps.

### **Sharing**  
In a successful DevOps setup, everyone—developers, QA, product managers, and operations teams—shares responsibility for the final product. When all teams understand that they are collectively responsible for delivering the solution, the result is a better product for users. Shared responsibility leads to better collaboration and a more effective DevOps pipeline.


## DevOps Metrics

**Introduction**  
Before you can introduce security in the DevOps process, it's important to understand the metrics that DevOps engineers track. As we discussed in the "Introduction to DevSecOps" session, building empathy and understanding among teams is key to getting their support for security measures.

**DevOps Metrics**  
When manually creating infrastructure, deployments can be delayed, and too many errors in the live application can signal that security test automation needs improvement. To know where improvements are needed, engineers use specific metrics to track the performance of their processes. Here are some important metrics and the questions they help answer:

- **Meantime to Production (MTTP)**: How long does it take for new code changes to be deployed after they’re committed?
- **Frequency of Deployment**: How often are releases deployed?
- **Lead Time**: How long does it take to develop, build, test, and deploy a new feature?
- **Speed of Deployment**: Once a new release is ready, how long does it take to deploy it to production?
- **Deployment Agility**: This combines deployment speed and frequency to measure how quickly and often teams can deploy.
- **Production Failure Rate**: How often do failures occur in the live production environment?
- **MTTR (Mean Time to Recover)**: How long does it take to recover from a failure once it happens?

### **MTTP (Mean Time to Production)**  
One important DevOps metric is **MTTP**, which measures the time between when a code change is committed and when it’s deployed to production. For example, when a test passes, it means the code meets the required standards. By using test automation and working in small batches, teams can speed up MTTP. Quick feedback on code changes helps developers find and fix flaws faster, improving the time it takes to release code.

### **Failure Rate**  
The **failure rate** tracks how often code changes cause problems in production. This metric focuses on failures that happen after the code is deployed, not those caught during testing. A high failure rate may indicate issues with code quality. Practices that reduce MTTP times, like working in small batches and using automated tests, also help lower failure rates by making bugs easier to spot and fix. Monitoring failure rates is important to ensure new releases are secure.

### **Deployment Frequency**  
**Deployment frequency** tells you how often new code is deployed into production. This is an important metric because it shows how quickly teams can release new changes. Teams that can deploy on-demand, many times a day if needed, typically have automated deployment pipelines. These pipelines include automated testing and feedback loops, minimizing the need for manual intervention and speeding up the release process.

### **MTTR (Mean Time to Recover)**  
**MTTR** measures how quickly a system recovers after a failure. If there’s an issue with the service, it’s important to deploy a fix as soon as possible or roll back the changes that caused the failure. Monitoring system health continuously and having alerts in place helps teams respond quickly. Operations teams must be equipped with the right tools and permissions to resolve issues fast, ensuring minimal downtime.

### **Communicating Risk**  
Tracking these metrics allows you to show how the process improves over time, providing solid evidence to support your security goals. **Risk** can mean different things to different teams. For DevSecOps engineers, risk is the likelihood of a vulnerability being exploited and its potential impact on systems. For DevOps engineers, risk might refer to things like a high failure rate in production. By understanding the different definitions of risk, DevSecOps engineers can find common ground with other teams and help them see the security risks involved. This collaboration can help integrate security better across the DevOps process.

