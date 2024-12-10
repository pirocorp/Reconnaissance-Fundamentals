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

If the user is first prompted to enter a password and then prompted to enter a verification code on a separate page, the user is effectively in a "logged in" state before entering the verification code. In this case, it is worth testing to see if you can directly skip to "logged-in only" pages after completing the first authentication step. Occasionally, a website doesn't check whether or not you completed the second step before loading the page.





