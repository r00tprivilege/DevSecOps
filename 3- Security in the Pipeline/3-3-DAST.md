## DAST

### **Introduction to Dynamic Application Security Testing (DAST)**

#### **Overview**

Dynamic Application Security Testing (DAST) is a method of identifying vulnerabilities in an application by simulating the actions of an external attacker. This technique focuses on testing the application in its running state, rather than examining the code itself, making it an effective way to find security issues that may not be apparent during static analysis.

#### **Learning Objectives**
In this session, you will:
- Discover how DAST tools can be used to identify security weaknesses in live applications.
- Examine the benefits and limitations of using DAST compared to other security testing techniques.
- Get hands-on experience with some of the tools typically used for DAST in real-world environments. 

By the end of this exercise, you should have a deeper understanding of how DAST helps secure applications and how it fits into a comprehensive security strategy.

## Dynamic Application Security Testing (DAST)

### **What is Dynamic Application Security Testing (DAST)?**

Dynamic Application Security Testing (DAST) involves testing a live, running web application for vulnerabilities by simulating how an external attacker would approach the system. Unlike Static Application Security Testing (SAST), which analyzes source code, DAST treats the application as a "black box" and searches for weaknesses by exploiting potential vulnerabilities, either manually or through automated tools.

The key benefit of DAST is that it focuses on vulnerabilities that an attacker can exploit without needing knowledge of the underlying code or system architecture. This means DAST identifies issues that are likely to be found during real-world attacks, making it highly effective at identifying risks that might otherwise be overlooked. DAST doesn’t replace other testing methods but complements them by offering a more comprehensive security assessment when used alongside other techniques like SAST or manual penetration testing.

### **Manual vs Automated DAST**

DAST can be carried out in two ways:
1. **Manual DAST**: This involves a security expert manually testing the application by simulating attacks to discover potential vulnerabilities.
2. **Automated DAST**: Here, an automated tool scans the web application to find vulnerabilities without requiring manual intervention.

Both methods play vital roles in the Software Development Life Cycle (SDLC) and often work best when combined. While automated DAST tools can quickly scan large portions of code and provide immediate feedback, manual testing is essential for identifying complex or nuanced security flaws that may not be detected by automated tools. However, manual testing can be time-consuming, making it less feasible to use for frequent checks throughout the development process.

**Automated DAST** excels in performing continuous and fast scans during development cycles, while **Manual DAST** is better for in-depth testing, especially after the application has reached more stable stages or during major updates.

### **DAST in the Software Development Lifecycle (SDLC)**

DAST is most commonly integrated during the later stages of the SDLC. Typically, automated DAST tools are utilized during the testing phase, enabling rapid feedback on potential security issues. The automated scans focus on quickly finding simple vulnerabilities, such as open ports, insecure HTTP headers, and injection flaws, while more advanced security tests may require a manual approach.

While automated DAST provides a quick and efficient method of scanning, manual DAST often occurs periodically throughout development—such as on a weekly basis—depending on the project. This periodic testing helps ensure that more complex vulnerabilities, such as business logic flaws or deeper application-specific issues, are caught before the application is deployed to production.

When the application is close to being production-ready, performing a thorough web application penetration test (often considered an advanced form of DAST) is a standard practice. This comprehensive assessment aims to find deeper vulnerabilities that automated scans might miss.

### **Advantages and Disadvantages of DAST**

**Pros:**
- **Runtime Testing**: DAST identifies vulnerabilities during runtime, such as those that are unique to the live environment and may not be visible in the code alone.
- **Language-Agnostic**: DAST tools do not depend on the programming language used to build the application, making them adaptable to a wide range of environments.
- **Effective for Common Web Vulnerabilities**: DAST tools excel at finding specific issues like HTTP request smuggling, parameter pollution, or cache poisoning that might evade SAST tools.
- **Fewer False Positives**: Since DAST operates in a real-world environment, it typically generates fewer false positives compared to static analysis tools.
- **Identifies Business Logic Issues**: While not perfect, DAST tools can help detect certain business logic flaws, depending on the tool and configuration used.

