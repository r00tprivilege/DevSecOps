## SAST

### **Introduction**

In this module, we will explore **Static Application Security Testing (SAST)**, a crucial technique for identifying vulnerabilities within the application code during its development phase. By analyzing the source code, SAST helps detect potential security flaws before the application goes live. This study will highlight the strengths and limitations of SAST, as well as how it can be integrated with other security practices to enhance the overall protection of applications right from the early stages of development.

### **Learning Objectives**
- Gain insights into how SAST can be utilized to uncover security weaknesses in real-world software projects.
- Explore the benefits and challenges associated with using SAST as part of the security testing process.
- Understand how to seamlessly incorporate SAST into various stages of the software development lifecycle to enhance security.

## Code Review

### **Code Review: Ensuring Secure Software Development**

A key method for building secure applications is through **code review**, a practice where the source code of an application is examined for potential security flaws. Code reviews provide a detailed, white-box approach, meaning the reviewer has full access to the codebase, allowing for a comprehensive check of the application’s functionality and logic. By continuously reviewing the code throughout the development process, developers can catch vulnerabilities early, ensuring that they are addressed before the software reaches production. This proactive approach significantly reduces the time and effort required to resolve security issues, which would otherwise escalate in complexity and cost if discovered later in the development cycle.

### **Importance of Early Detection**

If vulnerabilities are overlooked or ignored early in the development process, they can accumulate and persist until the final stages of development, where fixing them becomes much more difficult and expensive. Code reviews focus on identifying these vulnerabilities in the early stages, making them easier and less costly to correct.

### **Manual vs Automated Code Review**

Code reviews generally involve both **manual inspection** and the use of **automated tools**, with each having its own strengths and weaknesses. Striking the right balance between both methods is crucial for achieving effective security testing at various points in the development cycle.

- **Manual Code Review**:
  - A manual review allows for in-depth analysis by a skilled reviewer, who can identify subtle issues that might not be caught by automated tools. This is especially important for complex or custom code logic that tools may not understand fully.
  - However, the task can become overwhelming, especially with large codebases. A reviewer’s ability to maintain focus can decrease over time, leading to missed vulnerabilities due to fatigue or oversight. Additionally, manual reviews are generally more time-consuming and expensive.
  
- **Automated Code Review**:
  - Automated tools offer a fast and efficient way to scan the code for known vulnerabilities. These tools can instantly process large amounts of code, providing consistent results. They excel at identifying common or standardized vulnerabilities quickly, which saves significant time and effort compared to manual inspection.
  - However, automated tools are limited by the predefined set of rules they use to detect vulnerabilities. If a tool’s rule set does not cover a specific vulnerability, it will likely miss it. Therefore, these tools work best when combined with manual reviews, particularly for more complex or unusual vulnerabilities.
  
### **Cost Considerations**

The cost of manual reviews is generally higher, as they require significant time and expertise from the reviewer. Automated tools, on the other hand, provide a more cost-effective solution by quickly scanning code for basic vulnerabilities without human involvement. This makes automated tools ideal for early-stage testing, where many of the common issues can be addressed swiftly and efficiently.

### **Best Practices for Code Review**

To maximize the effectiveness of code reviews, a hybrid approach is often recommended:
- **Early Stage**: Use **automated tools** in the initial stages of the development lifecycle. These tools can quickly identify low-hanging fruit (simple vulnerabilities), allowing developers to address them early, saving time and reducing costs.
- **Periodic Manual Reviews**: As the project progresses, schedule **manual code reviews** at critical points in the development cycle, especially when complex logic is introduced or significant milestones are reached. Manual reviews are essential for catching nuanced or less common vulnerabilities that automated tools might miss.

By combining both manual and automated approaches, teams can ensure a comprehensive and efficient process for securing applications throughout their development.


## Manual Code Review

### **Manual Code Review for Vulnerability Detection**

