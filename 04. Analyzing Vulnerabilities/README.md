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