**Cons:**
- **Limited Code Coverage**: DAST tools can miss vulnerabilities tied to unique, custom application behaviors that are triggered only by specific conditions.
- **Difficult for Dynamic Apps**: Applications that rely heavily on client-side JavaScript or complex workflows may be challenging for DAST tools to fully crawl and test.
- **No Detailed Remediation Information**: DAST tools often cannot provide in-depth remediation steps since they do not have access to the source code.
- **Slow for Some Tests**: Certain types of scans may take a considerable amount of time to complete, especially in large applications with many entry points.
- **Requires a Running Application**: DAST needs a live application instance, which means it is typically conducted after deployment or on a staging environment.

### **Getting Started with DAST**

Most DAST tools, especially automated ones, follow a basic set of operations to identify vulnerabilities:

1. **Spidering or Crawling**: The tool scans the application to map out its structure, identifying various URLs, endpoints, and parameters that can potentially be attacked.
2. **Vulnerability Scanning**: After mapping the application, the tool attempts to exploit the identified parameters by sending malicious payloads designed to uncover weaknesses such as SQL injections, XSS, or file inclusion vulnerabilities.

For demonstration, we will use a well-known DAST tool, **OWASP ZAP Proxy**. While ZAP is open-source and widely used in the industry, many enterprise-level DAST solutions are commercial products with additional features like integration with ticketing systems, detailed reporting, and advanced vulnerability management tools. Despite the differences in their feature sets, most enterprise-grade DAST tools work on the same core principles.

### **Summary of DAST Tools**

While **ZAP Proxy** is a great example of a DAST tool, commercial DAST tools often offer advanced features such as:
- **Integrated Dashboards** for visual vulnerability tracking.
- **Automated Ticketing System Integrations** to facilitate vulnerability tracking and resolution.
- **Expanded Rule Sets** for detecting a broader range of vulnerabilities.

The main difference between DAST tools lies in their capabilities for detecting vulnerabilities and their added enterprise features. However, the core tasks of vulnerability scanning and crawling are consistent across different tools.

## Spiders and Crawlers

### **Web Crawling and Spidering for Vulnerability Testing**

#### **Crawling a Web Application with ZAP Proxy**

In the first phase of vulnerability testing, it's crucial to map out all the accessible resources in a target web application. This helps define the scope for subsequent security assessments. One of the most effective tools for this is ZAP Proxy’s built-in **Spider** module, which automates the process of navigating through the application by following links on a specified starting page.

To begin the spidering process:

1. **Navigate to the Spider Tool**: Open **ZAP Proxy**, then go to the menu and select **Tools > Spider**. This opens the Spider interface where you can set the target web application's URL as your starting point.

2. **Configure the Spider**: In the Spider dialog, enter the starting page URL (e.g., `http://localhost:8080`). You can leave the **Context** and **User** fields blank for now. You can also choose additional options:
   - **Recurse**: This option ensures that all links within the website are followed recursively.
   - **Spider Subtree Only**: Restrict spidering to only the subfolders beneath the provided URL.
   - **Show Advanced Options**: Enable the advanced settings to further customize the spidering process if needed.

3. **Start the Scan**: After setting up, click **Start Scan**. ZAP will begin crawling the site, starting from the provided URL and exploring linked pages. You will see the list of discovered URLs populate under the **Sites** tab.

For example, if you initiate the scan with a starting URL like `http://localhost:8080/`, the tool will list all reachable pages from that starting point. Any URL outside of this root address will be flagged as out-of-scope and not included in the crawl results.

#### **Challenges with JavaScript Links**

In modern web applications, many dynamic elements are created using JavaScript, which may not be visible in the initial HTML source code. If you look at the scan results, you might notice some URLs are missing. This can happen if the link you are looking for is generated dynamically by JavaScript. For instance, a link such as `/dynamic-gallery.php` may not appear in the results if it was rendered by JavaScript after the page load.

Since ZAP’s standard spider doesn’t process JavaScript, it won't be able to follow links generated through this method. In such cases, **AJAX Spider** can be used to handle JavaScript-rendered content.

#### **Using AJAX Spider for Dynamic Content**

To bypass the limitations of the standard spider, **ZAP Proxy** offers an advanced feature called **AJAX Spider**, which allows the tool to simulate interactions with a real browser, such as Firefox or Chrome. This helps process JavaScript content and crawl dynamically generated pages. 