Before delving into Static Application Security Testing (SAST) tools, it's important to understand how manual code reviews are conducted. This understanding will provide clarity on how SAST tools analyze code for vulnerabilities. In this task, our goal is to manually identify **SQL injection vulnerabilities** within the source code of a basic web application. While the application has other security issues, we will focus on detecting SQL injection flaws to understand the traditional process of code reviewing and how it correlates with automated analysis tools like SAST.

#### **Getting Started**
Make sure your virtual machine (VM) is running before proceeding. If it is not already started, click the "Start Machine" button attached to this task. If the VM appears in split view and is not visible, click the "Show Split View" button located at the top right of this room.

For this task, the code to review can be found at the directory path:  
`/home/ubuntu/Desktop/simple-webapp/`

#### **Step 1: Searching for Potentially Insecure Functions**
The first step in a code review is identifying potentially insecure functions. In our case, we are looking for SQL injection vulnerabilities, so we need to find any functions that could interact with the database in a way that might be vulnerable to SQL injection attacks. Since the application uses **PHP** and **MySQL**, we should focus on functions related to sending raw queries to the database. Some common PHP functions to look for include:

| Database Engine | Function             |
|-----------------|----------------------|
| MySQL           | `mysqli_query()`      |
|                 | `mysql_query()`       |
|                 | `mysqli_prepare()`    |
|                 | `query()`             |
|                 | `prepare()`           |

A simple way to search for such functions in our project's code is to use the `grep` command. To search for instances of `mysqli_query()`, navigate to the base directory of the project and execute the following command:

```bash
user@machine$ cd /home/ubuntu/Desktop/simple-webapp
user@machine$ grep -r -n 'mysqli_query('
```

The `-r` option tells `grep` to recursively search all files, and the `-n` option provides the line number where the function appears. The output might look something like this:

```bash
db.php:18: $result = mysqli_query($conn, $query);
```

This output shows that `mysqli_query()` is used on line 18 of the `db.php` file. While this might indicate a potential vulnerability, we cannot be sure just from this single line. Let's analyze the context further.

#### **Step 2: Understanding the Context of the Vulnerability**
Let's open the `db.php` file and examine the surrounding code:

```php
function db_query($conn, $query) {
    $result = mysqli_query($conn, $query);
    return $result;
}
```

Here, we see that `mysqli_query()` is wrapped inside the `db_query()` function, and the `$query` parameter is passed directly without any sanitization or validation. This is where potential vulnerabilities may arise.

#### **Step 3: Tracing User Input to Potentially Vulnerable Functions**
Next, we need to trace where `db_query()` is called in other parts of the code to track user input that could potentially lead to an SQL injection. Using `grep`, we search for instances of `db_query()`:

```bash
user@machine$ grep -r -n 'db_query('
```

This might return results like:

```bash
hidden-panel.php:7: $result = db_query($conn, $sql);
hidden-panel.php:20: $result2 = db_query($conn, $sql2);
hidden-panel.php:23: $result3 = db_query($conn, $sql3);
db.php:17: function db_query($conn, $query) {
```

We can see that `db_query()` is used in `hidden-panel.php` at lines 7, 20, and 23. Let's investigate each of these lines individually.

#### **Step 4: Analyzing the Vulnerable SQL Queries**
Start with the first instance found on line 7:

```php
$sql = "SELECT id, firstname, lastname FROM MyGuests WHERE id=" . $_GET['guest_id'];
$result = db_query($conn, $sql);
```

Here, the `$_GET['guest_id']` input is directly concatenated into an SQL query. Since there is no input sanitization, this is a classic case of SQL injection vulnerability. An attacker could manipulate the `guest_id` parameter to alter the query's behavior.

Next, let's look at the second instance on line 20:

```php
$sql2 = "SELECT id, logtext FROM logs WHERE id='" . preg_replace('/[^a-z0-9A-Z"]/', "", $_GET['log_id']) . "'";
$result2 = db_query($conn, $sql2);
```

In this case, the `$_GET['log_id']` input is sanitized using `preg_replace()`, which only allows alphanumeric characters and double quotes. However, because the SQL query is enclosed in single quotes (`'`), double quotes won't pose a threat in this situation. This query is not vulnerable to SQL injection because the input is properly sanitized.

