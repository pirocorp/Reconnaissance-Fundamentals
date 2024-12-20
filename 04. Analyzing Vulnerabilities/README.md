# Analyzing Vulnerabilities

Vulnerabilities are, at their core, poorly written code. The better you are with coding, the more you can understand everything. Vulnerabilities are a core concept in cyber security. On one hand, they must be mitigated/patched, and on the other, they must be exploited. Vulnerabilities can arise from literally everywhere! Never think, "There is no way that will work." Guess what, it is a way! Try it out!

## Path traversal

Path traversal is also known as directory traversal. These vulnerabilities enable an attacker to read arbitrary files on the server that is running an application. This might include:

- Application code and data.
- Credentials for back-end systems.
- Sensitive operating system files.

In some cases, an attacker might be able to write to arbitrary files on the server, allowing them to modify application data or behavior and ultimately take complete control of the server.

Example:

```URL
https://insecure-website.com/loadImage?filename=../../../etc/passwd
```

This causes the application to read from the following file path: 

```bash
/var/www/images/../../../etc/passwd
```

This standard file on Unix-based operating systems contains details of the server's registered users. Still, an attacker could retrieve other arbitrary files using the same technique.


## Access Control

Access control applies constraints on who or what is authorized to perform actions or access resources. In the context of web applications, access control is dependent on authentication and session management:

- **Authentication** confirms that the user is who they say they are.
- **Session management** identifies which user makes subsequent HTTP requests.
- **Access control** determines whether the user can perform the action they are attempting to perform.

Broken access controls are common and often present a critical security vulnerability. Access control design and management are complex and dynamic problems that apply business, organizational, and legal constraints to a technical implementation. Access control design decisions have to be made by humans, so the potential for errors is high.

### Vertical privilege escalation

If a user can gain access to functionality, they are not permitted to access it. This is called vertical privilege escalation. For example, if a non-administrative user can access an admin page where they can delete user accounts, then this is vertical privilege escalation.

#### Unprotected functionality

At its most basic, vertical privilege escalation arises when an application does not enforce any protection for sensitive functionality. For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page. However, users can access the administrative functions by browsing the relevant admin URL.

For example, a website might host sensitive functionality at the following URL:

```URL
https://insecure-website.com/admin
```

This might be accessible by any user, not only administrative users who have a link to the functionality in their user interface. In some cases, the administrative URL might be disclosed in other locations, such as the robots.txt file:

```URL
https://insecure-website.com/robots.txt
```

Even if the URL isn't disclosed anywhere, an attacker may be able to use a wordlist to brute-force the location of the sensitive functionality.

Sometimes, sensitive functionality is concealed by giving it a less predictable URL. This is an example of so-called "security by obscurity." However, hiding sensitive functionality does not provide adequate access control because users might discover the obfuscated URL in several ways.

Imagine an application that hosts administrative functions at the following URL:

```URL
https://insecure-website.com/administrator-panel-yb556
```

This might not be directly guessable by an attacker. However, the application might still leak the URL to users. The URL might be disclosed in JavaScript that constructs the user interface based on the user's role:

```HTML
<script>
	var isAdmin = false;
	if (isAdmin) {
		...
		var adminPanelTag = document.createElement('a');
		adminPanelTag.setAttribute('href', 'https://insecure-website.com/administrator-panel-yb556');
		adminPanelTag.innerText = 'Admin panel';
		...
	}
</script>
```

This script adds a link to the user's UI if they are an admin user. However, the script containing the URL is visible to all users regardless of their role.


#### Parameter-based access control methods

Some applications determine the user's access rights or role at login and store this information in a user-controllable location. This could be:

- A hidden field.
- A cookie.
- A preset query string parameter.

The application makes access control decisions based on the submitted value. For example:

```URL
https://insecure-website.com/login/home.jsp?admin=true
https://insecure-website.com/login/home.jsp?role=1
```

This approach is insecure because users, such as administrative functions, can modify the value and access functionality they're not authorized to.

### Horizontal privilege escalation

Horizontal privilege escalation occurs if a user can gain access to resources belonging to another user instead of their resources of that type. For example, if an employee can access the records of other employees and their own, then this is horizontal privilege escalation.

Horizontal privilege escalation attacks may use similar types of exploit methods to vertical privilege escalation. For example, a user might access their account page using the following URL:

```URL
https://insecure-website.com/myaccount?id=123
```

If an attacker modifies the ```id``` parameter value to that of another user, they might gain access to another user's account page and the associated data and functions.

> **Note** This is an example of an insecure direct object reference (IDOR) vulnerability. This type of vulnerability arises when user-controller parameter values are used to access resources or functions directly.

In some applications, the exploitable parameter does not have a predictable value. For example, an application might use globally unique identifiers (GUIDs) instead of an incrementing number to identify users. This may prevent an attacker from guessing or predicting another user's identifier. However, the GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced, such as user messages or reviews.

### Horizontal to vertical privilege escalation

Often, a horizontal privilege escalation attack can be turned into a vertical privilege escalation by compromising a more privileged user. For example, a horizontal escalation might allow an attacker to reset or capture another user's password. If the attacker targets an administrative user and compromises their account, they can gain administrative access and perform vertical privilege escalation.

An attacker might be able to gain access to another user's account page using the parameter tampering technique already described for horizontal privilege escalation:

```URL
https://insecure-website.com/myaccount?id=456
```

The attacker will gain access to an administrative account page if the target user is an application administrator. This page might disclose the administrator's password, provide a means of changing it, or provide direct access to privileged functionality.


## Authentication vulnerabilities

Authentication vulnerabilities are easy to understand conceptually. However, they are usually critical because of the precise relationship between authentication and security.

Authentication vulnerabilities allow attackers to access sensitive data and functionality and expose an additional attack surface for further exploits. For this reason, it's essential to learn how to identify and exploit authentication vulnerabilities and bypass standard protection measures.


### What is the difference between authentication and authorization?

**Authentication** verifies that a user is who they claim to be. **Authorization** involves verifying whether a user is allowed to do something.

### Brute-force attacks

A brute-force attack is when an attacker uses a trial-and-error system to guess valid user credentials. These attacks are typically automated using wordlists of usernames and passwords. Automating this process, especially using dedicated tools, potentially enables an attacker to make many login attempts quickly.

Brute-forcing is not always a case of making completely random guesses at usernames and passwords. Using basic logic or publicly available knowledge, attackers can fine-tune brute-force attacks to make much more educated guesses, considerably increasing their efficiency. Websites that rely on password-based login as their sole method of authenticating users can be highly vulnerable if they do not implement sufficient brute-force protection.

#### Brute-forcing usernames

Usernames are especially easy to guess if they conform to a recognizable pattern, such as an email address. For example, it is very common to see business logins in the format `firstname.lastname@somecompany.com`. However, even with no apparent pattern, sometimes high-privileged accounts are created using predictable usernames, such as `admin` or `administrator`.

During auditing, check whether the website discloses potential usernames publicly. For example, are you able to access user profiles without logging in? Even if the actual content of the profiles is hidden, the name used in the profile is sometimes the same as the login username. You should also check HTTP responses to see if any email addresses are disclosed. Occasionally, responses contain email addresses of high-privileged users, such as administrators or IT support.

#### Brute-forcing passwords

Passwords can similarly be brute-forced, with the difficulty varying based on the password's strength. Many websites adopt some form of password policy, which forces users to create high-entropy passwords that are, theoretically, at least, more challenging to crack using brute force alone. This typically involves enforcing passwords with the following:

- A minimum number of characters
- A mixture of lower and uppercase letters
- At least one special character

However, while high-entropy passwords are complex for computers alone to crack, we can use a basic knowledge of human behavior to exploit the vulnerabilities that users unwittingly introduce to this system. Rather than creating a strong password with a random combination of characters, users often take a password they can remember and try to crowbar it to fit the password policy. For example, if `mypassword` is not allowed, users may try something like `Mypassword1!` or `Myp4$$w0rd` instead.

In cases where the policy requires users to change their passwords regularly, it is common for users to make minor, predictable changes to their preferred password. For example, `Mypassword1!` becomes `Mypassword1?` or `Mypassword2!`.

This knowledge of likely credentials and predictable patterns means that brute-force attacks can often be much more sophisticated and effective than simply iterating through every possible combination of characters.

### Username enumeration

Username enumeration occurs when an attacker can observe changes in the website's behavior and identify whether a given username is valid.