**Steps to Use AJAX Spider**:
1. **Start the AJAX Spider**: Go to **Tools > AJAX Spider** in ZAP. Input the initial URL as the target, just like the regular spider. In the **Browser** dropdown, select **Firefox** (you can choose headless browsers for non-GUI operations if preferred).

2. **Start the Crawl**: Once you’ve selected the browser and configured the options, click **Start Scan**. ZAP will launch Firefox and begin interacting with the application, just as a real user would. During the scan, you’ll notice that the browser loads pages and executes scripts on the site.

3. **Review Crawled URLs**: After the AJAX Spider completes its run, ZAP will update the **Sites** tab with the newly discovered URLs, including those that were rendered dynamically by JavaScript (e.g., `/dynamic-gallery.php`). These pages would have been missed by the regular spider but are now included due to the AJAX Spider’s use of a real browser for crawling.

This method is particularly useful for modern applications that heavily rely on JavaScript to generate or modify content after the initial page load. By using a real browser to parse the HTML generated by these scripts, the AJAX Spider can fully capture the dynamic behavior of the application, ensuring a more comprehensive security test.

#### **Summary**

1. **Regular Spidering**: Start by using the **Spider** tool to map out static content by crawling all the links on your target URL. This helps identify basic vulnerabilities in static resources.
   
2. **AJAX Spidering**: For websites that use JavaScript to dynamically generate or alter content, employ the **AJAX Spider** tool. This will simulate real user interactions with a browser to fetch dynamically generated links and elements that standard spiders might miss.

3. **Refined Coverage**: Combining both regular spidering and AJAX spidering gives you a complete map of the web application, ensuring that both static and dynamic resources are included in the vulnerability assessment.

By using both spidering techniques, you can ensure a thorough scan of your web application, helping identify both simple and complex vulnerabilities that may otherwise be overlooked.

## Scanning for Vulnerabilities

### **Vulnerability Scanning with ZAP Proxy**

#### **Customizing a Scan Policy in ZAP Proxy**

When using Dynamic Application Security Testing (DAST) tools like **ZAP Proxy**, configuring a customized scan policy is essential for efficient vulnerability detection. Tailoring the scan profile to the specific needs of your web application ensures that unnecessary payloads are not sent, which saves time and focuses on the most relevant tests. 

In most cases, **DAST tools** are used in a **white-box** setup, where the details of the underlying application and technologies are already known. For example, the web application we're using for this exercise has the following details:

- **Operating System**: Ubuntu
- **Web Server**: Nginx 1.18
- **Programming Language**: Python (no frameworks)
- **Databases**: None

Since our application doesn't use a database, running a default scan profile might be inefficient. For instance, the scanner might try SQL injection tests that are irrelevant to our application, unnecessarily extending the scan time. This is particularly noticeable when scanning more complex applications, where scanning irrelevant vulnerabilities can waste valuable time.

To create or modify a scan policy in **ZAP Proxy**, follow these steps:

1. Go to **Analysis > Scan Policy Manager** in the ZAP menu.
2. Click on **Add** to create a new scan policy or modify an existing one.

This will open the policy manager, where you can configure different types of tests based on your application's requirements.

#### **Understanding Scan Policy Parameters**

Each scan category in ZAP comes with two essential parameters:

- **Threshold**: Controls the level of confidence required before ZAP reports a vulnerability.
  - **Low threshold**: ZAP will report vulnerabilities based on minimal information. This could lead to more findings, but some may be false positives.
  - **High threshold**: ZAP will report vulnerabilities only if there is a high degree of certainty, reducing false positives but potentially missing some vulnerabilities (false negatives).
  - **OFF**: Disables a category of tests entirely.

- **Strength**: Controls the number of tests conducted in a given category.
  - **Higher strength**: More tests will be performed, potentially uncovering more vulnerabilities but significantly increasing scanning time.
  - **Lower strength**: Fewer tests will be run, saving time but possibly missing vulnerabilities.

Each application's requirements will determine the ideal combination of these settings. It's often a matter of trial and error to find the optimal configuration.