Now, let's examine the third instance on line 23:

```php
$sql3 = "SELECT id, name FROM asciiart WHERE id=" . preg_replace("/[^0-9]/", "", $_GET['art_id'], 1);
$result3 = db_query($conn, $sql3);
```

In this case, the `$_GET['art_id']` input is sanitized using `preg_replace()` with the restriction that only numeric characters are allowed. However, the third parameter of `preg_replace()` is set to `1`, meaning only the first non-numeric character will be removed. Any subsequent non-numeric characters will remain, leaving the query vulnerable to SQL injection. This line **is vulnerable** because an attacker could inject non-numeric characters past the first replacement.

#### **Step 5: Conclusion from Manual Review**
We have identified two SQL injection vulnerabilities in the application:
- The first vulnerability in `hidden-panel.php` (line 7) is due to improper handling of user input in the SQL query.
- The third vulnerability in `hidden-panel.php` (line 23) is due to insufficient sanitization, which allows attackers to bypass the filter.

While this example is relatively simple, a real-world application would likely contain much larger codebases, making manual reviews much more difficult. Tracing every instance of a potentially vulnerable function can be overwhelming. This is where **SAST tools** can automate the process of scanning the entire codebase and flagging potential vulnerabilities.

#### **Next Steps: Using SAST Tools**
Now that we have completed the manual review and identified SQL injection vulnerabilities, we will move on to using SAST tools. These tools can help us automate the process of vulnerability detection and provide a more efficient way to analyze code for security issues at scale. We will assess how well these tools perform and compare them with our manual review findings.


## Automated Code Revie

### **Automated Code Review with Static Application Security Testing (SAST)**

#### **Introduction to Static Application Security Testing (SAST)**

Static Application Security Testing (SAST) refers to the process of using automated tools to analyze source code for security vulnerabilities. The goal of SAST is not to replace manual code reviews but to provide a quick and efficient way to automate basic code checks, helping developers find vulnerabilities early in the development process. Unlike manual code reviews, SAST tools can run quickly and continuously during the development lifecycle, making it easier to detect flaws without requiring highly specialized security knowledge.

SAST complements other security methods, such as **Dynamic Application Security Testing (DAST)** and **Software Composition Analysis (SCA)**, to ensure comprehensive security coverage throughout the development lifecycle. Like any security technique, SAST has its own set of strengths and limitations:

| **Pros**                                                                 | **Cons**                                                                 |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------|
| Does not require a running instance of the application                  | The source code may not always be accessible (especially for third-party apps) |
| Offers broad coverage of application functionality                      | Can generate false positives                                            |
| Faster execution compared to dynamic analysis methods                    | Cannot identify vulnerabilities related to runtime behavior             |
| Reports exact locations of vulnerabilities within the code               | Often specific to certain programming languages; may not support all languages |
| Easy to integrate into Continuous Integration/Continuous Deployment (CI/CD) pipelines | May miss complex vulnerabilities that are context-dependent            |

#### **How SAST Works**

Most SAST tools follow a two-step process to detect vulnerabilities in code:

1. **Code Transformation:**  
   SAST tools begin by ingesting the source code and transforming it into an abstract representation for easier analysis. This step is crucial for enabling a deeper analysis of the code, independent of its syntax and structure. Commonly, SAST tools use **Abstract Syntax Trees (ASTs)**, though some tools may use proprietary representations that suit their analysis techniques.

2. **Vulnerability Analysis:**  
   After the code has been transformed into an abstract model, the tool applies various analysis methods to identify potential security flaws. These techniques range from basic function searches to complex dataflow analysis. Let's review some of the key analysis techniques used by SAST tools.

#### **Key Analysis Techniques Used by SAST Tools**