Username enumeration typically occurs on the login page, for example, when you enter a valid username but an incorrect password or on registration forms when you enter a username already taken. This dramatically reduces the time and effort required to brute-force a login because the attacker can quickly generate a shortlist of valid usernames.

### Bypassing two-factor authentication

At times, the implementation of two-factor authentication is flawed to the point where it can be bypassed entirely.

If the user is first prompted to enter a password and then prompted to enter a verification code on a separate page, the user is effectively in a "logged in" state before entering the verification code. In this case, it is worth testing to see if you can directly skip to "logged-in only" pages after completing the first authentication step. Occasionally, a website needs to check whether or not you completed the second step before loading the page.


## Server-side Request Forgery (SSRF)

Server-side request forgery is a web security vulnerability allowing an attacker to cause the server-side application to request an unintended location.

In a typical SSRF attack, the attacker might cause the server to connect to internal-only services within the organization's infrastructure. In other cases, they may be able to force the server to connect to arbitrary external systems. This could leak sensitive data, such as authorization credentials.


### SSRF attacks against the server

In an SSRF attack against the server, the attacker causes the application to make an HTTP request back to the server hosting it via its loopback network interface. This typically involves supplying a URL with a hostname like `127.0.0.1` (a reserved IP address that points to the loopback adapter) or `localhost` (a commonly used name for the same adapter).

For example, imagine a shopping application that lets the user view whether an item is in stock in a particular store. The application must query various back-end REST APIs to provide the stock information. It passes the URL to the relevant back-end API endpoint via a front-end HTTP request. When a user views the stock status for an item, their browser makes the following request:

```HTTP
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
```

This causes the server to request the specified URL, retrieve the stock status, and return this to the user.

In this example, an attacker can modify the request to specify a URL local to the server:

```HTTP
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://localhost/admin
```

The server fetches the contents of the `/admin` URL and returns it to the user.

An attacker can visit the `/admin` URL, but the administrative functionality is usually only accessible to authenticated users. This means an attacker won't see anything of interest. However, the normal access controls are bypassed if the request to the `/admin` URL comes from the local machine. The application grants full access to the administrative functionality because the request appears to originate from a trusted location.

Why do applications behave this way and implicitly trust requests from the local machine? This can arise for various reasons:

- The access control check might be implemented in a different component before the application server. The check is bypassed when a connection is made back to the server.
- For disaster recovery purposes, the application might allow administrative access, without logging in, to any user coming from the local machine. This allows an administrator to recover the system if they lose their credentials. This assumes that only a fully trusted user would come directly from the server.
- The administrative interface might listen on a different port number from the main application and might not be reachable directly by users.

These trust relationships, where requests originating from the local machine are handled differently than ordinary requests, often make SSRF a critical vulnerability.

### SSRF attacks against other back-end systems

Sometimes, the application server can interact with back-end systems that users cannot directly reach. These systems often have non-routable private IP addresses. The network topology normally protects the back-end systems, so they often have a weaker security posture. In many cases, internal back-end systems contain sensitive functionality that can be accessed without authentication by anyone who can interact with the systems.

In the previous example, imagine an administrative interface at the back-end URL `https://192.168.0.68/admin`. An attacker can submit the following request to exploit the SSRF vulnerability and access the administrative interface:

```HTTP
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://192.168.0.68/admin
```

## File Upload Vulnerabilities

File upload vulnerabilities are when a web server allows users to upload files to its filesystem without sufficiently validating their name, type, contents, or size. Failing to enforce restrictions on these properly could mean that even an essential image upload function can be used to upload arbitrary and potentially dangerous files instead. This could even include server-side script files that enable remote code execution.

In some cases, uploading the file is enough to cause damage. Other attacks may involve a follow-up HTTP request for the file, typically to trigger the server's execution.

### How do file upload vulnerabilities arise?

Given the apparent dangers, it's rare for websites in the wild to have no restrictions whatsoever on which files users can upload. More commonly, developers implement what they believe to be robust validation that is either inherently flawed or can be easily bypassed.

For example, they may attempt to blacklist dangerous file types but fail to account for parsing discrepancies when checking the file extensions. As with any blacklist, it's also easy to accidentally omit more obscure file types that may still be dangerous.