For our specific example:
- Since the application does not use a database or any XML processing, we can safely **disable all tests related to databases** and **XML processing**. 
- We should also **disable DOM-based Cross-Site Scripting (XSS) tests**, as these can consume substantial resources and will not be relevant for this example.

#### **Running Your First Scan**

Once the scan policy is configured, it's time to initiate an actual vulnerability scan:

1. Go to **Tools > Active Scan** in the ZAP menu.
2. Select the starting point from the list of URLs that were previously crawled (e.g., `http://localhost:8081/`).
3. Check the **Recurse** box to ensure the scanner checks all pages that are linked from the starting point. 
4. Click **Start Scan** to begin the process.

The scan will start, and over time, you will begin to see the results in the **Alerts** section of ZAP. Each alert will contain a description of the vulnerability found, as well as details of the request and response used to detect the issue.

#### **Reviewing Scan Results**

The **Alerts** section provides an overview of the vulnerabilities discovered during the scan. For each finding, you will see a summary of the issue, including:

- **Description**: A general explanation of the vulnerability.
- **Request/Response**: The specific request made and the corresponding response that led to the detection.

Once the scan is complete, review the findings to verify their validity. If you believe a result is a **false positive**, you can mark it as such by right-clicking the finding in the **Alerts** tab and selecting **Mark as False Positive**.

#### **Summary of Steps:**

1. **Create a customized scan policy**: Tailor the scan profile based on your application's technologies and potential attack vectors. Disable irrelevant tests to save time.
2. **Run the active scan**: Use the **Active Scan** tool to initiate the scanning process, starting from the previously discovered URLs.
3. **Review results**: After the scan completes, assess the findings, ensuring they're accurate. Mark any false positives appropriately.

By following these steps and adjusting the scan policies to fit your specific application, you'll be able to conduct effective vulnerability scans that are both efficient and accurate.


## Authenticated Scans

### **Authenticated Vulnerability Scanning in ZAP Proxy**

#### **Handling Logins in Scans**

Up to now, we’ve run a successful scan and identified several vulnerabilities in the target application. However, there are still more vulnerabilities to discover. One area that hasn’t been covered yet is the **administration panel**, which can only be accessed after logging in. Since **ZAP Proxy** does not automatically have the credentials to access this section, it cannot scan areas requiring authentication.

To resolve this, we need to teach ZAP how to authenticate and maintain an active session during the scanning process. This can be achieved by recording the authentication flow into a **ZEST script**, allowing ZAP to repeat this process during its scans. **ZEST scripts** essentially record and replay a series of HTTP requests, making them useful for automating login procedures.

**Important**: Disable the ZAP **HUD** (Heads-Up Display) in the toolbar during this process. Some functions may not work as expected if the HUD is enabled. You can find the button to disable it at the far end of the toolbar.

#### **Recording the Authentication Process**

1. **Start a new ZEST script**: 
   - Click on **Record a New ZEST Script** from the ZAP toolbar.
   - Set the script title and select **Authentication** as the script type.
   - Enter the base URL of the application to filter out unrelated requests from other sites.

2. **Begin recording**: 
   - Click **Start Recording**. This will record all HTTP requests sent through ZAP Proxy.
   - Open the browser by clicking the **Open Browser** button in the toolbar.
   
3. **Log into the application**: 
   - In the opened browser, navigate to `http://example.com/login`.
   - Log in manually using the following credentials:
     - **Username**: adminuser
     - **Password**: securepassword123

4. **Stop recording**: 
   - Once you’re logged in, stop recording by clicking the **Record a New ZEST Script** button again.
   - You can close the browser window as well.
   
5. **Review and delete unnecessary requests**: 
   - Some captured requests may not be required for the authentication flow (like static assets or unrelated API calls). You can remove those from the script.

6. **Testing the recorded script**: 
   - After the script is recorded, you can test it by running it in the **Script Console**.
   - The application should respond to the login POST request with a redirect to a user dashboard (e.g., `dashboard.php`).

#### **Creating a Context for Authentication**

Now that we’ve recorded the authentication script, we need to link it to a **Context**. A context defines a group of URLs where the authentication will be applied. In our case, the authentication applies to the entire application, so we’ll create a context that encompasses all URLs.