1. **Semantic Analysis**  
   Semantic analysis aims to identify insecure coding practices by searching for potentially dangerous functions within localized contexts. It's similar to manually "grepping" through code for vulnerable functions. For example, a common vulnerability in PHP applications is the improper use of user inputs directly in SQL queries:

   ```php
   mysqli_query($db, "SELECT * FROM users WHERE username=" . $_GET['username']);
   ```

   This line could result in a **SQL injection** vulnerability, as user input is directly injected into the query string without proper sanitization.

2. **Dataflow Analysis**  
   Dataflow analysis is used when a vulnerable function is found, but it's not immediately clear whether user inputs are properly sanitized before they reach the function. This method traces the flow of data throughout the application, from **sources** (user inputs) to **sinks** (dangerous functions). A source-to-sink path without proper input sanitization indicates a security flaw.

   For example, consider the following PHP function:

   ```php
   function db_query($conn, $query) {
       $result = mysqli_query($conn, $query);
       return $result;
   }
   ```

   To analyze whether this function is vulnerable, dataflow analysis would trace where the `$query` parameter originates. If it comes from an unsanitized user input (the source), it can potentially lead to a security risk when passed to the `mysqli_query()` function (the sink).

3. **Control Flow Analysis**  
   This analysis examines the logical flow of operations in the code to identify vulnerabilities such as race conditions, the use of uninitialized variables, or resource leaks. For instance, consider this Java snippet:

   ```java
   String cmd = System.getProperty("cmd");
   cmd = cmd.trim();
   ```

   If the `cmd` property is undefined or returns `NULL`, calling `.trim()` on `NULL` will throw a runtime exception. Control flow analysis identifies such risks by analyzing the sequence of operations and ensuring proper initialization and exception handling.

4. **Structural Analysis**  
   Structural analysis inspects the overall structure of code for issues like improper use of classes, functions that never execute (dead code), and insecure cryptographic practices. Here's an example of an insecure RSA implementation:

   ```php
   $options = array('private_key_bits' => 1024, 'private_key_type' => OPENSSL_KEYTYPE_RSA);
   $res = openssl_pkey_new($options);
   ```

   A 1024-bit RSA key is considered insufficient by modern security standards. Structural analysis would flag this implementation due to the weak key size.

5. **Configuration Analysis**  
   SAST tools also examine application configuration files for security misconfigurations that could lead to vulnerabilities. For example, in PHP, settings like `allow_url_fopen` and `allow_url_include` may enable remote file inclusion (RFI) and server-side request forgery (SSRF) attacks if misconfigured. A configuration check might find something like this:

   ```ini
   allow_url_include = On
   allow_url_fopen = On
   ```

   These configurations open attack vectors and would be flagged by SAST tools.

#### **Conclusion**

While each SAST tool may have its own approach and feature set, these core analysis techniques help identify various types of vulnerabilities early in the development process. By integrating SAST tools into your **CI/CD pipeline**, you can ensure that security vulnerabilities are identified and addressed as part of the regular software development lifecycle, enabling faster, more secure application releases.

It's important to remember that SAST tools aren't a one-size-fits-all solution and may not catch all types of vulnerabilities. They work best in conjunction with other security methods like **DAST**, **SCA**, and manual code reviews. By using these tools together, you can create a comprehensive security strategy that addresses both static and dynamic vulnerabilities.


## Rechecking Our Application with Static Analysis Tools

### **Rechecking Our Application with Static Analysis Tools**

#### **Introduction**

After understanding how Static Application Security Testing (SAST) tools work, we are now ready to use them to recheck an application. For this task, we will target a simple web application built with PHP, located in a folder called "basic-webapp" on your system. Our focus will be to identify potential vulnerabilities and review best practices.

#### **Using "Statix" Tool for PHP Code Analysis**

We will begin by using **Statix**, a straightforward static analysis tool for PHP code. This tool is pre-installed as part of the application's project setup, so no additional installation is required. However, if you need to install it manually, you can refer to Statix's official documentation for detailed steps.

To begin, open a terminal and navigate to the project's root directory. You will find a `statix.xml` file there, which serves as the configuration file for the tool. Here is an example of what the file might look like:

```xml
<?xml version="1.0"?>
<statix errorLevel="3" resolveFromConfigFile="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xmlns="https://getstatix.org/schema/config" xsi:schemaLocation="https://getstatix.org/schema/config vendor/statix/config.xsd" findUnusedBaselineEntry="true">
    <projectFiles>
        <directory name="src"/>
        <ignoreFiles>
            <directory name="lib"/>
        </ignoreFiles>
    </projectFiles>
</statix>
```

In the above configuration:

- The `errorLevel` parameter controls how strict the tool will be when identifying issues. A lower number means more issues will be flagged.
- The `projectFiles` section specifies the directories to scan (in this case, the `src` directory), while the `lib` directory is excluded to avoid scanning third-party libraries.

#### **Running Statix for Initial Code Review**

With the configuration in place, you can now run Statix using the following command from within the project directory:

```bash
user@machine$ cd /home/username/Desktop/basic-webapp/
user@machine$ ./vendor/bin/statix --no-cache
```

Statix will start analyzing the code, and here’s an example of the type of output you might see:

```bash
ERROR: TypeMismatch - src/panel.php:10:5 - Operand of type 0 is always falsy (see https://statix.dev/056)
    if ($result->num_rows = 0) {
```

In this case, Statix has identified an issue with a comparison operator. The programmer has mistakenly used the assignment operator (`=`) instead of the equality operator (`==`). As a result, the condition will always evaluate as false, which could cause unexpected behavior.

While these types of issues are not necessarily security vulnerabilities, Statix is helping to highlight potential problems that can lead to runtime errors. By adhering to these coding best practices, you can reduce the risk of bugs.

#### **Running Dataflow Analysis for Security Vulnerabilities**

One of Statix's key features is its ability to perform **dataflow analysis**, which looks for potential security vulnerabilities in the code. To enable this feature, run the following command:

```bash
user@machine$ ./vendor/bin/statix --no-cache --taint-analysis
```

The output will show any security issues related to untrusted input being passed into potentially dangerous functions. Here’s an example output:

```bash
ERROR: TaintedInclude - src/view.php:22:9 - Detected tainted code passed to include or similar (see https://statix.dev/251)
    $_GET
    <no known location>
    $_GET['img'] - src/view.php:22:28
    include('./assets/'.$_GET['img']);
```

In this case, the tool has flagged a **Local File Inclusion (LFI)** vulnerability, where user-controlled input (`$_GET['img']`) is concatenated directly into the path for an `include()` statement. This can lead to security risks if an attacker is able to manipulate the input to include arbitrary files.

Dataflow analysis can often reveal the most significant security flaws, but structural issues such as improper coding practices can also lead to other bugs or unpredictable application behavior. It's crucial to address both types of findings.

#### **Handling False Positives and False Negatives**

When using SAST tools, it’s important to be aware that errors may not always be accurate. These are generally categorized into two types:

1. **False Positives**: The tool flags a non-issue as a potential vulnerability.
2. **False Negatives**: The tool fails to identify an actual vulnerability.

For example, during manual code review, we identified two confirmed **SQL injection** vulnerabilities, but Statix only flagged one. Here's what you might see:

```bash
user@machine$ ./vendor/bin/statix --no-cache --taint-analysis
ERROR: TaintedSql - src/db.php:18:32 - Detected tainted SQL (see https://statix.dev/244)
    $_GET
    <no known location>
    $_GET['user_id'] - src/panel.php:6:65
    $sql = "SELECT id, name FROM Users WHERE id=".$_GET['user_id'];
    concat - src/panel.php:6:8
    $sql = "SELECT id, name FROM Users WHERE id=".$_GET['user_id'];
```

To further explore this issue, let's comment out the problematic code:

```php
// $sql = "SELECT id, name FROM Users WHERE id=".$_GET['user_id'];
// $result = db_query($conn, $sql);
```

Re-running Statix shows a new error related to a different query:

```bash
ERROR: TaintedSql - src/db.php:18:32 - Detected tainted SQL (see https://statix.dev/244)
    $_GET
    <no known location>
    $_GET['log_id'] - src/panel.php:19:87
    $sql2 = "SELECT id, text FROM logs WHERE id='".preg_replace('/[^a-z0-9A-Z"]/', "", $_GET['log_id']). "'";
    call to preg_replace - src/panel.php:19:87
    $sql2 = "SELECT id, text FROM logs WHERE id='".preg_replace('/[^a-z0-9A-Z"]/', "", $_GET['log_id']). "'";
```

Statix identifies the vulnerability correctly in the second query, but it may not have picked up the first one initially. This discrepancy arises because Statix treats both queries similarly and assumes that fixes should be applied at a generic database query level, not recognizing the difference between the two instances.

To help Statix better analyze the situation, we can add annotations to clarify that the `db_query()` function should be treated as a "sink" for SQL injections. The following comment can be added above the function definition:

```php
/**
 * @statix-taint-sink sql $query
 * @statix-taint-specialize
 */
function db_query($conn, $query) {
    $result = mysqli_query($conn, $query);
    return $result;
}
```

These annotations tell Statix to track potential tainted inputs that flow into the `db_query()` function, ensuring that it flags any vulnerable queries.

After running Statix again, we should now see a list of all SQL injection vulnerabilities, including those that were previously missed:

```bash
ERROR: TaintedSql - src/db.php:21:26 - Detected tainted SQL (see https://statix.dev/244)
    $_GET
    <no known location>
    $_GET['user_id'] - src/panel.php:6:65
    $sql = "SELECT id, name FROM Users WHERE id=".$_GET['user_id'];
    concat - src/panel.php:6:8
    $sql = "SELECT id, name FROM Users WHERE id=".$_GET['user_id'];
    call to db_query - src/panel.php:7:27
    $result = db_query($conn, $sql);

ERROR: TaintedSql - src/db.php:21:26 - Detected tainted SQL (see https://statix.dev/244)
    $_GET
    <no known location>
    $_GET['log_id'] - src/panel.php:19:87
    $sql2 = "SELECT id, text FROM logs WHERE id='".preg_replace('/[^a-z0-9A-Z"]/', "", $_GET['log_id']). "'";
    call to preg_replace - src/panel.php:19:87
    $sql2 = "SELECT id, text FROM logs WHERE id='".preg_replace('/[^a-z0-9A-Z"]/', "", $_GET['log_id']). "'";
    preg_replace - src/panel.php:19:87
    $sql2 = "SELECT id, text FROM logs WHERE id='".preg_replace('/[^a-z0-9A-Z"]/', "", $_GET['log_id']). "'";
    preg_replace - vendor/statix/stubs/CoreGenericFunctions.phpstub:1182:10
    function preg_replace($pattern, $replacement, $subject, int $limit = -1, &$count = null) {}
    concat - src/panel.php:19:9
    $sql2 = "SELECT id, text FROM logs WHERE id='".preg_replace('/[^a-z0-9A-Z"]/', "", $_GET['log_id']). "'";
    concat - src/panel.php:19:9
    $sql2 = "SELECT id, text FROM logs WHERE id='".preg_replace('/[^a-z0-9A-Z"]/', "", $_GET['log_id']). "'";
    $sql2 - src/panel.php:19:1
```


## SAST in the Development Cycle

### **Integrating Static Application Security Testing (SAST) into the Development Cycle**

#### **Overview of SAST in the Development Lifecycle**

Static Application Security Testing (SAST) is one of the first security measures implemented during the software development lifecycle. It is commonly integrated during the coding phase, which is beneficial because SAST tools don't require a fully functional application to identify vulnerabilities. By using SAST early, you can detect security issues as soon as possible, even in early code stages.

SAST can be integrated into the development process in several ways, depending on the project requirements:

- **CI/CD Integration**: This method involves incorporating SAST tools into the continuous integration and continuous delivery (CI/CD) pipeline. Whenever a pull request (PR) or a merge occurs, the SAST tools automatically analyze the code for vulnerabilities. This ensures that the code being merged has gone through a basic security check. To avoid performance issues in the development pipeline, some teams opt to run SAST scans only during the merge process rather than for every pull request, reducing wait times for developers.
  
- **IDE Integration**: In this method, SAST tools are integrated into the developers' integrated development environments (IDEs), allowing for real-time code analysis. This proactive approach enables developers to fix security issues as they write the code, preventing the accumulation of vulnerabilities later in the project. You may want to use both IDE and CI/CD-based SAST tools. IDE integrations are typically for basic structural checks and secure coding practices, while CI/CD tools might run more advanced analyses, like dataflow and taint analysis, which require more time and resources.

For further details on how security tools can be integrated into CI/CD pipelines, you may want to refer to resources about integrating Dynamic Application Security Testing (DAST) tools into CI/CD systems, such as Jenkins. The integration process for SAST is similar, and we will not delve into it here.

#### **Integrating SAST into IDEs**

To facilitate early-stage detection of vulnerabilities, the use of SAST tools directly within your IDE can be very effective. For example, if you are using a virtual machine (VM) with **VS Code**, it comes pre-configured with a couple of SAST tools:

1. **StaticLinter**: One of the SAST tools integrated with VS Code. StaticLinter is configured to perform real-time static analysis as you write code. By simply typing in the editor, StaticLinter will immediately flag any issues it detects, mirroring the alerts you would see in the command-line version. While it doesn’t run advanced dataflow analysis (like taint analysis), it is helpful for identifying basic structural issues and coding practices that improve code quality. 

2. **CodeGuard**: Another useful SAST tool that can be added to VS Code directly from the Visual Studio Marketplace. Similar to StaticLinter, CodeGuard provides inline security alerts as you type, displaying detected issues within your code. CodeGuard also allows you to define custom security rules, enabling it to be tailored to your specific project needs. For example, you can access the custom rule set in the project’s `custom-rules` directory. You don’t need to worry about customizing rules for now, but you can examine the rules set for the current project if needed.

Both **StaticLinter** and **CodeGuard** are valuable for proactive security. They show detected issues inline in the code as you write, helping you address problems before they become ingrained in the project. The main difference between the two tools is that **CodeGuard** scans all files when VS Code starts, displaying issues across the project, whereas **StaticLinter** only scans the file currently open in the editor.

Once installed and configured, both tools add visual indicators within the IDE to help developers spot issues quickly. For example, whenever there’s an issue with a specific line of code, an alert appears next to that line, and hovering over it provides more details about the problem.

#### **Using SAST Tools in VS Code**

Here’s how you can use the tools within VS Code:

1. **Inline Alerts**: For every line with a detected issue, you will see a small warning icon or a line number highlight. Hovering over the highlighted issue will give you a description of the problem.
   
   For instance, if there’s an issue in **`login.php`** at line 46, you can hover over that line to view details like this:

   - **Detected Issue**: Possible SQL Injection vulnerability on line 46 in **login.php**.
   - **Description**: User input is being passed to an SQL query without validation or sanitization.

2. **Error List**: You can view a complete list of detected issues by clicking on the **Errors** indicator at the bottom of the VS Code interface. This provides a central overview of all the issues detected by the SAST tools in your current code, making it easy to navigate between problems.

By having these tools integrated directly into your IDE, you ensure that security issues are addressed as they arise, significantly improving the quality and security of the code. It’s a proactive approach that helps developers write secure code without needing to wait until later stages of the development cycle.

#### **Conclusion**

Using **StaticLinter** and **CodeGuard** within your IDE, alongside CI/CD-based SAST tools, can greatly enhance the security of your application from the beginning of the development lifecycle. By flagging issues early and enabling developers to address vulnerabilities in real-time, these tools help ensure cleaner, more secure code. Whether you opt for one or both tools in your workflow depends on your project’s needs, but integrating SAST into both your IDE and CI/CD pipeline provides comprehensive coverage.