In other cases, the website may attempt to check the file type by verifying properties that an attacker can easily manipulate using tools like [Burp Proxy](https://portswigger.net/burp/documentation/desktop/tools/proxy) or [Repeater](https://portswigger.net/burp/documentation/desktop/tools/repeater).

Ultimately, even robust validation measures may be applied inconsistently across the website's network of hosts and directories, resulting in discrepancies that can be exploited.

### Exploiting unrestricted file uploads to deploy a web shell

From a security perspective, the worst scenario is when a website allows you to upload server-side scripts, such as PHP, Java, or Python files, and is configured to execute them as code. This makes it trivial to create your web shell on the server.

> **Web shell**
> 
> A web shell is a malicious script that enables an attacker to execute arbitrary commands on a remote web server simply by sending HTTP requests to the correct endpoint.

If you can successfully upload a web shell, you effectively have complete control over the server. This means you can read and write arbitrary files, exfiltrate sensitive data, and even use the server to pivot attacks against internal infrastructure and servers outside the network. For example, the following PHP one-liner could be used to read arbitrary files from the server's filesystem:

```php
<?php echo file_get_contents('/path/to/target/file'); ?>
```
Once uploaded, sending a request for this malicious file will return the contents of the target file in the response.

A more versatile web shell may look something like this:

```php
<?php echo system($_GET['command']); ?>
```

This script enables you to pass an arbitrary system command via a query parameter as follows:

```HTTP
GET /example/exploit.php?command=id HTTP/1.1
```

### Flawed file type validation

When submitting HTML forms, the browser typically sends the provided data in a POST request with the content type `application/x-www-form-url-encoded`. This is fine for sending simple text like your name or address. However, it isn't suitable for sending large amounts of binary data, such as an entire image or PDF document. The content type `multipart/form-data` is preferred in this case.

Consider a form containing fields for uploading an image, providing a description, and entering your username. Submitting such a form might result in a request that looks something like this:

```HTTP
POST /images HTTP/1.1
Host: normal-website.com
Content-Length: 12345
Content-Type: multipart/form-data; boundary=---------------------------012345678901234567890123456

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="image"; filename="example.jpg"
Content-Type: image/jpeg

[...binary content of example.jpg...]

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="description"

This is an interesting description of my image.

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="username"

wiener
---------------------------012345678901234567890123456--
```

As you can see, the message body is split into separate parts for each of the form's inputs. Each part contains a `Content-Disposition` header, which provides basic information about the input field it relates to. These individual parts may also include their own `Content-Type` header, which tells the server the MIME type of the submitted data using this input.

One way that websites may attempt to validate file uploads is to check that this input-specific `Content-Type` header matches an expected MIME type. For example, if the server only expects image files, it may only allow types like `image/jpeg` and `image/png`. Problems can arise when the server implicitly trusts the value of this header. If no further validation is performed to check whether the file's contents match the supposed MIME type, this defense can be easily bypassed using tools like [Burp Repeater](https://portswigger.net/burp/documentation/desktop/tools/repeater).


## OS command injection

OS command injection, or shell injection, allows an attacker to execute operating system (OS) commands on the server running an application, typically fully compromising the application and its data. Often, an attacker can leverage an OS command injection vulnerability to compromise other parts of the hosting infrastructure and exploit trust relationships to pivot the attack to other systems within the organization.

### Useful commands

After you identify an OS command injection vulnerability, executing some initial commands to obtain information about the system is helpful. Below is a summary of some commands that are useful on Linux and Windows platforms:

|   Purpose of command  |    Linux    |    Windows    |
|:---------------------:|:-----------:|:-------------:|
| Name of current user  | whoami      | whoami        |
| Operating system      | uname -a    | ver           |
| Network configuration | ifconfig    | ipconfig /all |
| Network connections   | netstat -an | netstat -an   |
| Running processes     | ps -ef      | tasklist      |

### Injecting OS commands

In this example, a shopping application lets the user view whether an item is in stock in a particular store. This information is accessed via a URL:

```URL
https://insecure-website.com/stockStatus?productID=381&storeID=29
```

To provide the stock information, the application must query various legacy systems. For historical reasons, the functionality is implemented by calling out to a shell command with the product and store IDs as arguments:

```bash
stockreport.pl 381 29
```

This command outputs the stock status for the specified item, which is returned to the user. The application implements no defenses against OS command injection, so an attacker can submit the following input to execute an arbitrary command:

```bash
& echo aiwefwlguh &
```

If this input is submitted in the `productID` parameter, the command executed by the application is:

```bash
stockreport.pl & echo aiwefwlguh & 29
```

The `echo` command causes the supplied string to be echoed in the output. This is a valuable way to test for some types of OS command injection. The `&` character is a shell command separator. This example causes three separate commands to execute, one after another. The output returned to the user is:

```bash
Error - productID was not provided
aiwefwlguh
29: command not found
```

The three lines of output demonstrate that:

- The original `stockreport.pl` command was executed without expected arguments, so an error message was returned.
- The injected `echo` command was executed, and the supplied string was echoed in the output.
- The original argument `29` was executed as a command, which caused an error.

Placing the additional command separator `&` after the injected command is helpful because it separates the injected command from whatever follows the injection point. This reduces the chance that what follows will prevent the injected command from executing.


## SQL injection (SQLi)

SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with an application's database queries. This can allow an attacker to view data they cannot typically retrieve, including data belonging to other users or any other data the application can access. An attacker can often modify or delete this data, causing persistent changes to the application's content or behavior.

Sometimes, an attacker can escalate a SQL injection attack to compromise the underlying server or other back-end infrastructure. It can also enable them to perform denial-of-service attacks.

### How to detect SQL injection vulnerabilities

You can detect SQL injection manually using a systematic set of tests against every entry point in the application. To do this, you would typically submit:

- The single quote character `'` and look for errors or other anomalies.
- Some SQL-specific syntax evaluates the entry point's base (original) value and sets it to a different value, looking for systematic differences in the application responses.
- Boolean conditions such as `OR 1=1` and `OR 1=2`, and look for differences in the application's responses.
- Payloads are designed to trigger time delays when executed within an SQL query, and they look for differences in the time taken to respond.
- OAST payloads are designed to trigger an out-of-band network interaction when executed within a SQL query and monitor any resulting interactions.
  
Alternatively, you can quickly and reliably find most SQL injection vulnerabilities using [Burp Scanner](https://portswigger.net/burp/documentation/scanner).

### Retrieving hidden data

Imagine a shopping application that displays products in different categories. When the user clicks on the Gifts category, their browser requests the URL:

```URL
https://insecure-website.com/products?category=Gifts
```

This causes the application to make a SQL query to retrieve details of the relevant products from the database:

```SQL
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```

The restriction `released = 1` is being used to hide products that have not been released. We could assume that `released = 0` applies to unreleased products.

The application doesn't implement any defenses against SQL injection attacks. This means an attacker can construct the following attack, for example:

```URL
https://insecure-website.com/products?category=Gifts'--
```

This results in the SQL query:

```SQL
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
```

Note that `--` is a comment indicator in SQL. This means that the rest of the query is interpreted as a comment, effectively removing it. This example implies the query no longer includes `AND released = 1`. As a result, all products are displayed, including those not yet released.

You can use a similar attack to cause the application to display all the products in any category, including categories that they don't know about:

```URL
https://insecure-website.com/products?category=Gifts'+OR+1=1--
```

This results in the SQL query:

```SQL
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```

The modified query returns all items where the `category` is `Gifts`, or `1` is equal to `1`. The query returns all items as `1=1` is always `true`.


> **Warning**
>
> Take care when injecting the condition `OR 1=1` into an SQL query. Even if it appears harmless in the context you're injecting into, it's common for applications to use data from a single request in multiple queries. For example, if your condition reaches an `UPDATE` or `DELETE` statement, it can result in an accidental data loss.


### Subverting application logic

Imagine an application that lets users log in with a username and password. If a user submits the username `wiener` and the password `bluecheese`, the application checks the credentials by performing the following SQL query:

```SQL
SELECT * FROM users WHERE username = 'wiener' AND password = 'bluecheese'
```

The login is successful if the query returns the user's details. Otherwise, it is rejected. 

In this case, an attacker can log in as any user without a password. They can do this using the SQL comment sequence `--` to remove the password check from the query's WHERE clause. For example, submitting the username `administrator'--` and a blank password results in the following query:

```SQL
SELECT * FROM users WHERE username = 'administrator'--' AND password = ''
```

This query returns the user whose `username` is `administrator` and successfully logs the attacker in as that user.