1. **Creating the context**:
   - Right-click on the base URL (e.g., `http://example.com`) under the **Sites** tab and select **Include in Context -> New Context**.
   - This creates a **regex** that matches all pages in the application.

2. **Linking the ZEST script**:
   - In the **Context** settings, go to the **Authentication** tab.
   - Set the authentication type to **Script-based Authentication** and load the ZEST script by clicking **Load**.
   
3. **Defining a user**: 
   - ZAP requires at least one user to be defined in the **Users** section, even though the credentials are embedded in the ZEST script. Create a user for the context, but the script will handle authentication.

4. **Finalize the context**:
   - Click **OK**. The resources under the **Sites** tab will now be marked with a target icon, indicating they are part of the defined context.

#### **Re-spidering the Application**

With the authentication context set up, we now need to run the spider again, but this time with the authentication details in place.

1. **Re-run the spider**:
   - Right-click on the base URL and choose **Re-run Spider** with the context and user you created.
   - This will allow ZAP to crawl all authenticated areas of the application, which were previously hidden.

2. **Review new resources**:
   - Once the spidering process is complete, check the **Added Nodes** tab to see which new resources have been discovered. You might see new parts of the app that require authentication to access.

#### **Preventing Logouts During Scans**

During the spidering or scanning process, ZAP might inadvertently log out of the session, especially if it interacts with logout pages (e.g., `logout.php`). To prevent this from happening:

1. **Excluding logout pages**:
   - Right-click on any logout-related scripts (e.g., `logout.php`) in the **Sites** tab and choose **Exclude from Context**.
   - This ensures that ZAP avoids interacting with logout pages during scans.

2. **Defining session indicators**:
   - To ensure ZAP recognizes when the session is still active, define **logged-in** and **logged-out** indicators based on specific page elements.
   - For instance, if `dashboard.php` is only accessible when logged in, we can use that as a **logged-in indicator**.
   - Right-click on the **dashboard.php** page in the **Sites** tab, select the text associated with the logout link, and choose **Flag as Context -> (Your Context Name): Authentication Logged-in Indicator**.

3. **Defining logged-out indicators**:
   - Similarly, you can define a **logged-out indicator**, such as the login link on a page like `aboutme.php`, which is visible only when the user is logged out.
   - Right-click on the HTML link for the login page and select **Flag as Context -> (Your Context Name): Authentication Logged-out Indicator**.

4. **Set up a verification strategy**:
   - In the **Context** settings under **Authentication**, configure a **Verification Strategy** to check the status of the session periodically. For example, you can configure ZAP to poll the `/aboutme.php` page every 60 requests to verify if the session is still valid.

#### **Final Scan with Authentication**

Now that the authentication flow, context, and session verification are configured, we can run the final scan to cover authenticated areas of the application.

1. **Run the active scan**:
   - Go to **Tools > Active Scan**, select the context and user you created, and start the scan.

2. **Review the results**:
   - ZAP should now discover additional vulnerabilities that were previously inaccessible due to authentication restrictions. Be sure to review any new findings and address the highest-risk vulnerabilities.

By following these steps, you will have successfully configured authenticated scans in **ZAP Proxy**, ensuring that the security assessment covers both publicly accessible and protected areas of your web application.


## Checking APIs with ZAP

### **Scanning APIs for Security Vulnerabilities**

Web applications increasingly rely on APIs to handle backend operations and integrate with third-party services. Unlike traditional web applications, APIs are typically more challenging to scan because they don’t have interconnected pages or visible links that a spider can crawl. Each API endpoint usually operates independently, and discovering new endpoints without explicit knowledge from the development team is difficult. Additionally, even when an endpoint is known, it’s necessary to understand the parameters that can be passed to each endpoint to properly test it.

In this scenario, instead of relying on automated spidering techniques to discover API endpoints, we will depend on the development team to provide a precise API specification. This allows us to bypass the discovery phase and focus directly on testing the security of the endpoints.

#### **API Documentation**
To ensure we can interact with the API effectively and test its security, the development team typically provides API documentation, which includes a list of all available endpoints and the required parameters. This documentation often follows standardized formats, such as **OpenAPI (formerly Swagger)**, **SOAP**, or **GraphQL**.

For example, in an OpenAPI 2.0 specification, the file will include a list of API paths, each specifying the available HTTP methods (such as `GET`, `POST`, `PUT`, etc.) and the required parameters for each request. Here's an example of an OpenAPI specification for an endpoint `/media/{item_id}`:

```json
"/media/{item_id}": {
  "get": {
    "parameters": [
      {
        "description": "Unique media item identifier",
        "in": "path",
        "name": "item_id",
        "required": true,
        "type": "string"
      }
    ],
    "responses": {
      "default": {
        "description": "Returns media item details",
        "schema": {
          "$ref": "#/definitions/MediaItem"
        }
      }
    }
  }
}
```

This specification tells us that a `GET` request to `/media/{item_id}` requires the `item_id` parameter to be passed in the URL, and the response will contain details about the specified media item.

API documentation may be complex and difficult to read in its raw format. For ease of use, many API providers will also offer a **Swagger UI** or similar interface that allows users to explore and test API endpoints interactively.

**Note:** In a production environment, API documentation is often kept hidden to reduce the risk of exposing sensitive details about the API. In such cases, it’s crucial to ask the development team for access to the API specifications.

#### **Importing API Specifications into ZAP**
ZAP supports importing API definitions in multiple formats, including OpenAPI, SOAP, and GraphQL. You can import the API definitions either via a local file or a URL. If the API specification is available online, you can import it directly from the URL.

For instance, if the API documentation is accessible at `http://example.com/api/swagger.json`, you can follow these steps to import it into ZAP:

1. Navigate to **Import -> Import an OpenAPI definition from a URL** in ZAP.
2. Enter the URL (e.g., `http://example.com/api/swagger.json`) and click **Import**.

Once imported, ZAP will process the API definition and display the available endpoints and parameters in the **Sites** tab. The tool will automatically start passive scanning of these endpoints and report any potential security issues it identifies.

#### **Scanning the API**
After importing the API specification into ZAP, you can scan it just like any other web resource. Here’s how you can perform an active scan against the API:

1. Right-click the API URL (e.g., `http://example.com/api`) in the **Sites** tab.
2. Select **Attack -> Active Scan** from the context menu.

ZAP will begin scanning the API for vulnerabilities, testing the security of each endpoint by attempting to identify issues such as improper authentication, authorization flaws, injection vulnerabilities, and other common security risks.

#### **Reviewing Scan Results**
Once the scan completes, you can view the results in the **Alerts** tab. ZAP will show you any vulnerabilities it discovered during the scan. Each finding will include details such as the type of vulnerability, the affected endpoint, and recommended remediation actions.

These results will help you identify areas of the API that may need to be secured, enabling you to ensure that the API endpoints are robust and protected against potential attacks.

By following this process, you can effectively scan APIs for security vulnerabilities, ensuring that they are secure and reliable for use within your application.

## Integrating DAST into the development pipeline

### **Automating Security Scanning in DevSecOps Pipelines**

When incorporating **Dynamic Application Security Testing (DAST)** into a development pipeline, the goal is to run automated security scans on web applications and APIs. This process aims to detect vulnerabilities early in the development cycle. While this might sound straightforward, there are several considerations to ensure that security testing doesn’t disrupt the development flow.

Key factors to consider for implementing automated DAST in a pipeline:
- **Deciding on Scan Frequency**: We need to determine when scans should run during the development process. Should they run on every code commit, or be scheduled at specific times (e.g., nightly)?
- **Triggering Scans**: Scans can be triggered manually after a commit, automatically after each commit, or at scheduled intervals.
- **Scan Intensity**: Running a full, comprehensive vulnerability scan on each commit may significantly slow down the development process. We need to choose a scan profile that ensures critical vulnerabilities are identified without slowing down development.

To minimize disruptions, we will work with the development team to balance security testing needs with the existing development workflow.

In this task, we'll explore how to quickly integrate DAST into the CI/CD pipeline. The pipeline will trigger automatic security scans with each commit to test a subset of vulnerabilities to avoid long delays.

### **Reviewing the CI/CD Pipeline**

Our development pipeline includes the following components:

- **Source Code Repository**: The code for the web application and APIs is stored in a repository hosted on a **GitLab** server, located at `http://192.168.1.100:4000/`.
- **CI/CD Server**: A **Jenkins** instance automates the build, test, and deployment process. You can access Jenkins at `http://192.168.1.100:8080/`.

Every time a commit is made to the GitLab repository, Jenkins picks up the code, builds a Docker container, and deploys it. These Docker containers are what we'll scan for vulnerabilities.

To access the repository or Jenkins, use the following credentials:

- **Username**: devsecops  
- **Password**: securepassword  

### **Automated Scanning with zap2docker**

To integrate **OWASP ZAP** into our CI/CD pipeline, we will use `zap2docker`, a Dockerized version of ZAP designed for automation. The official documentation for `zap2docker` can be found here.

**Note**: The following commands are for reference purposes. You don’t need to run them manually as Jenkins will execute them for you later.

1. **Install zap2docker**  
   First, pull the `zap2docker-stable` image from Docker Hub:
   ```bash
   docker pull owasp/zap2docker-stable
   ```

2. **Scan Profiles**  
   ZAP provides different scan scripts. Below are a few examples of the available scan profiles:

   - **Baseline Scan**: A quick scan that spiders the target website for up to 1 minute, with no active scanning.
     ```bash
     docker run -t owasp/zap2docker-stable zap-baseline.py -t http://192.168.1.100:5000/
     ```

   - **Full Scan**: Performs both spidering and an active scan without time limitations.
     ```bash
     docker run -t owasp/zap2docker-stable zap-full-scan.py -t http://192.168.1.100:5000/
     ```

   - **API Scan**: Scans APIs, requiring an API description file (e.g., OpenAPI, GraphQL, or SOAP).
     ```bash
     docker run -t owasp/zap2docker-stable zap-api-scan.py -t http://192.168.1.100:5000/api/swagger.json -f openapi
     ```

   You can add the `-j` flag to perform an AJAX scan during the baseline and full scans.

### **Integrating ZAP into the CI/CD Pipeline**

We already have a pre-configured `zap2docker` instance in our environment. The task now is to instruct Jenkins to run `zap2docker` with the appropriate settings.

In Jenkins, we can see an organization called `secops`, which contains two repositories for the web application and API. Each repository has a `main` branch.

For example, the **web-app** project has already been built twice. The Jenkins pipeline consists of two stages:
- **Building the Docker Image**: This stage compiles the code and creates a Docker image.
- **Deploying the Docker Image**: This stage deploys the Docker container to the application environment.

Each stage is defined in the Jenkinsfile within the repository. For instance, in the web-app repository’s Jenkinsfile, the web application is deployed to port `8082`.

If we want to integrate ZAP, we can add a **third stage** after the Docker image is built to run security scans on the application. This stage is already defined in the Jenkinsfile, and we can simply uncomment the necessary section to enable it.

We will use the **Baseline Scan** profile for every commit to avoid slowing down the pipeline with long-running full scans. The Baseline Scan identifies high-priority issues but skips more time-consuming active scans like **SQL injection** or **Cross-Site Scripting** (XSS).

### **Running the Automated Scan**

Once the changes are committed, Jenkins will automatically start the build process. You can monitor the progress in Jenkins by visiting the **web-app** project and viewing the builds.

The build will take around 5 minutes. After completing the scan, it will likely fail because ZAP will detect vulnerabilities in the application. To check the results, go to the **Workspaces** section of the build.

In the **zap-reports** folder, you can find the **ZAP report**. Download and review the report to answer the questions at the end of the task.

**Note**: Make sure to download and save the report rather than opening it directly from Jenkins, as viewing it in the Jenkins interface might cause formatting issues.

### **Repeating the Process for the API**

Now that ZAP is integrated into the web-app pipeline, we can repeat the same process for the **API** repository. Once ZAP has run the scan on the API, you can view the results in the **zap-reports** folder of the Jenkins build workspace for the **simple-api** project.

Download and analyze the report to answer the corresponding questions.

By integrating ZAP into the CI/CD pipeline, you can now run automated security scans with each commit to proactively identify vulnerabilities in both your web applications and APIs. This approach provides early detection of security issues, enabling faster remediation while keeping the development pipeline running smoothly.
